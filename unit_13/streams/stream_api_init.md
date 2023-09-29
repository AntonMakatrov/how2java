# Создание потока данных
   
Для создания потока данных можно применять различные методы.
В качестве источника потока мы можем использовать коллекции.
В JDK 8 в интерфейс Collection, который реализуется всеми классами коллекций, были добавлены два метода для работы с потоками:

-   `default Stream<E> stream` возвращается поток данных из коллекции
-   `default Stream<E> parallelStream` возвращается параллельный поток данных из коллекции

Рассмотрим пример с ArrayList

```java
import java.util.stream.Stream;
import java.util.*;

public class Program {
 
    public static void main(String[] args) {
        ArrayList<String> cities = new ArrayList<>();
        Collections.addAll(cities, "Moscow", "London", "Madrid", "Barcelona");
        cities.stream() // получаем поток
            .filter(s -> s.length() == 6) // применяем фильтр по длине строки
            .forEach(System.out::println); // выводим отфильтрованные строки на консоль
    }
}
```

Здесь с помощью вызова cities.stream() получаем поток, который использует данные из списка cities.
С помощью каждой промежуточной операции, которая применяется к потоку, мы также можем получить поток с учетом модификаций.
Например, мы можем изменить предыдущий пример следующим образом:

```java
import java.util.stream.Stream;
import java.util.*;

public class Program {
 
    public static void main(String[] args) {
        ArrayList<String> cities = new ArrayList<>();
        Collections.addAll(cities, "Moscow", "London", "Madrid", "Barcelona");
         
        Stream<String> citiesStream = cities.stream(); // получаем поток
        citiesStream = citiesStream.filter(s -> s.length() == 6); // применяем фильтр по длине строки
        citiesStream.forEach(System.out::println); // выводим отфильтрованные строки на консоль
    }
}
```

**Важно**! После использования терминальных операций другие терминальные или
промежуточные операции к этому же потоку не могут быть применены, поток уже употреблен.

Например, в следующем случае мы получим ошибку:

```java
citiesStream.forEach(s -> System.out.println(s)); // терминальная операция употребляет поток
System.out.println(citiesStream.count()); // здесь ошибка, так как поток уже употреблен
citiesStream = citiesStream.filter(s -> s.length() > 5); // тоже нельзя, так как поток уже употреблен
```

Фактически жизненный цикл потока проходит следующие три стадии:

-   Создание потока
-   Применение к потоку ряда промежуточных операций
-   Применение к потоку терминальной операции и получение результата

Кроме вышерассмотренных методов мы можем использовать еще ряд способов для создания потока данных.
Один из таких способов представляет метод Arrays.stream(T[] array), который создает поток данных из массива:

```java
Stream<String> citiesStream = Arrays.stream(new String[]{ "Moscow", "London", "Madrid", "Barcelona" }) ;
citiesStream.forEach(System.out::println); // выводим все элементы массива
```

Для создания потоков _IntStream_, _DoubleStream_, _LongStream_ можно использовать соответствующие перегруженные версии этого метода:

```java
IntStream intStream = Arrays.stream(new int[]{1,2,4,5,7});
intStream.forEach(System.out::println);
 
LongStream longStream = Arrays.stream(new long[]{100,250,400,5843787,237});
longStream.forEach(System.out::println);
 
DoubleStream doubleStream = Arrays.stream(new double[] {3.4, 6.7, 9.5, 8.2345, 121});
doubleStream.forEach(System.out::println);
```

И еще один способ создания потока представляет статический метод of(T..values) класса Stream:

```java
Stream<String> citiesStream =Stream.of("Moscow", "London", "Madrid", "Barcelona");
citiesStream.forEach(s->System.out.println(s));
 
// можно передать массив
String[] cities = { "Moscow", "London", "Madrid", "Barcelona" };
Stream<String> citiesStream2 =Stream.of(cities);
        
IntStream intStream = IntStream.of(1, 2, 4, 5, 7);
intStream.forEach(System.out::println);
 
LongStream longStream = LongStream.of(100, 250, 400, 5843787, 237);
longStream.forEach(l -> System.out.println(l));
 
DoubleStream doubleStream = DoubleStream.of(3.4, 6.7, 9.5, 8.2345, 121);
doubleStream.forEach(System.out::println);
```

---

### [Назад к оглавлению](../README.md)