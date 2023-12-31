# Интерфейс Set и класс HashSet

Интерфейс `Set` расширяет интерфейс `Collection` и представляет набор уникальных элементов.
`Set` не добавляет новых методов, только вносит изменения унаследованные.
В частности, метод `add()` добавляет элемент в коллекцию и возвращает **true**, если в коллекции еще нет такого элемента.

Обобщенный класс `HashSet` представляет хеш-таблицу.
Он наследует свой функционал от класса `AbstractSet`, а также реализует интерфейс `Set`.

Хеш-таблица представляет такую структуру данных, в которой все объекты имеют уникальный ключ или хеш-код.
Данный ключ позволяет уникально идентифицировать объект в таблице.

Для создания объекта `HashSet` можно воспользоваться одним из следующих конструкторов:

-   `HashSet()` создает пустой список
-   `HashSet(Collection<? extends E> col)` создает хеш-таблицу, в которую добавляет все элементы коллекции **col**
-   `HashSet(int capacity)` параметр **capacity** указывает начальную емкость таблицы, которая по умолчанию равна **16**
-   `HashSet(int capacity, float koef)` параметр **koef** или коэффициент заполнения,
    значение которого должно быть в пределах от **0.0** до **1.0**, указывает,
    насколько должна быть заполнена емкость объектами прежде чем произойдет ее расширение.
    Например, коэффициент **0.75** указывает, что при заполнении емкости на **3/4** произойдет ее расширение.

Класс `HashSet` не добавляет новых методов, реализуя лишь те, что объявлены в родительских классах и применяемых интерфейсах


```java
import java.util.HashSet;
 
public class Program{
      
    public static void main(String[] args) {
          
        HashSet<String> states = new HashSet<>();
          
        // добавление элементов
        states.add("Germany");
        states.add("France");
        states.add("Italy");
        // попытка добавления элемента, который уже есть в коллекции
        boolean isAdded = states.add("Germany");
        System.out.println(isAdded);
        
        System.out.printf("Set contains %d elements \n", states.size());
          
        for(String state : states){
          
            System.out.println(state);
        }
        // удаление элемента
        states.remove("Germany");
          
        // хеш-таблица объектов Person
        HashSet<Person> people = new HashSet<>();
        people.add(new Person("Mike"));
        people.add(new Person("Tom"));
        people.add(new Person("Nick"));
        for(Person p : people) {
            System.out.println(p.getName());
        }
    }
}
class Person {
      
    private String name;

    public Person(String value) {
        name = value;
    }
    String getName() {
        return name;
    }
}
```

---

### [Назад к оглавлению](./README.md)