# Класс Phaser

Класс **Phaser** позволяет синхронизировать потоки, представляющие отдельную фазу или стадию выполнения общего действия.
**Phaser** определяет объект синхронизации, который ждет, пока не завершится определенная фаза.
Затем **Phaser** переходит к следующей стадии или фазе и снова ожидает ее завершения.

Конструкторы класса **Phaser**

```java
Phaser()
Phaser(int parties)
Phaser(Phaser parent)
Phaser(Phaser parent, int parties)
```

Параметр **parties** указывает на количество сторон (грубо говоря, потоков), которые должны выполнять все фазы действия.
Первый конструктор создает объект **Phaser** без каких-либо сторон.
Второй конструктор регистрирует передаваемое в конструктор количество сторон.
Третий и четвертый конструкторы также устанавливают родительский объект Phaser.

Основные методы класса Phaser:

-   `int register()` регистрирует сторону, которая выполняет фазы, и возвращает номер текущей фазы - обычно фаза 0
-   `int arrive()`:` сообщает, что сторона завершила фазу и возвращает номер текущей фазы
-   `int arriveAndAwaitAdvance()` аналогичен методу `arrive()`, только при этом заставляет **phaser** ожидать завершения фазы всеми остальными сторонами
-   `int arriveAndDeregister()` сообщает о завершении всех фаз стороной и снимает ее с регистрации.
    Возвращает номер текущей фазы или отрицательное число, если синхронизатор **Phaser** завершил свою работу
-   `int getPhase()` возвращает номер текущей фазы

При работае с классом **Phaser** обычно сначала создается его объект.
Далее нам надо зарегистрировать все участвующие стороны.
Для регистрации в каждой стороне вызывается метод `register()`, либо можно обойтись и без этого метода,
передав нужное количество сторон в конструктор **Phaser**.

Затем каждая сторона выполняет некоторый набор действий, составляющих фазу.
А синхронизатор **Phaser** ждет, пока все стороны не завершат выполнение фазы.
Чтобы сообщить синхронизатору, что фаза завершена, сторона должна вызвать метод `arrive()` или `arriveAndAwaitAdvance()`.
После этого синхронизатор переходит к следующей фазе.

Пример использования класса **Phaser**

```java
import java.util.concurrent.Phaser;
 
public class Program {
    public static void main(String[] args) {
        Phaser phaser = new Phaser(1);
        new Thread(new PhaseThread(phaser, "PhaseThread 1")).start();
        new Thread(new PhaseThread(phaser, "PhaseThread 2")).start();

        // waiting for finishing phase 0
        int phase = phaser.getPhase();
        phaser.arriveAndAwaitAdvance();
        System.out.println("Phase " + phase + " finished");
        // waiting for finishing phase 1
        phase = phaser.getPhase();
        phaser.arriveAndAwaitAdvance();
        System.out.println("Phase " + phase + " finished");
        // waiting for finishing phase 2
        phase = phaser.getPhase();
        phaser.arriveAndAwaitAdvance();
        System.out.println("Phase " + phase + " finished");

        phaser.arriveAndDeregister();
    }
}
 
class PhaseThread implements Runnable {
    Phaser phaser;
    String name;
    PhaseThread(Phaser phaser, String name){
        this.phaser = phaser;
        this.name = name;
        phaser.register();
    }
    public void run() {
        System.out.println(name + " running phase " + phaser.getPhase());
        phaser.arriveAndAwaitAdvance();

        System.out.println(name + " running phase " + phaser.getPhase());
        phaser.arriveAndAwaitAdvance();

        System.out.println(name + " running phase " + phaser.getPhase());
        phaser.arriveAndDeregister();
    }
}
```

Фазы выполняются тремя сторонами - главным потоком и двумя потоками **PhaseThread**.
Поэтому при создании объекта **Phaser** ему передается число `1` - главный поток,
а в конструкторе **PhaseThread** вызывается метод `register()`.
Можно и не использовать метод `register()`, но тогда нам надо было бы указать `Phaser phaser = new Phaser(3)`,
так как у нас три стороны.

Фаза в каждой стороне представляет минимальный примитивный набор действий:
для потоков **PhaseThread** это вывод сообщения, а для главного потока - подсчет текущей фазы с помощью метода `getPhase()`.
При этом отсчет фаз начинается с нуля.
Каждая сторона завершает выполнение фазы вызовом метода `phaser.arriveAndAwaitAdvance()`.
При вызове этого метода пока последняя сторона не завершит выполнение текущей фазы, все остальные стороны блокируются.

После завершения выполнения последней фазы происходит отмена регистрации всех сторон с помощью метода `arriveAndDeregister()`

В данном случае получается немного путанный вывод.
Так, сообщения о выполнении фазы `1` выводится после сообщения об окончании фазы `0`.
Что связано с многопоточностью - фазы завершились, но в одном потоке еще не выведено сообщение о завершении,
тогда как другие потоки уже начали выполнение следующей фазы.
В любом случае все это происходит уже после завершения фазы.

Чтобы было более наглядно, можно использовать `sleep()` в потоках

```java
public void run(){
         
        System.out.println(name + " running phase " + phaser.getPhase());
        phaser.arriveAndAwaitAdvance();
        try {
            Thread.sleep(100);
        } catch(InterruptedException ex) {
            System.out.println(ex.getMessage());
        }
         
        System.out.println(name + " running phase " + phaser.getPhase());
        phaser.arriveAndAwaitAdvance();
        try {
            Thread.sleep(100);
        } catch(InterruptedException ex) {
            System.out.println(ex.getMessage());
        }
        System.out.println(name + " running phase " + phaser.getPhase());
        phaser.arriveAndDeregister();
    }
```

---

### [Назад к оглавлению](./README.md)