# Создание и выполнение потоков

Для создания нового потока мы можем создать новый класс, либо наследуя его от класса Thread, либо реализуя в классе интерфейс **Runnable**

---

### Наследование от класса Thread

Создадим свой класс на основе Thread:

```java
class MyThread extends Thread {
      
    MyThread(String name) {
        super(name);
    }
      
    public void run() {
        
        System.out.printf("%s started\n", Thread.currentThread().getName());
        try{
            Thread.sleep(2000);
        } catch(InterruptedException e){
            System.out.println("Thread interrupted");
        }
        System.out.printf("%s finished\n", Thread.currentThread().getName());
    }
}

public class Program {
  
    public static void main(String[] args) {
        System.out.println("Main thread started");
        new MyThread("My Own Thread").start();
        System.out.println("Main thread finished");
    }
}
```

Класс потока называется **MyThread**. 
В конструктор класса передается имя потока, которое затем передается в конструктор базового класса.
В конструктор своего класса потока мы можем передать различные данные,
но главное, чтобы в нем вызывался конструктор базового класса Thread, в который передается имя потока.

И также в **MyThread** переопределяется метод `run()`, код которого собственно и будет представлять весь тот код,
который выполняется в потоке.

В методе `main()` для запуска потока **MyThread** у него вызывается метод `start()`, после чего начинается выполнение того кода,
который определен в методе `run()`

Аналогично созданию одного потока мы можем запускать сразу несколько потоков:

```java
public static void main(String[] args) {
    System.out.println("Main thread started");
    for(int i=1; i < 6; i++) {
        new MyThread("My Own Thread  " + i).start();
    }
    System.out.println("Main thread finished");
}
```

---

### Ожидание завершения потока

При запуске потоков в примерах выше **Main thread** завершался до дочернего потока.
Как правило, более распространенной ситуацией является случай, когда **Main thread** завершается самым последним.
Для этого надо применить метод `join()`.

В данном примере текущий поток будет ожидать завершения потока, для которого вызван метод `join()`:

```java
public static void main(String[] args) {
    System.out.println("Main thread started");
    MyThread t = new MyThread("My Own Thread");
    t.start();
    try{
        t.join(); 
    } catch(InterruptedException e){
        System.out.printf("%s interrupted", t.getName());
    }
    System.out.println("Main thread finished");
}
```

Метод `join()` заставляет вызвавший поток (**Main thread**) ожидать завершения вызываемого потока,
для которого и применяется метод `join()`

Если в программе используется несколько дочерних потоков, и надо, чтобы **Main thread** завершался после дочерних,
то для каждого дочернего потока надо вызвать метод `join()`

---

### Реализация интерфейса Runnable

Другой способ определения потока представляет реализация интерфейса **Runnable**.
Интерфейс имеет один метод `run()`

```java
interface Runnable {
    void run();
}
```

В методе `run()` собственно определяется весь тот код, который выполняется при запуске потока.

После определения объекта **Runnable** он передается в один из конструкторов класса **Thread**:

```java
class MyThread implements Runnable {
    public void run(){
        System.out.printf("%s started\n", Thread.currentThread().getName());
        try {
            Thread.sleep(2000);
        } catch(InterruptedException e){
            System.out.println("Thread interrupted");
        }
        System.out.printf("%s finished\n", Thread.currentThread().getName());
    }
} 
  
public class Program {
  
    public static void main(String[] args) {
        System.out.println("Main thread started");
        new Thread(new MyThread(),"My Own Thread").start();
        System.out.println("Main thread finished");
    }
}
```

Реализация интерфейса **Runnable** во многом аналогична переопределению класса **Thread**.
Также в методе `run()` определяется простейший код, который усыпляет поток на 2000 миллисекунд.

В методе `main()` вызывается конструктор **Thread**, в который передается объект **MyThread**.
И чтобы запустить поток, вызывается метод `start()`

Поскольку **Runnable** фактически представляет функциональный интерфейс, который определяет один метод,
то объект этого интерфейса мы можем представить в виде лямбда-выражения:

```java
public class Program {
    public static void main(String[] args) {
        System.out.println("Main thread started");
        Runnable r = () -> {
            System.out.printf("%s started\n", Thread.currentThread().getName());
            try {
                Thread.sleep(2000);
            } catch(InterruptedException e){
                System.out.println("Thread interrupted");
            }
            System.out.printf("%s finished\n", Thread.currentThread().getName());
        };
        Thread myThread = new Thread(r, "My Own Thread").start();
        System.out.println("Main thread finished");
    }
}
```

---

### [Назад к оглавлению](./README.md)