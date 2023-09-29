# Семафоры

Семафоры представляют еще одно средство синхронизации для доступа к ресурсу.
В Java семафоры представлены классом **Semaphore**, который располагается в пакете `java.util.concurrent`.

Для управления доступом к ресурсу семафор использует счетчик, представляющий количество разрешений.
Если значение счетчика больше нуля, то поток получает доступ к ресурсу, при этом счетчик уменьшается на единицу.
После окончания работы с ресурсом поток освобождает семафор, и счетчик увеличивается на единицу.
Если же счетчик равен нулю, то поток блокируется и ждет, пока не получит разрешение от семафора.

Установить количество разрешений для доступа к ресурсу можно с помощью конструкторов класса **Semaphore**:

```java
Semaphore(int permits)
Semaphore(int permits, boolean fair)
```

Параметр `permits` указывает на количество допустимых разрешений для доступа к ресурсу.
Параметр `fair` во втором конструкторе позволяет установить очередность получения доступа.
Если он равен **true**, то разрешения будут предоставляться ожидающим потокам в том порядке, в каком они запрашивали доступ.
Если же он равен **false**, то разрешения будут предоставляться в неопределенном порядке.

Для получения разрешения у семафора надо вызвать метод `acquire()`, который имеет две формы

```java
void acquire() throws InterruptedException
void acquire(int permits) throws InterruptedException
```

Для получения одного разрешения применяется первый вариант, а для получения нескольких разрешений - второй вариант.
После вызова этого метода пока поток не получит разрешение, он блокируется.

После окончания работы с ресурсом полученное ранее разрешение надо освободить с помощью метода `release()`

```java
void release()
void release(int permits)
```

Первый вариант метода освобождает одно разрешение, а второй вариант - количество разрешений, указанных в `permits`.

Пример использования семафора

```java
import java.util.concurrent.Semaphore;
 
public class Program {
 
    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(1); // 1 разрешение
        ClassA classA = new ClassA();
        for (int i = 1; i < 5; i++) {
            new Thread(new CustomThread(classA, semaphore, "CustomThread " + i)).start();
        }
    }
}
class ClassA {
    int x = 0;  
}
 
class CustomThread implements Runnable {
    ClassA a;
    Semaphore semaphore;
    String name;

    CustomThread(ClassA a, Semaphore semaphore, String name) {
        this.a = a;
        this.semaphore = semaphore;
        this.name = name;
    }
      
    public void run() {
        try{
            System.out.println(name + " acquire acceptance");
            semaphore.acquire();
            res.x=1;
            for (int i = 1; i < 5; i++){
                System.out.println(this.name + " : " + a.x);
                a.x++;
                Thread.sleep(1000);
            }
        } catch(InterruptedException e){
            System.out.println(e.getMessage());
        }
        System.out.println(name + " release acceptance");
        semaphore.release();
    }
}
```

Здесь есть общий ресурс **ClassA** с полем x, которое изменяется каждым потоком.
Потоки представлены классом **CustomThread**, который получает семафор и выполняет некоторые действия над ресурсом. 
В основном классе программы эти потоки запускаются.

Семафоры отлично подходят для решения задач, где надо ограничивать доступ.
Например, классическая задача про обедающих философов.

Ее суть:  
есть несколько философов, допустим, пять, но одновременно за столом могут сидеть не более двух.
И надо, чтобы все философы пообедали, но при этом не возникло взаимоблокировки философами друг друга в борьбе за тарелку и вилку

```java
import java.util.concurrent.Semaphore;
 
public class Program {
    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(2);
        for(int i = 1; i < 6; i++) {
            new Philosopher(semaphore, i).start();
        }
    }
}
class Philosopher extends Thread {
    Semaphore semaphore;
    int eatingCount = 0;
    int id;
    Philosopher(Semaphore semaphore, int id) {
        this.semaphore = semaphore;
        this.id = id;
    }
     
    public void run() {
        try {
            while(eatingCount < 3) {
                semaphore.acquire(); 
                System.out.println("Philosopher " + id + " sitting to eat");
                sleep(1000);
                eatingCount++;
                System.out.println("Philosopher " + id + " going out");
                semaphore.release();
                sleep(1000);
            }
        } catch(InterruptedException e) {
            System.out.println ("Philosopher " + id + " has some problems");
        }
    }
}
```

В итоге только два философа смогут одновременно находиться за столом, а другие будут ждать

---

### [Назад к оглавлению](./README.md)