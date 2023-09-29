# Плоское отображение. Метод flatMap

Плоское отображение выполняется тогда, когда из одного элемента нужно получить несколько. 
Данную операцию выполняет метод _flatMap_ 

`<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)`

 примере выше мы выводим название телефона и его цену.
 Но что, если мы хотим установить для каждого телефона цену со скидкой и цену без скидки.
 То есть из одного объекта Phone нам надо получить два объекта с информацией, например, в виде строки.
 Для этого применим flatMap:

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
            .flatMap(p->Stream.of(
                    String.format("название: %s  цена без скидки: %d", p.getName(), p.getPrice()),
                    String.format("название: %s  цена со скидкой: %d", p.getName(), (int) (p.getPrice() * 0.8))
            ))
            .forEach(s->System.out.println(s));
    }
}
```

---

### [Назад к оглавлению](../../README.md)