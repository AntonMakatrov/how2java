# Методы skip и limit
   
Метод `skip(long n)` используется для пропуска `n` элементов.
Этот метод возвращает новый поток, в котором пропущены первые `n` элементов.

Метод `limit(long n)` применяется для выборки первых `n` элементов потоков.
Этот метод также возвращает модифицированный поток, в котором не более `n` элементов.

Зачастую эта пара методов используется вместе для создания эффекта постраничной навигации (pagination)

```java
Stream<String> phoneStream = Stream.of("iPhone", "Lumia", "Samsung Galaxy", "LG", "Nexus");
         
phoneStream.skip(1)
    .limit(2)
    .forEach(System.out::println);
```

В данном случае метод skip пропускает один первый элемент, а метод limit выбирает два следующих элемента.
В итоге мы получим следующий консольный вывод

```
Lumia
Samsung Galaxy
```

Вполне может быть, что метод `skip` может принимать в качестве параметра число большее, чем количество элементов в потоке.
В этом случае будут пропущены все элементы, а в результирующем потоке будет `0` элементов.

И если в метод `limit` передается число, большее, чем количество элементов, то просто выбираются все элементы потока.

Рассмотрим, как создать постраничную навигацию

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.stream.*;
import java.util.Scanner;
 
public class Program {
 
    public static void main(String[] args) {
         
        List<String> phones = new ArrayList<String>();
        phones.addAll(Arrays.asList(new String[]
                {"iPhone", "Lumia", "Huawei",
                "Samsung Galaxy", "LG G4", "Xiaomi MI",
                "ASUS Zenfone", "Sony Xperia", "Meizu",
                "Lenovo"}));
         
        int pageSize = 3; // количество элементов на страницу

        System.out.println("Введите номер страницы: ");
        Scanner scanner = new Scanner(System.in);

        int page = scanner.nextInt();
        
        phones.stream()
            .skip((page-1) * pageSize)
            .limit(pageSize)
            .forEach(System.out::println);
    }
}
```

В данном случае у нас набор из 10 элементов.
С помощью переменной pageSize определяем количество элементов на странице - 3.
То есть у нас получится 4 страницы (на последней будет только один элемент).

В потоке выбираем только те элементы, которые находятся на указанной странице.

---

### [Назад к оглавлению](../../README.md)