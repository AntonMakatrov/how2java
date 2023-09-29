# Завершение и прерывание потока

Примеры потоков ранее представляли поток как последовательный набор операций.
После выполнения последней операции завершался и поток.
Однако нередко имеет место и другая организация потока в виде бесконечного цикла.
Например, поток сервера в бесконечном цикле прослушивает определенный порт на предмет получения данных.
И в этом случае мы также можем предусмотреть механизм завершения потока.

---

### Завершение потока

Распространенный способ завершения потока представляет опрос логической переменной.
И если она равна, например, **false**, то поток завершает бесконечный цикл и заканчивает свое выполнение.

Определим следующий класс потока:

```java
class MyThread implements Runnable {
      
    private boolean isActive;
      
    void disable(){
        isActive = false;
    }
      
    MyThread(){
       isActive = true;
    }
      
    public void run(){
        System.out.printf("%s started\n", Thread.currentThread().getName());
        int i = 1; // счетчик циклов
        while(isActive){
            System.out.println("i= " + i++);
            try {
                Thread.sleep(1000);
            } catch(InterruptedException e) {
                System.out.println("Thread has been interrupted");
            }
        }
        System.out.printf("%s finished\n", Thread.currentThread().getName());
    }
}
```

Переменная **isActive** указывает на активность потока.
С помощью метода `disable()` мы можем сбросить состояние этой переменной.

```java
public static void main(String[] args) {
    System.out.println("Main thread started");
    MyThread myThread = new MyThread();
    new Thread(myThread,"My Own Thread").start();
    try {
        Thread.sleep(2000);
        myThread.disable();
        Thread.sleep(3000);
    } catch(InterruptedException e) {
        System.out.println("Thread interrupted");
    }
    System.out.println("Main thread finished");
}
```

Итак, вначале запускается дочерний поток: `new Thread(myThread,"MyThread").start()`.
Затем на 2 секунды останавливается **Main thread** и потом вызываем метод **myThread.disable()**, который переключает в потоке флаг **isActive**.
И дочерний поток завершается.

---

### Метод interrupt

Еще один способ вызова завершения или прерывания потока представляет метод `interrupt()`.
Вызов этого метода устанавливает у потока статус, что он прерван.
Сам метод возвращает **true**, если поток может быть прерван, в ином случае возвращается **false**.

При этом сам вызов этого метода **НЕ** завершает поток, он только устанавливает статус:
в частности, метод `isInterrupted()` класса **Thread** будет возвращать значение **true**.
Мы можем проверить значение возвращаемое данным методом и прозвести некоторые действия

```java
class MyThread extends Thread {
    MyThread(String name) {
        super(name);
    }
    public void run(){
          
        System.out.printf("%s started\n", Thread.currentThread().getName());
        int i = 1;
        while(!isInterrupted()){
            System.out.println("i= " + i++);
        }
        System.out.printf("%s finished\n", Thread.currentThread().getName());
    }
}
public class Program {
  
    public static void main(String[] args) {
        System.out.println("Main thread started");
        MyThread t = new MyThread("My Own Thread");
        t.start();
        try{
            Thread.sleep(1500);
            t.interrupt();
            Thread.sleep(1500);
        } catch(InterruptedException e) {
            System.out.println("Thread interrupted");
        }
        System.out.println("Main thread finished");
    }
}
```

В классе, который унаследован от **Thread**, мы можем получить статус текущего потока с помощью метода `isInterrupted()`.
И пока этот метод возвращает **false**, мы можем выполнять цикл.
А после того, как будет вызван метод `interrupt()`, `isInterrupted()` возвратит **true**, и соответственно произойдет выход из цикла.

Если основная функциональность заключена в классе, который реализует интерфейс **Runnable**,
то там можно проверять статус потока с помощью метода `Thread.currentThread().isInterrupted()`:

```java
class MyThread implements Runnable {
    public void run() {
        System.out.printf("%s started\n", Thread.currentThread().getName());
        int i = 1;
        while(!Thread.currentThread().isInterrupted()) {
            System.out.println("i= " + i++);
        }
        System.out.printf("%s finished\n", Thread.currentThread().getName());
    }
}
public class Program {
    public static void main(String[] args) {
        System.out.println("Main thread started");
        MyThread myThread = new MyThread();
        Thread t = new Thread(myThread,"My Own Thread"); 
        t.start();
        try{
            Thread.sleep(1500);
            t.interrupt();
            Thread.sleep(1500);
        } catch(InterruptedException e) {
            System.out.println("Thread interrupted");
        }
        System.out.println("Main thread finished");
    }
}
```

Однако при получении статуса потока с помощью метода `isInterrupted()` следует учитывать,
что если мы обрабатываем в цикле исключение **InterruptedException** в блоке **catch**,
то при перехвате исключения статус потока автоматически сбрасывается, и после этого `isInterrupted()` будет возвращать **false**.

Добавим в цикл потока задержку с помощью метода `sleep()`

```java
public void run() {
    System.out.printf("%s started\n", Thread.currentThread().getName());
    int i = 1;
    while(!isInterrupted()) {
        System.out.println("i= " + i++);
        try {
            Thread.sleep(100);
        } catch(InterruptedException e) {
            System.out.println(getName() + " interrupted");
            System.out.println(isInterrupted());
            interrupt();
        }
    }
    System.out.printf("%s finished... \n", Thread.currentThread().getName());
}
```

Когда поток вызовет метод `interrupt()`, метод `sleep()` сгенерирует исключение **InterruptedException**, и управление перейдет к блоку **catch**.
Но если проверить статус потока, то увидим, что метод `isInterrupted()` возвращает **false**.
Как вариант, в этом случае мы можем повторно прервать текущий поток, опять же вызвав метод `interrupt()`.
Тогда при новой итерации цикла **while** метод `isInterrupted()` возвратит **true**, и поизойдет выход из цикла.

Либо можно сразу же в блоке **catch** выйти из цикла с помощью **break**

```java
while(!isInterrupted()) {
    System.out.println("i= " + i++);
    try {
        Thread.sleep(1000);
    } catch(InterruptedException e) {
        System.out.println(getName() + " interrupted");
        break;
    }
}
```

Если бесконечный цикл помещен в конструкцию `try...catch`, то достаточно обработать **InterruptedException**:

```java
public void run() {
    System.out.printf("%s started\n", Thread.currentThread().getName());
    int i = 1;
    try {
        while(!isInterrupted()){
            System.out.println("i= " + i++);
            Thread.sleep(1000);
        }
    } catch(InterruptedException e) {
        System.out.println(getName() + " interrupted");
    }
         
    System.out.printf("%s finished\n", Thread.currentThread().getName());
}
```

---

### [Назад к оглавлению](./README.md)