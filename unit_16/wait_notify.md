# Методы wait и notify

Иногда при взаимодействии потоков встает вопрос о извещении одних потоков о действиях других.
Например, действия одного потока зависят от результата действий другого потока,
и надо как-то известить один поток, что второй поток произвел некую работу.
И для подобных ситуаций у класса Object определено ряд методов:

-   `wait()` освобождает монитор и переводит вызывающий поток в состояние ожидания до тех пор,
    пока другой поток не вызовет метод **notify()**
-   `notify()` продолжает работу потока, у которого ранее был вызван метод **wait()**
-   `notifyAll()` возобновляет работу всех потоков, у которых ранее был вызван метод **wait()**

Все эти методы вызываются только из синхронизированного контекста - синхронизированного блока или метода.

Рассмотрим, как мы можем использовать эти методы.
Возьмем стандартную задачу - **Производитель-Потребитель** `Producer-Consumer` -
пока производитель не произвел продукт,потребитель не может его купить.
Пусть производитель должен произвести **10** товаров, соответственно потребитель должен их все купить.
Но при этом одновременно на складе может находиться не более **3** товаров.
Для решения этой задачи задействуем методы `wait()` и `notify()`

```java
public class Program {
    public static void main(String[] args) {
        Store store=new Store();
        Producer producer = new Producer(store);
        Consumer consumer = new Consumer(store);
        new Thread(producer).start();
        new Thread(consumer).start();
    }
}

class Store {
    private int product = 0;
    public synchronized void get() {
        while (product < 1) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        product--;
        System.out.printf("Sold 1 item. %d items left in store.", product);
        notify();
    }

    public synchronized void put() {
        while (product >= 3) {
            try {
                wait();
            } catch (InterruptedException e) { 
                e.printStackTrace();
            } 
        }
        product++;
        System.out.printf("Added 1 item. %d items left in store.", product);
        notify();
    }
}

class Producer implements Runnable {
    Store store;
    Producer(Store store) {
       this.store = store; 
    }
    public void run() {
        for (int i = 1; i < 10; i++) {
            store.put();
        }
    }
}

class Consumer implements Runnable {
    Store store;
    Consumer(Store store) {
       this.store = store; 
    }
    public void run() {
        for (int i = 1; i < 10; i++) {
            store.get();
        }
    }
}
```

Итак, здесь определен класс магазина, потребителя и покупателя.
Производитель в методе `run()` добавляет в объект **Store** с помощью его метода `put()` 10 товаров.
Потребитель в методе `run()` в цикле обращается к методу `get()` объекта **Store** для получения этих товаров.
Оба метода **Store** - `put()` и `get()` являются синхронизированными.

Для отслеживания наличия товаров в классе **Store** проверяем значение переменной **product**.
По умолчанию товара нет, поэтому переменная равна **0**.
Метод `get()` - получение товара должен срабатывать только при наличии хотя бы одного товара.
Поэтому в методе get проверяем, отсутствует ли товар `while (product < 1)`

Если товар отсутсвует, вызывается метод `wait()`.
Этот метод освобождает монитор объекта **Store** и блокирует выполнение метода `get()`,
пока для этого же монитора не будет вызван метод `notify()`.

Когда в методе `put()` добавляется товар и вызывается `notify()`,
то метод `get()` получает монитор и выходит из конструкции `while (product < 1)`, так как товар добавлен.
Затем имитируется получение покупателем товара. 
Для этого выводится сообщение, и уменьшается значение **product** `product--`.
И в конце вызов метода `notify()` дает сигнал методу `put()` продолжить работу.

В методе `put()` работает похожая логика, только теперь метод `put()` должен срабатывать,
если в магазине не более трех товаров.
Поэтому в цикле проверяется наличие товара, и если товар уже есть,
то освобождаем монитор с помощью `wait()` и ждем вызова `notify()` в методе `get()`.

Таким образом, с помощью `wait()` в методе `get()` мы ожидаем, когда производитель добавит новый продукт.
А после добавления вызываем `notify()`, как бы говоря, что магазин теперь снова пуст, и можно еще добавлять.

А в методе `put()` с помощью `wait()` мы ожидаем освобождения места на складе.
После того, как место освободится, добавляем товар и через `notify()` уведомляем покупателя о том, что он может забирать товар.

---

### [Назад к оглавлению](./README.md)