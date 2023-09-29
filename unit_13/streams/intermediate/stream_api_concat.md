# Объединение потоков. Метод concat

Статический метод `concat()` объединяет элементы двух потоков, возвращая объединенный поток

```java
import java.util.stream.Stream;
 
public class Program {
  
    public static void main(String[] args) {
          
        Stream<String> people1 = Stream.of("Tom", "Bob", "Sam");
        Stream<String> people2 = Stream.of("Alice", "Kate", "Sam");
         
        Stream.concat(people1, people2)
            .forEach(System.out::println);
    }
}
```

---

### [Назад к оглавлению](../../README.md)