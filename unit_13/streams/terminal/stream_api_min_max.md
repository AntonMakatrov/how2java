# Операции сведения. Методы min и max

Методы `min()` и `max()` возвращают соответственно минимальное и максимальное значение.
Поскольку данные в потоке могут представлять различные типы, в том числе сложные классы,
то в качестве параметра в эти методы передается объект интерфейса Comparator,
который указывает, как сравнивать объекты:  
`Optional<T> min(Comparator<? super T> comparator)`  
`Optional<T> max(Comparator<? super T> comparator)`  

Оба метода возвращают элемент потока (минимальный или максимальный), обернутый в объект `Optional`.

Например, найдем минимальное и максимальное число в числовом потоке:

```java
import java.util.stream.Stream;
import java.util.Optional;
import java.util.ArrayList;
import java.util.Arrays;
public class Program {
 
    public static void main(String[] args) {
         
        ArrayList<Integer> numbers = new ArrayList<Integer>();
        numbers.addAll(Arrays.asList(new Integer[]{1, 2, 3, 4, 5, 6, 7, 8, 9}));
         
        Optional<Integer> min = numbers.stream()
                                        .min(Integer::compare);
        Optional<Integer> max = numbers.stream()
                                        .max(Integer::compare);
        System.out.println(min.get());
        System.out.println(max.get());
    } 
}
```

Интерфейс `Comparator` - это функциональный интерфейс, который определяет один метод _compare_,
принимающий два сравниваемых объекта и возвращающий число 
(если первый объект больше, возвращается положительное число, иначе возвращается отрицательное число).
Поэтому вместо конкретной реализации компаратора мы можем передать лямбда-выражение или метод,
который соответствует методу _compare_ интерфейса `Comparator`.
Поскольку сравниваются числа, то в метод передается в качестве компаратора статический метод `Integer.compare()`.

При этом методы `min` и `max` возвращают именно [Optional](../stream_api_optional.md),
и чтобы получить непосредственно результат операции из [Optional](../stream_api_optional.md), необходимо вызвать метод `get()`.

Рассмотрим более сложный случай, когда нам надо сравнивать более сложные объекты:

```java
import java.util.stream.Stream;
import java.util.Optional;
import java.util.ArrayList;
import java.util.Arrays;

class Phone {
      
    private String name;
    private int price;
      
    public Phone(String name, int price) {
        this.name = name;
        this.price = price;
    }

    public static int compare (Phone p1, Phone p2) {
        return p1.getPrice() > p2.getPrice() ? 1 : -1;
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
         
        ArrayList<Phone> phones = new ArrayList<Phone>();
        phones.addAll(Arrays.asList(new Phone[]{
            new Phone("iPhone", 8000), 
            new Phone("Nokia", 30000),
            new Phone("Samsung Galaxy", 48000),
            new Phone("HTC", 6000)
        }));
         
        Phone min = phones.stream().min(Phone::compare).get();
        Phone max = phones.stream().max(Phone::compare).get();
        System.out.printf("MIN Name: %s Price: %d \n", min.getName(), min.getPrice());
        System.out.printf("MAX Name: %s Price: %d \n", max.getName(), max.getPrice());
    } 
}

```

В данном случае мы находим минимальный и максимальный объект Phone (с максимальной и минимальной ценой).
Для определения функциональности сравнения в классе Phone реализован статический метод compare,
который соответствует сигнатуре метода compare интерфейса `Comparator`.
И в методах `min` и `max` применяем этот статический метод для сравнения объектов.

---

### [Назад к оглавлению](../../README.md)