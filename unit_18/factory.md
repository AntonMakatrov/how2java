# Factory

Данный шаблон проектирования предоставляет интерфейс для создания экземпляров некоторого класса

---

### Область применения

-   можно создавать объекты разных типов с помощью одного и того же метода.
    Это очень удобно, когда возникает ситуация, в которой мы не знаем, какой тип нам понадобится.
-   можно "запаковать" дополнительный функционал в Фабрику.
    Например, посчитаем, сколько объектов каждого типа было создано конкретной фабрикой.
-   с помощью паттерна Factory мы можем генерировать сложные объекты намного проще и с меньшим количеством ошибок.

---

### Реализация

```java
public interface Shape {
    void draw();
}
```

```java
public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Rectangle");
    }
}

public class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Square");
    }
}

public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Circle");
    }
}
```

```java
public enum ShapeType {
    SQUARE,
    RECTANGLE,
    CIRCLE
}
```

```java
public class ShapeFactory {
    public Shape getShape(ShapeType shapeType){
        switch (shapeType) {
            case SQUARE:
                return new Square();
            case RECTANGLE:
                return new Rectangle();
            case CIRCLE:
                return new Circle();
            default:
                return null;
        }
    }
}
```

```java
public class FactoryPatternDemo {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        Shape shape1 = shapeFactory.getShape(ShapeType.CIRCLE);
        shape1.draw();

        Shape shape2 = shapeFactory.getShape(ShapeType.RECTANGLE);
        shape2.draw();

        Shape shape3 = shapeFactory.getShape(ShapeType.SQUARE);
        shape3.draw();
    }
}
```

---

### [Назад к оглавлению](./README.md)