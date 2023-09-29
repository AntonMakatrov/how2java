# Метод collect
   
Большинство операций класса Stream, которые модифицируют набор данных, возвращают этот набор в виде потока.
Однако бывают ситуации, когда хотелось бы получить данные не в виде потока,
а в виде обычной коллекции, например, _ArrayList_ или _HashSet_.
И для этого у класса Stream определен метод `collect`.
Первая версия метода принимает в качестве параметра функцию преобразования к коллекции

`<R,A> R collect(Collector<? super T,A,R> collector)`

Параметр `R` представляет тип результата метода, параметр `Т` - тип элемента в потоке,
а параметр `А` - тип промежуточных накапливаемых данных.
В итоге параметр `collector` представляет функцию преобразования потока в коллекцию.

Эта функция представляет объект `Collector`, который определен в пакете java.util.stream.
Мы можем написать свою реализацию функции, однако Java уже предоставляет ряд встроенных функций, определенных в классе `Collectors`:

-   `toList()` преобразование к типу _List_
-   `toSet()` преобразование к типу _Set_
-   `toMap()` преобразование к типу _Map_

Преобразуем набор в потоке в список:

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;
 
public class Program {
 
    public static void main(String[] args) {
         
        List<String> phones = new ArrayList<String>();
        Collections.addAll(phones, "iPhone", "Lumia", "Huawei", "Samsung Galaxy", "LG G4",
                                "Xiaomi MI", "ASUS Zenfone", "Sony Xperia", "Meizu", "Lenovo");
          
        List<String> filteredPhones = phones.stream()
                .filter(s -> s.length() < 10)
                .collect(Collectors.toList());
                 
        for(String s : filteredPhones) {
            System.out.println(s);
        }
    } 
}
```

Использование метода `toSet()` аналогично.

```java
Set<String> filteredPhones = phones.stream()
                .filter(s -> s.length() < 10)
                .collect(Collectors.toSet());
```

Для применения метода `toMap()` надо задать ключ и значение

```java
import java.util.Map;
import java.util.stream.Collectors;
import java.util.stream.Stream;

class Phone{
      
    private String name;
    private int price;
      
    public Phone(String name, int price) {
        this.name = name;
        this.price = price;
    }
      
    public String getName() {
        return name; 
    }
    
    public int getPrice() {
        return price;
    }
}

public class Program {
 
    public static void main(String[] args) {
         
        Stream<Phone> phoneStream = Stream.of(new Phone("iPhone", 56000), 
            new Phone("Nokia", 12000),
            new Phone("Samsung", 40000),
            new Phone("LG", 22000));
          
          
        Map<String, Integer> phones = phoneStream
            .collect(Collectors.toMap(Phone::getName, Phone::getPrice));
      
        phones.forEach((k,v) -> System.out.println(k + " " + v));
    } 
}

```

Лямбда-выражение `Phone::getName` (аналогично `p -> p.getName()`) получает значение для ключа элемента,
а `Phone::getPrice` (аналогично `t -> t.getPrice()`) - извлекает значение элемента.

Если нам надо создать какой-то определенный тип коллекции, например, HashSet,
то мы можем использовать специальные функции, которые определены в классах-коллекций

```java
import java.util.HashSet;
import java.util.stream.Collectors;
import java.util.stream.Stream;
 
public class Program {
 
    public static void main(String[] args) {
         
        Stream<String> phones = Stream.of("iPhone", "Lumia", "Huawei", "Samsung Galaxy", "LG G4",
                                        "Xiaomi MI", "ASUS Zenfone", "Sony Xperia", "Meizu", "Lenovo");
          
        HashSet<String> filteredPhones = phones.filter(s->s.length()<12).
                                    collect(Collectors.toCollection(HashSet::new));
         
        filteredPhones.forEach(System.out::println);
    } 
}
```

Выражение `HashSet::new` представляет функцию создания коллекции.
Аналогичным образом можно получать другие коллекции, например, ArrayList

`ArrayList<String> result = phones.collect(Collectors.toCollection(ArrayList::new));`

Вторая форма метода collect имеет три параметра:

`<R> R collect(Supplier<R> supplier, BiConsumer<R,? super T> accumulator, BiConsumer<R,R> combiner)`

-   `supplier` создает объект коллекции
-   `accumulator` добавляет элемент в коллекцию
-   `combiner` бинарная функция, которая объединяет два объекта

```java
import java.util.ArrayList;
import java.util.stream.Collectors;
import java.util.stream.Stream;
 
public class Program {
 
    public static void main(String[] args) {
         
        Stream<String> phones = Stream.of("iPhone", "Lumia", "Huawei", "Samsung Galaxy", "LG G4",
                                        "Xiaomi MI", "ASUS Zenfone", "Sony Xperia", "Meizu", "Lenovo");
   
        ArrayList<String> filteredPhones = phones.filter(s -> s.length() < 6)
            .collect(()-> new ArrayList<>(), // создаем ArrayList
                (list, item) -> list.add(item), // добавляем в список элемент
                (list1, list2) -> list1.addAll(list2)); // добавляем в список другой список
          
        filteredPhones.forEach(System.out::println);
    } 
}
```

Тот же самый пример с использование указателей

```java
import java.util.ArrayList;
import java.util.stream.Collectors;
import java.util.stream.Stream;
 
public class Program {
 
    public static void main(String[] args) {
         
        Stream<String> phones = Stream.of("iPhone", "Lumia", "Huawei", "Samsung Galaxy", "LG G4",
                                        "Xiaomi MI", "ASUS Zenfone", "Sony Xperia", "Meizu", "Lenovo");
   
        ArrayList<String> filteredPhones = phones.filter(s -> s.length() < 6)
            .collect(ArrayList::new, // создаем ArrayList
               ArrayList::add, // добавляем в список элемент
                ArrayList::addAll); // добавляем в список другой список
          
        filteredPhones.forEach(System.out::println);
    } 
}
```

---

### [Назад к оглавлению](../../README.md)