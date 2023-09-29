# Класс java.time.LocalTime

Класс `LocalTime` является неизменяемым и представляет собой время в читабельном виде.
По умолчанию он предоставляет формат **hh:mm:ss.zzz**.
Так же, как и `LocalDate`, этот класс обеспечивает поддержку часовых поясов и создание даты,
передавая в качестве аргументов часы, минуты и секунды.

Пример использования `LocalTime`:

```java
import java.time.LocalTime;

public class LocalTimeTest {
    public static void main(String[] args) {
 
        // Получение текущего времени
        LocalTime time = LocalTime.now();
        System.out.println("Получаем текущее время : " + time);
 
        //Создание LocalTime с использование своих данных
        LocalTime specificTime = LocalTime.of(16, 30, 50, 234782);
        System.out.println("Какое-то время дня : " + specificTime);
 
        //Получение даты через 666666 секунд после 01.01.1970
        LocalTime sec666666 = LocalTime.ofSecondOfDay(666666);
        System.out.println("Через 666666 секунд после 01.01.1970 : " + sec666666);
    }
}
```

---

### [Назад к оглавлению](./README.md)