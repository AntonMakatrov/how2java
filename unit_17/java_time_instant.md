# Класс java.time.Instant

Класс `java.time.Instant` используется для работы с машиночитаемым форматом времени —
он сохраняет дату и время в так называемый «**unix timestamp** (отметку времени)». 

Пример использования `Instant`:

```java
import java.time.Duration;
import java.time.Instant;
 
public class InstantTest {
    public static void main(String[] args) {

        //Текущая отметка времени
        Instant timestamp = Instant.now();
        System.out.println("Текущая отметка времени : "+timestamp);
 
        //Instant для timestamp
        Instant specificTime = Instant.ofEpochMilli(timestamp.toEpochMilli());
        System.out.println("Instant для timestamp : " + specificTime);
 
        //Пример использования Duration
        Duration sixtyDay = Duration.ofDays(60);
        System.out.println(sixtyDay);
    }
}
```

В Java 8 добавлен метод `toInstant()`, который помогает преобразовать существующие экземпляры **Date**
и **Calendar** в новый API времени и даты, как в следующем фрагменте кода:

```java
LocalDateTime.ofInstant(date.toInstant(), ZoneId.systemDefault());
LocalDateTime.ofInstant(calendar.toInstant(), ZoneId.systemDefault());
```

**LocalDateTime** может быть создан из секунд эпохи, как показано ниже.
Результатом кода ниже будет **LocalDateTime** , представляющий `2049-12-18T19:11:14`

```java
LocalDateTime.ofEpochSecond(2523467474, 0, ZoneOffset.UTC)
```

---

### [Назад к оглавлению](./README.md)