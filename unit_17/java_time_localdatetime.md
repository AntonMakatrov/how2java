# Класс java.time.LocalDateTime

Класс `java.time.LocalDateTime` — представляет собой дату и время в формате по умолчанию: **yyyy-MM-dd-HH-mm-ss.zzz**.
Чтобы создать экземпляр `LocalDateTime` есть метод, который принимает **LocalDate** и **LocalTime** в качестве входных аргументов.

Пример использования `LocalDateTime`:

```java
import java.time.*;
 
public class LocalDateTimeTest {
    public static void main(String[] args) {
 
        // получение текущего времени
        LocalDateTime today = LocalDateTime.now();
        System.out.println("Получаем текущее время : " + today);
 
        // создание новой даты с помощью LocalDate и LocalTime
        today = LocalDateTime.of(LocalDate.now(), LocalTime.now());
        System.out.println("DateTime : " + today);
 
        // создание LocalDateTime с параметрами: год, месяц, день, час, минута, секунда
        LocalDateTime randDate = LocalDateTime.of(2017, Month.JULY, 9, 11, 6, 22);
        System.out.println("LocalDateTime с указанной датой : " + randDate);
 
        // получение даты через 782000 секунд после 01.01.1970
        LocalDateTime dateFromBase = LocalDateTime.ofEpochSecond(782000, 0, ZoneOffset.UTC);
        System.out.println("Через 2000 секунд после 01.01.1970 : " + dateFromBase);
    }
}
```

---

### [Назад к оглавлению](./README.md)