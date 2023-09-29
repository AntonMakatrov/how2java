# Использование вспомогательных методов Date Time API

Как упоминалось ранее, работу большинства классов с датой и временем в Java 8 обеспечивают различные вспомогательные методы:
прибавить или отнять несколько дней, недель, месяцев и т.д.
Есть и другие методы для управления датой с помощью `TemporalAdjuster` и расчета разницы между двумя датами.

Пример использования вспомогательных методов в Java 8 Date API:

```java
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.Period;
import java.time.temporal.TemporalAdjusters;
 
public class DateAPITest {
    public static void main(String[] args) {
 
        LocalDate today = LocalDate.now();
 
        // получение года и проверка на високосность
        System.out.println("Год " + today.getYear() + " - високосный? : " + today.isLeapYear());
 
        // сравнение двух LocalDate: до и после
        System.out.println("Сегодня — это до 02.03.2017? : " + today.isBefore(LocalDate.of(2017,3,2)));
 
        // создание LocalDateTime с LocalDate
        System.out.println("Текущее время : " + today.atTime(LocalTime.now()));
 
        // операции + и - с датами
        System.out.println("9 дней после сегодняшнего дня будет: " + today.plusDays(9));
        System.out.println("3 недели после сегодняшнего дня будет: " + today.plusWeeks(3));
        System.out.println("20 месяцев после сегодняшнего дня будет: " + today.plusMonths(20));
 
        System.out.println("9 дней до сегодняшнего дня будет: " + today.minusDays(9));
        System.out.println("3 недели до сегодняшнего дня будет: " + today.minusWeeks(3));
        System.out.println("20 месяцев до сегодняшнего дня будет: " + today.minusMonths(20));
 
        Period period = today.until(lastDayOfYear);
        System.out.println("Находим время между жвумя датами : "+period);
        System.out.println("В этом году осталось " + period.getMonths() + " месяц(ев)");

        System.out.println("Первый день этого месяца : " + today.with(TemporalAdjusters.firstDayOfMonth()));
        LocalDate lastDayOfYear = today.with(TemporalAdjusters.lastDayOfYear());
        System.out.println("Последний день этой года : " + lastDayOfYear);
    }
}
```

Пример парсинга и форматирования даты:

```java
import java.time.Instant;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
 
public class DateParseFormatTest {
    public static void main(String[] args) {
 
        LocalDate date = LocalDate.now();
        // стандартный формат даты
        System.out.println("стандартный формат даты для LocalDate : " + date);
        // применение своего формата даты
        System.out.println(date.format(DateTimeFormatter.ofPattern("d::MMM::uuuu")));
        System.out.println(date.format(DateTimeFormatter.BASIC_ISO_DATE));
        
        LocalDateTime dateTime = LocalDateTime.now();
        // стандартный формат даты
        System.out.println("стандартный формат даты LocalDateTime : " + dateTime);
        // применение своего формата даты
        System.out.println(dateTime.format(DateTimeFormatter.ofPattern("d::MMM::uuuu HH::mm::ss")));
        System.out.println(dateTime.format(DateTimeFormatter.BASIC_ISO_DATE));
 
        Instant timestamp = Instant.now();
        // стандартный формат даты
        System.out.println("стандартный формат : " + timestamp);
    }
}
```

---

### [Назад к оглавлению](./README.md)