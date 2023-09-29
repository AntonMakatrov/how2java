# Отображение. Метод map

Отображение или маппинг позволяет задать функцию преобразования одного объекта в другой,
то есть получить из элемента одного типа элемент другого типа.
Для отображения используется метод map 

`<R> Stream<R> map(Function<? super T, ? extends R> mapper)`

Передаваемая в метод map функция задает преобразование от объектов типа `T` к типу `R`.
И в результате возвращается новый поток с преобразованными объектами.

Выполним преобразование от типа Phone к типу String:

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
                 
        phoneStream
            .map(Phone::getName) // помещаем в поток только названия телефонов
            .forEach(System.out::println);
    }
}
```
Операция `map(Phone::getName)` ( аналогична `map(p-> p.getName())`) помещает в новый поток только названия телефонов.


Еще один пример преобразования

```java
phoneStream
    .map(p-> "название: " + p.getName() + " цена: " + p.getPrice())
    .forEach(System.out::println);
```

Здесь также результирующий поток содержит только строки, только теперь названия соединяются с ценами.

Для преобразования объектов в типы _Integer_, _Long_, _Double_ определены специальные методы:

-   `mapToInt()`
-   `mapToLong()`
-   `mapToDouble()`

---

### [Назад к оглавлению](../../README.md)