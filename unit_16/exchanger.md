# Обмен между потоками. Класс Exchanger

Класс **Exchanger** предназначен для обмена данными между потоками.
Он является типизированным и типизируется типом данных, которыми потоки должны обмениваться.

Обмен данными производится с помощью единственного метода этого класса `exchange()`:

```java
V exchange(V x) throws InterruptedException
V exchange(V x, long timeout, TimeUnit unit) throws InterruptedException, TimeoutException
```

Параметр `x` представляет буфер данных для обмена.
Вторая форма метода также определяет параметр `timeout` - время ожидания и `unit` - тип временных единиц, применяемых для параметра `timeout`.

Пример использования класса Exchanger:

```java
import java.util.concurrent.Exchanger;
  
public class Program {
    public static void main(String[] args) {
        Exchanger<String> exchanger = new Exchanger<>();
        new Thread(new PutThread(exchanger)).start();
        new Thread(new GetThread(exchanger)).start();
    }
}
  
class PutThread implements Runnable {
    Exchanger<String> exchanger;
    String message;
    PutThread(Exchanger<String> exchanger) {
        this.exchanger = exchanger;
        message = "Hello best friend!";
    }

    public void run() {
        try {
            message=exchanger.exchange(message);
            System.out.println("PutThread received: " + message);
        } catch(InterruptedException ex) {
            System.out.println(ex.getMessage());
        }
    }
} 
class GetThread implements Runnable {
    Exchanger<String> exchanger;
    String message;
    GetThread(Exchanger<String> exchanger){
        this.exchanger = exchanger;
        message = "Hello friend!";
    }
    public void run() {
        try {
            message=exchanger.exchange(message);
            System.out.println("GetThread received: " + message);
        } catch(InterruptedException ex) {
            System.out.println(ex.getMessage());
        }
    }
} 
```

В классе **PutThread** отправляет в буфер сообщение `Hello best friend!`

```java
message=exchanger.exchange(message);
```

Причем в ответ метод `exchange()` возвращает данные, которые отправил в буфер другой поток.
То есть происходит обмен данными.
Хотя нам необязательно получать данные, мы можем просто их отправить

```java
exchanger.exchange(message);
```

Логика класса **GetThread** аналогична - также отправляется сообщение.

---

### [Назад к оглавлению](./README.md)

