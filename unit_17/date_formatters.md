# Классы DateFormat, SimpleDateFormat

---

### Класс java.text.DateFormat

Класс `DateFormat` является абстрактным классом, с помощью которого можно форматировать и анализировать показания даты и времени.
Метод `getDateInstance()` возвращает экземпляр класса `DateFormat`, который может форматировать информацию о дате.

Чаще всего используется метод format(), позволяющий вывести дату в нужном формате.

---

### Класс java.text.SimpleDateFormat

Класс `SimpleDateFormat` является подклассом класса **DateFormat** и
позволяет определять собственные шаблоны форматирования для отображения даты и времени.

пример форматирования даты с использованием класса `SimpleDateFormat`:

```java
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class SimpleDateFormatExample {

    public static void main(String[] args) {
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy.MM.dd G 'at' HH:mm:ss z");
        System.out.println("date: " + dateFormat.format( new Date() ) );
    }
}
```

Если на компьютере локализацией по умолчанию является русская локализация,
то в результате выполнения приведенного кода Вы увидите следующее

```
date: 2012.02.07 н.э. at 15:13:08 EET
```

Рассмотрим некоторые методы класса `SimpleDateFormat`.
У класса есть 4 конструктора:


-   `SimpleDateFormat()` создает **SimpleDateFormat**,
    используя паттерн времени и формат символов по умолчанию для текущей локализации
-   `SimpleDateFormat(String pattern)` создает **SimpleDateFormat**,
    используя заданный паттерн времени и формат символов по умолчанию для текущей локализации
-   `SimpleDateFormat(String pattern, DateFormatSymbols formatSymbols)` создает **SimpleDateFormat**,
    используя заданные паттерн времени и формат символов
-   `SimpleDateFormat(String pattern, Locale locale)` создает **SimpleDateFormat**,
    используя заданный паттерн времени и формат символов по умолчанию для заданной локализации

Следующий пример демонстрирует работу всех четырех конструкторов:

```java
import java.text.DateFormatSymbols;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class SimpleDateFormatExample {

    public static void main(String[] args) {
        DateFormatSymbols myDateFormatSymbols = new DateFormatSymbols(){
            @Override
            public String[] getMonths() {
                return new String[]{"января", "февраля", "марта", "апреля", "мая", "июня",
                    "июля", "августа", "сентября", "октября", "ноября", "декабря"};
            }
        };

        Date currentDate = new Date();
        SimpleDateFormat dateFormat = null;
        
        dateFormat = new SimpleDateFormat();
        System.out.println("Constructor 1: " + dateFormat.format( currentDate ) );
        
        dateFormat = new SimpleDateFormat("dd MMMM");
        System.out.println("Constructor 2: " + dateFormat.format( currentDate ) );
        
        dateFormat = new SimpleDateFormat("dd MMMM", myDateFormatSymbols );
        System.out.println("Constructor 3: " + dateFormat.format( currentDate ) );
        
        dateFormat = new SimpleDateFormat("dd MMMM", Locale.ENGLISH);
        System.out.println("Constructor 4: " + dateFormat.format( currentDate ) );
    }
}
```

Результат:

```
Constructor 1: 09.05.19 16:44
Constructor 2: 09 Май
Constructor 3: 09 мая
Constructor 4: 09 May
```

Конструктор по умолчанию использует паттерн времени и формат символов по умолчанию для текущей локализации.
То есть, для русской локализации стандартным паттерном времени является паттерн `dd.MM.yy HH:mm`

Конструктор `SimpleDateFormat(String pattern)` принимает паттерн даты, в котором будет отдавать результат метод `format()`.
В примере мы использовали паттерн `dd MMMM`

Конструктор `SimpleDateFormat("dd MMMM", myDateFormatSymbols )` аналогичен предыдущему за исключением того,
что название месяца используется не по умолчанию, а те, которые возвращает переменная **myDateFormatSymbols**.
В свою очередь, в переменной **myDateFormatSymbols** переопределен метод **getMonths()**
чтобы он возвращал названия месяцев с прописной буквы и в родительном падеже.

Конструктор `SimpleDateFormat("dd MMMM", Locale.ENGLISH)` аналогичен конструктору `SimpleDateFormat(String pattern)`,
но использует заданную локализацию.
В нашем случае это английская локализация **Locale.ENGLISH**.


Символы форматирования принимаемые классом `SimpleDateFormat` в качестве паттерна даты:

| Символ | Описание | Пример
|--------|------------------------------------------|--------
| G	     | эра (в английской локализации - AD и BC)	| н.э.
| y	     | год (4-х значное число) | 2012
| yy	 | год (последние 2 цифры) | 12
| yyyy	 | год (4-х значное число) | 2012
| M	     | номер месяца без лидирующих нулей | 2
| MM	 | номер месяца (с лидирующими нулями если номер месяца < 10) | 02
| MMM	 | четырех буквенное сокращение месяца в русской локализации и трех буквенное - в английской (Feb) | фев
| MMMM	 | полное название месяца (в английской локализации - February) | Февраль
| w	     | неделя в году без лидирующих нулей | 7
| ww	 | неделя в году с лидирующими нулями | 07
| W	     | неделя в месяце без лидирующих нулей | 2
| WW	 | неделя в месяце с лидирующим нулем (если это необходимо) | 02
| D	     | день в году | 38
| d	     | день месяца без лидирующих нулей | 7
| dd	 | день месяца с лидирующими нулями | 07
| F	     | день недели в месяце без лидирующих нулей | 1
| FF	 | день недели в месяце с лидирующими нулями | 01
| E	     | день недели (сокращение) | Вт
| EEEE	 | день недели (полностью) | вторник
| a	     | AM/PM указатель | AM
| A	     | AM/PM указатель | AM
| H	     | часы в 24-часовом формате без лидирующих нулей | 6
| HH	 | часы в 24-часовом формате с лидирующим нулем | 06
| k	     | количество часов в 24-часовом формате | 18
| K	     | количество часов в 12-часовом формате |6
| h	     | время в 12-часовом формате без лидирующих нулей | 6
| hh	 | время в 12-часовом формате с лидирующим нулем | 06
| m	     | минуты без лидирующих нулей |32
| mm	 | минуты с лидирующим нулем | 32
| s	     | секунды без лидирующих нулей | 11
| ss	 | секунды с лидирующим нулем | 11
| S	     | миллисекунды | 109
| z	     | часовой пояс | EET
| Z	     | часовой пояс в формате RFC 822 | +0200
| '	     | символ экранирования для текста | 'Date='
| ''	 | кавычка | 'o''clock'

Рассмотрим несколько примеров паттернов даты и времени, которые представлены в официальной документации.
Русская локализация:


| Паттерн даты и времени         | Результат
|--------------------------------|----------
| "yyyy.MM.dd G 'at' HH:mm:ss z" | 2012.02.07 н.э. at 16:51:35 EET
| "EEE, MMM d, ''yy"             | Вт, фев 7, '12
| "h:mm a"                       | 4:51 PM
| "hh 'o''clock' a, zzzz"        | 04 o'clock PM, Eastern European Time
| "K:mm a, z"	                 | 4:51 PM, EET
| "yyyyy.MMMMM.dd GGG hh:mm aaa" | 02012.Февраль.07 н.э. 04:51 PM
| "EEE, d MMM yyyy HH:mm:ss Z"   | Вт, 7 фев 2012 16:51:35 +0200
| "yyMMddHHmmssZ"	             | 120207165135+0200

Английская локализация:

| Паттерн даты и времени         |	Результат
|--------------------------------|-------------------
| "yyyy.MM.dd G 'at' HH:mm:ss z" | 2012.02.07 AD at 16:55:57 EET
| "EEE, MMM d, ''yy"             | Tue, Feb 7, '12
| "h:mm a"                       | 4:55 PM
| "hh 'o''clock' a, zzzz"        | 04 o'clock PM, Eastern European Time
| "K:mm a, z"                    | 4:55 PM, EET
| "yyyyy.MMMMM.dd GGG hh:mm aaa" | 02012.February.07 AD 04:55 PM
| "EEE, d MMM yyyy HH:mm:ss Z"   | Tue, 7 Feb 2012 16:55:57 +0200
| "yyMMddHHmmssZ"                | 120207165557+0200

---

### [Назад к оглавлению](./README.md)