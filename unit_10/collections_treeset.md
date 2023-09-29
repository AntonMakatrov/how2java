# TreeSet

Обобщенный класс **TreeSet<E>** представляет структуру данных в виде дерева,
в котором все объекты хранятся в отсортированном виде по возрастанию.
_TreeSet_ является наследником класса `AbstractSet` и реализует интерфейс `NavigableSet`, а следовательно, и интерфейс `SortedSet`.

В классе TreeSet определены следующие конструкторы:

-   `TreeSet()` создает пустое дерево
-   `TreeSet(Collection<? extends E> col)` создает дерево, в которое добавляет все элементы коллекции **col**
-   `TreeSet(SortedSet <E> set)` создает дерево, в которое добавляет все элементы сортированного набора **set**
-   `TreeSet(Comparator<? super E> comparator)` создает пустое дерево,
    где все добавляемые элементы впоследствии будут отсортированы компаратором.

`TreeSet` поддерживает все стандартные методы для вставки и удаления элементов

```java
import java.util.TreeSet;
 
public class Program {
      
    public static void main(String[] args) {
          
        TreeSet<String> states = new TreeSet<>();
          
        // добавление элементов
        states.add("Germany");
        states.add("France");
        states.add("Italy");
        states.add("Great Britain");
        
        System.out.printf("TreeSet contains %d elements \n", states.size());
         
        // удаление элемента
        states.remove("Germany");
        for(String state : states) {
            System.out.println(state);
        }
    }
}
```

Так как `TreeSet` реализует интерфейс `NavigableSet`, а через него и `SortedSet`, то мы можем применить к структуре дерева различные методы:

```java
import java.util.*;
 
public class Program {
      
    public static void main(String[] args) {
          
        TreeSet<String> states = new TreeSet<>();
          
        // добавление элементов
        states.add("Germany");
        states.add("France");
        states.add("Italy");
        states.add("Spain");
        states.add("Great Britain");
        
        // получение первого элемента (самого меньшего)
        System.out.println(states.first());
        // получение последнего элемента (самого большого)
        System.out.println(states.last());
        // получение поднабора от одного элемента до другого
        SortedSet<String> set = states.subSet("Germany", "Italy");
        System.out.println(set);
        // элемент из набора, который больше текущего
        String greater = states.higher("Germany");
        // элемент из набора, который меньше текущего
        String lower = states.lower("Germany");
        // возвращение набора в обратном порядке
        NavigableSet<String> navSet = states.descendingSet();
        // возвращение набора, в котором все элементы меньше текущего
        SortedSet<String> setLower=states.headSet("Germany");
        // возвращение набора, в котором все элементы больше текущего
        SortedSet<String> setGreater=states.tailSet("Germany");  
        System.out.println(navSet);
        System.out.println(setLower);
        System.out.println(setGreater);
    }
}
```

---

### [Назад к оглавлению](./README.md)