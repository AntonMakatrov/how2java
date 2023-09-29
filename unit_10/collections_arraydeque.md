# Очереди и класс ArrayDeque

В Java очереди представлены рядом классов.
Одни из них - класс ArrayDeque<E>. Этот класс представляют обобщенную двунаправленную очередь, наследуя функционал от класса AbstractCollection и применяя интерфейс Deque.

В классе ArrayDeque определены следующие конструкторы:

-   `ArrayDeque()` создает пустую очередь
-   `ArrayDeque(Collection<? extends E> col)` создает очередь, наполненную элементами из коллекции **col**
-   `ArrayDeque(int capacity)` создает очередь с начальной емкостью **capacity**.
    Если мы явно не указываем начальную емкость, то емкость по умолчанию будет равна `16`

Пример использования класса

```java
import java.util.ArrayDeque;
 
public class Program{
      
    public static void main(String[] args) {
          
        ArrayDeque<String> states = new ArrayDeque<>();
        // добавление элемента
        states.add("Germany");
        // добавление элемента в самое начало
        states.addFirst("France");
        // добавление элемента в самое начало
        states.push("Great Britain");
        // добавление элемента в конец коллекции
        states.addLast("Spain");
        // добавление элемента в конец коллекции
        states.add("Italy");
          
        // получение первого элемента без удаления
        String sFirst = states.getFirst();
        System.out.println(sFirst);
        // получение последнего элемента без удаления
        String sLast = states.getLast();
        System.out.println(sLast);
        
        System.out.printf("Queue size: %d \n", states.size());  // 5
         
        // перебор коллекции        
        while(states.peek() != null) {
            // извлечение c начала
            System.out.println(states.pop());
        }
          
        // очередь из объектов Person
        ArrayDeque<Person> people = new ArrayDeque<>();
        people.addFirst(new Person("Tom"));
        people.addLast(new Person("Nick"));

        // перебор без извлечения
        for(Person p : people) {
            System.out.println(p.getName());
        }
    }
}

class Person{
      
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