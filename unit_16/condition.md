# Условия в блокировках

Применение условий в блокировках позволяет добиться контроля над управлением доступом к потокам.
Условие блокировки представлет собой объект интерфейса **Condition** из пакета `java.util.concurrent.locks`.

Применение объектов **Condition** во многом аналогично использованию методов **wait/notify/notifyAll** класса **Object**,
которые были рассмотрены в одной из прошлых тем.
В частности, мы можем использовать следующие методы интерфейса **Condition**:

-   `await` поток ожидает, пока не будет выполнено некоторое условие и пока другой поток не вызовет методы **signal/signalAll**.
    Во многом аналогичен методу `wait()` класса **Object**
-   `signal` сигнализирует, что поток, у которого ранее был вызван метод `await()`, может продолжить работу.
    Применение аналогично использованию методу `notify()` класса **Object**
-   `signalAll` сигнализирует всем потокам, у которых ранее был вызван метод `await()`, что они могут продолжить работу.
    Аналогичен методу `notifyAll()` класса Object

Эти методы вызываются из блока кода, который попадает под действие блокировки **ReentrantLock**.
Сначала, используя эту блокировку, нам надо получить объект **Condition**   

```java
ReentrantLock locker = new ReentrantLock();
Condition condition = locker.newCondition();
```

Как правило, сначала проверяется условие доступа.
Если соблюдается условие, то поток ожидает, пока условие не изменится

```java
while (условие) {
    condition.await();
}
```

После выполнения всех действий другим потокам подается сигнал об изменении условия

```java
condition.signalAll();
```

Важно в конце вызвать метод **signal/signalAll**, чтобы избежать возможности взаимоблокировки потоков.

 В то же время покупатель не может купить товар, если на складе нет никаких товаров:

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.Condition;
 
public class Program {
    public static void main(String[] args) {
        Store store = new Store();
        Producer producer = new Producer(store);
        Consumer consumer = new Consumer(store);
        new Thread(producer).start();
        new Thread(consumer).start();
    }
}
class Store {
    private int productCount = 0;
    ReentrantLock lock;
    Condition condition;
    Store() {
        lock = new ReentrantLock();
        condition = locker.newCondition();
    }
    public void get() {
        locker.lock();
        try {
            while (product < 1) {
                condition.await();
            }
            productCount--;
            System.out.println("1 product sold. " + productCount + " left in store.");

            condition.signalAll();
        } catch (InterruptedException e) {
            System.out.println(e.getMessage());
        } finally {
            lock.unlock();
        }
    }
    public void put() {
        lock.lock();
        try {
            while (product >= 3) {
                condition.await();
            }
            product++;
            System.out.println("1 product add. " + productCount + " left in store.");

            condition.signalAll();
        } catch (InterruptedException e) {
          System.out.println(e.getMessage());
        } finally {
            locker.unlock();
        }
    }
}
class Producer implements Runnable {
    Store store;
    Producer(Store store){
       this.store = store; 
    }
    public void run() {
        for (int i = 1; i < 6; i++) {
            store.put();
        }
    }
}
class Consumer implements Runnable{
    Store store;
    Consumer(Store store) {
       this.store = store; 
    }
    public void run() {
        for (int i = 1; i < 6; i++) {
            store.get();
        }
    }
}
```

---

### [Назад к оглавлению](./README.md)