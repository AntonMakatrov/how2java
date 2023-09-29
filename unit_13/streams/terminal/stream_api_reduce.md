# Метод reduce
   
Метод `reduce` выполняет терминальные операции сведения, возвращая некоторое значение - результат операции.
Он имеет следующие формы:

-   `Optional<T> reduce(BinaryOperator<T> accumulator)`
-   `T reduce(T identity, BinaryOperator<T> accumulator)`
-   `U reduce(U identity, BiFunction<U,? super T,U> accumulator, BinaryOperator<U> combiner)`

Первая форма возвращает результат в виде объекта `Optional<T>`.
Вычислим произведение набора чисел:

```java
import java.util.stream.Stream;
import java.util.Optional;
 
public class Program {
 
    public static void main(String[] args) {
         
         
        Stream<Integer> numbersStream = Stream.of(1,2,3,4,5,6);
        Optional<Integer> result = numbersStream.reduce((x,y) -> x * y);
        System.out.println(result.get());
    } 
}
```

Объект `BinaryOperator<T>` представляет функцию,которая принимает два элемента и
выполняет над ними некоторую операцию,возвращая результат.
При этом метод reduce сохраняет результат и затем опять же применяет к этому результату и
следующему элементу в наборе бинарную операцию.
В данном случае мы получим результат, равный `1 * 2 * 3 * 4 * 5 * 6`

Затем с помощью метода _get_ мы можем получить результат вычислений: `result.get()`

Пример объединения слов в предложение

```java
Stream<String> wordsStream = Stream.of("I", "love", "you");
Optional<String> s = wordsStream.reduce((x,y) -> x + " " + y);
System.out.println(s.get());
```

Если нам надо, чтобы первым элементом в наборе было какое-то определенное значение,
то мы можем использовать вторую версию метода `reduce()`, которая в качестве первого параметра принимает `T identity`.
Этот параметр хранит значение, с которого будет начинаться цепочка бинарных операций

```java
Stream<String> wordsStream = Stream.of("I", "love", "you");
String sentence = wordsStream.reduce("PS:", (x,y) -> x + " " + y);
System.out.println(sentence);
```

Использование параметра `identity` также подходит для тех случаев,
когда надо предоставить значение по умолчанию, если поток пустой и не содержит элементов.

В предыдущих примерах тип возвращаемых объектов совпадал с типом элементов, которые входят в поток.
Однако это не всегда удобно.
Возможно, мы захотим возвратить результат, тип которого отличается от типа объектов потока

Например, пусть у нас есть класс Phone, представляющий телефон.
Нужно найти сумму цен тех телефонов, у которых цена меньше определенного значения.
Для этого воспользуемся третьей версией метода `reduce`

```java
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

class PhoneTest {

    public static void main(String[] args) {
        Stream<Phone> phoneStream = Stream.of(
                new Phone("IPhone", 54000),
                new Phone("Samsung", 35000),
                new Phone("Xiaomi", 20000)
        );
                 
        phoneStream
            .flatMap(p->Stream.of(
                    String.format("название: %s  цена без скидки: %d", p.getName(), p.getPrice()),
                    String.format("название: %s  цена со скидкой: %d", p.getName(), (int) (p.getPrice() * 0.8))
            ))
            .forEach(s->System.out.println(s));
        
        int sum = phoneStream.reduce(0, 
                    (x,y)-> y.getPrice() < 50000 ? x + y.getPrice() : x + 0, 
                    (x, y) -> x + y);
                 
        System.out.println(sum); // 117000

    }
}
```

В качестве первого параметра идет значение по умолчанию - 0.
Второй параметр производит бинарную операцию, которая получает промежуточное значение -
суммарную цену текущего и предыдущего телефонов.
Третий параметр представляет бинарную операцию, которая суммирует все промежуточные вычисления.

---

### [Назад к оглавлению](../../README.md)