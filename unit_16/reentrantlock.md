# Блокировки. ReentrantLock

Для управления доступом к общему ресурсу в качестве альтернативы оператору **synchronized** мы можем использовать блокировки.
Функциональность блокировок заключена в пакете `java.util.concurrent.locks`.

Вначале поток пытается получить доступ к общему ресурсу.
Если он свободен, то на него накладывает блокировку.
После завершения работы блокировка с общего ресурса снимается.
Если же ресурс не свободен и на него уже наложена блокировка, то поток ожидает, пока эта блокировка не будет снята.

Классы блокировок реализуют интерфейс **Lock**, который определяет следующие методы:

-   `void lock()` ожидает, пока не будет получена блокировка
-   `void lockInterruptibly() throws InterruptedException` ожидает, пока не будет получена блокировка, если поток не прерван
-   `boolean tryLock()` пытается получить блокировку, если блокировка получена, то возвращает **true**.
    Если блокировка не получена, то возвращает **false**.
    В отличие от метода `lock()` не ожидает получения блокировки, если она недоступна
-   `void unlock()` снимает блокировку
-   `Condition newCondition()` возвращает объект **Condition**, который связан с текущей блокировкой

Организация блокировки в общем случае довольно проста:
для получения блокировки вызывается метод `lock()`,
а после окончания работы с общими ресурсами вызывается метод `unlock()`, который снимает блокировку.

Объект **Condition** позволяет управлять блокировкой.

Пример использования класса **ReentrantLock**

```java
import java.util.concurrent.locks.ReentrantLock;
 
public class Program {
    public static void main(String[] args) {   
        ClassA classA = new ClassA();
        ReentrantLock lock = new ReentrantLock();
        for (int i = 1; i < 10; i++) {
            Thread t = new Thread(new ThreadCounter(classA, lock));
            t.setName("ThreadCounter " + i);
            t.start();
        }
    }
}
class ClassA {
    int x = 0;
}  
class ThreadCounter implements Runnable {
    ClassA a;
    ReentrantLock lock;
    ThreadCounter(ClassA a, ReentrantLock lock){
        this.a = a;
        this.lock = lock;
    }
    public void run() {
        lock.lock();
        try {
            a.x = 1;
            for (int i = 1; i < 3; i++) {
                System.out.printf("%s - %d \n", Thread.currentThread().getName(), a.x);
                a.x++;
                Thread.sleep(1000);
            }
        } catch(InterruptedException e) {
            System.out.println(e.getMessage());
        } finally {
            locker.unlock();
        }
    }
}
```

Здесь также используется общий ресурс ClassA, для управления которым создается 10 потоков.
На входе в блок устанавливается заглушка `locker.lock()`

После этого только один поток имеет доступ к критической секции, а остальные потоки ожидают снятия блокировки.
В блоке **finally** после всей окончания основной работы потока эта блокировка снимается.
Причем делается это обязательно в блоке **finally**,
так как в случае возникновения ошибки все остальные потоки окажутся заблокированными.

---

### [Назад к оглавлению](./README.md)