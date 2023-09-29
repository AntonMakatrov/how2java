# Операции сведения. Метод count

Операции сведения представляют терминальные операции, которые возвращают некоторое значение - результат операции.
В Stream API есть ряд операций сведения.

---

### count

Метод `count()` возвращает количество элементов в потоке данных

```java
import java.util.stream.Stream;
import java.util.Optional;
import java.util.*;
public class Program {
 
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>();
        names.addAll(Arrays.asList(new String[]{"Tom", "Sam", "Bob", "Alice"}));

        System.out.println(names.stream()
                                .count());
         
        // количество элементов с длиной не больше 3 символов
        System.out.println(names.stream()
                                .filter(n -> n.length() <= 3)
                                .count());
    } 
}
```

---

### [Назад к оглавлению](../../README.md)