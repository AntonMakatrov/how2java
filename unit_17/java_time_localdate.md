# Класс java.time.LocalDate

`java.time.LocalDate `— неизменяемый класс, который представляет объекты Date в формате по умолчанию **yyyy-MM-dd** (ISO формат без времени).
Он может быть использован для хранения дат, таких как дни рождения и зарплаты.
Мы можем использовать метод `now()`, чтобы получить текущую дату.
Мы также можем предоставить в качестве аргументов год, месяц и день, чтобы создать экземпляр **LocalDate**.
Этот класс предоставляет перегруженный метод `now()`,
которому мы можем предоставить **ZoneId** для получения даты в конкретном часовом поясе.
Этот класс предоставляет такую же функциональность как `java.sql.Date`.

Пример использования `LocalDate`:

```java
import java.time.LocalDate;
import java.time.Month;
 
public class LocalDateTest {
    public static void main(String[] args) {

        // текущая дата
        LocalDate today = LocalDate.now();
        System.out.println("Текущая дата : " + today);
 
        //Создание LocalDate с указанием года месяца и дня
        LocalDate specificDate = LocalDate.of(2017, Month.NOVEMBER, 30);
        System.out.println("Дата с указанием года, месяца и дня : " + specificDate);
 
 
        //Указание даты с ошибкой
        //получим исключение java.time.DateTimeException:
        //Invalid value for DayOfMonth (valid values 1 - 28/31): 33
        LocalDate invDate = LocalDate.of(2014, Month.JULY, 33);
 
        //Получение даты через 2360 дней с 01.01.1970
        LocalDate dateFromBase = LocalDate.ofEpochDay(2360);
        System.out.println("Дата с начала отсчета времени : " + dateFromBase);
 
        LocalDate day140_2019 = LocalDate.ofYearDay(2019, 140);
        System.out.println("140 день 2019 : " + day140_2019);
    }
}
```

---

### [Назад к оглавлению](./README.md)