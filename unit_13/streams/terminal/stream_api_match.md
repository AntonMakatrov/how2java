# Операции сведения. Методы allMatch, anyMatch и noneMatch

Еще одна группа операций сведения возвращает логическое значение **true** или **false**:

-   `boolean allMatch(Predicate<? super T> predicate)` возвращает **true**,
    если все элементы потока удовлетворяют условию в предикате
-   `boolean anyMatch(Predicate<? super T> predicate)` возвращает **true**,
    если хоть один элемент потока удовлетворяют условию в предикате
-   `boolean noneMatch(Predicate<? super T> predicate)` возвращает **true**,
    если ни один из элементов в потоке не удовлетворяет условию в предикате

Пример использования

```java
import java.util.stream.Stream;
import java.util.Optional;
import java.util.ArrayList;
import java.util.Arrays;
public class Program {
 
    public static void main(String[] args) {
         
        ArrayList<String> names = new ArrayList<String>();
        names.addAll(Arrays.asList(new String[]{"Tom", "Sam", "Bob", "Alice"}));
         
        // есть ли в потоке строка, длина которой больше 3
        boolean any = names.stream().anyMatch(s -> s.length() > 3);
        System.out.println(any);    // true
         
        // все ли строки имеют длину в 3 символа
        boolean all = names.stream().allMatch(s -> s.length() == 3);
        System.out.println(all);    // false
         
        // НЕТ ЛИ в потоке строки "Bill". Если нет, то true, если есть, то false
        boolean none = names.stream().noneMatch("Bill"::equals);
        System.out.println(none);   // true
    } 
}
```

---

### [Назад к оглавлению](../../README.md)