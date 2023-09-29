# Фильтрация. Метод filter
Для фильтрации элементов в потоке применяется метод `filter()`, который представляет промежуточную операцию.
Он принимает в качестве параметра некоторое условие в виде объекта `Predicate<T>` и возвращает новый поток из элементов,
которые удовлетворяют этому условию

```java
Stream<String> citiesStream = Stream.of("Moscow", "London", "Madrid", "Barcelona");
citiesStream.filter(s -> s.length() == 6)
            .forEach(System.out::println);
```

Условие `s.length() == 6` возвращает **true** для тех элементов, длина которых равна **6** символам.

Еще один пример фильтрации с более сложными данными. Допустим, у нас есть следующий класс Phone. Отфильтруем набор телефонов по цене

```java
class Phone {
     
    private String name;
    private int price;
     
    public Phone(String name, int price) {
        this.name=name;
        this.price=price;
    }
     
    public String getName() {
        return name;
    }
     
    public void setName(String name) {
        this.name = name;
    }
     
    public int getPrice() {
        return price;
    }
     
    public void setPrice(int price) {
        this.price = price;
    }
}

class PhoneTest {

    public static void main(String[] args) {
        Stream<Phone> phoneStream = Stream.of(
                new Phone("IPhone", 54000),
                new Phone("Samsung", 35000),
                new Phone("Xiaomi", 20000)
        );
                 
        phoneStream.filter(p->p.getPrice()<50000)
                    .forEach(p -> System.out.println(p.getName()));
    }
}
```

---

### [Назад к оглавлению](../../README.md)