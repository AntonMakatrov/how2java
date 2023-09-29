# Класс TreeMap

Класс `TreeMap<K, V>` представляет отображение в виде дерева.
Он наследуется от класса `AbstractMap` и реализует интерфейс `NavigableMap`, а следовательно, также и интерфейс `SortedMap`.
Поэтому в отличие от коллекции `HashMap` в `TreeMap` все объекты автоматически сортируются по возрастанию их ключей.

Класс `TreeMap` имеет следующие конструкторы:

-   `TreeMap()` создает пустое отображение в виде дерева
-   `TreeMap(Map<? extends K,​? extends V> map)` создает дерево, в которое добавляет все элементы из отображения **map**
-   `TreeMap(SortedMap<K, ? extends V> smap)` создает дерево, в которое добавляет все элементы из отображения **smap**
-   `TreeMap(Comparator<? super K> comparator)` создает пустое дерево,
    где все добавляемые элементы впоследствии будут отсортированы компаратором.

```java
import java.util.*;
 
public class Program{
      
    public static void main(String[] args) {
          
        TreeMap<Integer, String> states = new TreeMap<>();
        states.put(10, "Germany");
        states.put(2, "Spain");
        states.put(14, "France");
        states.put(3, "Italy");
         
        // получение объекта по ключу 2
        String first = states.get(2);
        // перебор элементов
        for(Map.Entry<Integer, String> item : states.entrySet()) {
            System.out.printf("Key: %d  Value: %s \n", item.getKey(), item.getValue());
        }
        // получение набора всех ключей
        Set<Integer> keys = states.keySet();
        // получение набора всех значений
        Collection<String> values = states.values();
         
        // получение всех объектов, которые стоят после объекта с ключом 4
        Map<Integer, String> afterMap = states.tailMap(4);
         
        // получение всех объектов, которые стоят до объекта с ключом 10
        Map<Integer, String> beforeMap = states.headMap(10);
         
        // получение последнего элемента дерева
        Map.Entry<Integer, String> lastItem = states.lastEntry();
         
        System.out.printf("Last item has key %d value %s \n", lastItem.getKey(), lastItem.getValue());
          
        Map<String, Person> people = new TreeMap<>();
        people.put("1240i54", new Person("Tom"));
        people.put("1564i55", new Person("Bill"));
        people.put("4540i56", new Person("Nick"));
         
        for(Map.Entry<String, Person> item : people.entrySet()) {
            System.out.printf("Key: %s  Value: %s \n", item.getKey(), item.getValue().getName());
        }
    }
}
class Person {
      
    private String name;
    public Person(String name) {
        this.name = name;
    }
    String getName() {
        return name;
    }
}
```

Кроме собственно методов интерфейса `Map` класс `TreeMap` реализует методы интерфейса `NavigableMap`.
Можно получить все объекты до или после определенного ключа с помощью методов `headMap()` и `tailMap()`.
Также мы можем получить первый и последний элементы и провести ряд дополнительных манипуляций с объектами.

---

### [Назад к оглавлению](./README.md)