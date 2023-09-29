# Сортировка. Метод sorted

Коллекции, на основе которых нередко создаются потоки, уже имеют специальные методы для сортировки содержимого.
Однако класс _Stream_ также включает возможность сортировки.
Такую сортировку мы можем задействовать, когда у нас идет набор промежуточных операций с потоком,
которые создают новые наборы данных, и нам надо эти наборы отсортировать.

Для простой сортировки по возрастанию применяется метод `sorted()`

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
 
public class Program {
  
    public static void main(String[] args) {
          
        List<String> phones = new ArrayList<>();
        Collections.addAll(phones, "iPhone", "Nokia", "Huawei",
                "Samsung Galaxy", "LG", "Xiaomi",
                "ASUS", "Sony Xperia", "Meizu", "Google Pixel");
          
        phones.stream()
                .filter(p -> p.length() < 12)
                .sorted() // сортировка по возрастанию
                .forEach(System.out::println);
    } 
}
```

Однако данный метод не всегда подходит.
Уже по консольному выводу мы видим, что метод сортирует объекты по возрастанию,
но при этом заглавные и строчные буквы рассматриваются отдельно.

Кроме того, данный метод подходит только для сортировки тех объектов, которые реализуют интерфейс Comparable.

Если же у нас классы объектов не реализуют этот интерфейс или мы хотим создать какую-то свою логику сортировки,
то мы можем использовать другую версию метода `sorted()`, которая в качестве параметра принимает компаратор.

Например, пусть у нас есть класс Phone.
Отсортируем поток обектов Phone

```java
import java.util.Comparator;
import java.util.stream.Stream;

class Phone{
     
    private String name;
    private String company;
    private int price;
     
    public Phone(String name, String comp, int price) {
        this.name=name;
        this.company=comp;
        this.price = price;
    }
     
    public String getName() { return name; }
    public int getPrice() { return price; }
    public String getCompany() { return company; }
}

class PhoneComparator implements Comparator<Phone> {
  
    public int compare(Phone a, Phone b){
      
        return a.getName().toUpperCase().compareTo(b.getName().toUpperCase());
    }
}

public class Program {
 
    public static void main(String[] args) {
 
        Stream<Phone> phoneStream = Stream.of(new Phone("iPhone X", "Apple", 600), 
            new Phone("Pixel 2", "Google", 500),
            new Phone("iPhone 8", "Apple",450),
            new Phone("Nokia 9", "HMD Global",150),
            new Phone("Galaxy S9", "Samsung", 300));
         
        phoneStream
            .sorted(new PhoneComparator())
            .forEach(p -> System.out.printf("%s (%s) - %d \n", p.getName(), p.getCompany(), p.getPrice()));
    } 
}
```

Здесь определен класс компаратора PhoneComparator, который сортирует объекты по полю name

Метод `sorted(new PhoneComparator())` аналогичен следующим вариантам:
-   `sorted((a , b) -> a.getName().toUpperCase().compareTo(b.getName().toUpperCase()))`
-   `sorted(a -> a.getName().toUpperCase())`
-   `sorted(Comparator.comparing(a -> a.getName().toUpperCase()))`

---

### [Назад к оглавлению](../../README.md)