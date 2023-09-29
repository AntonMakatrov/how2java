# Синхронизация потоков. Оператор synchronized

При работе потоки нередко обращаются к каким-то общим ресурсам, которые определены вне потока, например, обращение к какому-то файлу.
Если одновременно несколько потоков обратятся к общему ресурсу,
то результаты выполнения программы могут быть неожиданными и даже непредсказуемыми

```java
public class Program {
 
    public static void main(String[] args) {
        ClassA classA= new ClassA();
        for (int i = 1; i < 6; i++) {
            Thread t = new Thread(new ThreadCounter(classA));
            t.setName("Thread "+ i);
            t.start();
        }
    }
}
 
class ClassA {
    int x = 0;
}
 
class ThreadCounter implements Runnable {
    ClassA a;
    ThreadCounter(ClassA a) {
        this.a = a;
    }
    public void run(){
        a.x = 1;
        for (int i = 1; i < 5; i++) {
            System.out.printf("%s %d \n", Thread.currentThread().getName(), a.x);
            a.x++;
            try{
                Thread.sleep(1000);
            } catch(InterruptedException e){
                e.printStackTrace();
            }
        }
    }
}
```

То есть пока один поток не окончил работу с полем `a.x`, с ним начинает работать другой поток.

Чтобы избежать подобной ситуации, надо синхронизировать потоки.
Одним из способов синхронизации является использование ключевого слова **synchronized**.
Этот оператор предваряет блок кода или метод, который подлежит синхронизации.
Для его применения изменим класс ThreadCounter:

```java
class ThreadCounter implements Runnable {
    ClassA a;
    ThreadCounter(ClassA a) {
        this.a = a;
    }
    public void run(){
        synchronized (a) {
            a.x = 1;
            for (int i = 1; i < 5; i++) {
                System.out.printf("%s %d \n", Thread.currentThread().getName(), a.x);
                a.x++;
                try{
                    Thread.sleep(1000);
                } catch(InterruptedException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

При создании синхронизированного блока кода после оператора **synchronized** идет объект-заглушка `synchronized(res)`.
Причем в качестве объекта может использоваться только объект какого-нибудь класса, но не примитивного типа.

Каждый объект в Java имеет ассоциированный с ним монитор.
Монитор представляет своего рода инструмент для управления доступа к объекту.
Когда выполнение кода доходит до оператора **synchronized**, монитор объекта **classA** блокируется,
и на время его блокировки монопольный доступ к блоку кода имеет только один поток, который и произвел блокировку.
После окончания работы блока кода, монитор объекта **classA** освобождается и становится доступным для других потоков.

После освобождения монитора его захватывает другой поток, а все остальные потоки продолжают ожидать его освобождения.

При применении оператора **synchronized** к методу пока этот метод не завершит выполнение,
монопольный доступ имеет только один поток - первый, который начал его выполнение.
Пример использоваия synchronized к методу:

```java
public class Program {
 
    public static void main(String[] args) {
        ClassA classA= new ClassA();
        for (int i = 1; i < 6; i++) {
            Thread t = new Thread(new ThreadCounter(classA));
            t.setName("Thread "+ i);
            t.start();
        }
    }
}
class ClassA {
    int x = 0;
    synchronized void inc(){
        x = 1;
        for (int i = 1; i < 5; i++) {
            System.out.printf("%s %d \n", Thread.currentThread().getName(), x);
            x++;
            try {
                Thread.sleep(1000);
            } catch(InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
 
class ThreadCounter implements Runnable {
    ClassA a;
    ThreadCounter(ClassA a) {
        this.a = a;
    }
    public void run(){
        a.inc();
    }
}
```

Результат работы в данном случае будет аналогичен примеру выше с блоком **synchronized**.
Здесь опять в дело вступает монитор объекта **ClassA** - общего объекта для всех потоков.
Поэтому синхронизированным объявляется не метод `run()` в классе **ThreadCounter**, а метод `inc()` класса **a**.
Когда первый поток начинает выполнение метода `inc()`, он захватывает монитор объекта **a**.
А все потоки также продолжают ожидать его освобождения.

---

### [Назад к оглавлению](./README.md)
