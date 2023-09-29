# Перечисляемые типы (enumerations)

Кроме отдельных примитивных типов данных и классов в Java есть такой тип как enum или перечисление.
Перечисления представляют набор логически связанных констант.
Объявление перечисления происходит с помощью оператора enum, после которого идет название перечисления.
Затем идет список элементов перечисления через запятую:

```java
enum Day {
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}
```

Перечисление фактически представляет новый тип, поэтому мы можем определить переменную данного типа и использовать ее:

```java
public class Program {
      
    public static void main(String[] args) {
          
        Day current = Day.MONDAY;
        System.out.println(current);
    }
}

enum Day {
  
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}
```

Объявляя enum мы неявно создаем класс производный от `java.lang.Enum`.
Условно конструкция `enum Day { ... }` эквивалентна `class Day extends java.lang.Enum { ... }`.
И хотя явным образом наследоваться от `java.lang.Enum` нам не позволяет компилятор,
все же в том, что enum наследуется, легко убедиться с помощью reflection:

```java
System.out.println(Season.class.getSuperclass());
```
Наследование за нас автоматически выполняет компилятор Java.

---

### Элементы перечисления

Элементы enum **Day** (MONDAY, TUESDAY и т.д.) - это статически доступные экземпляры enum-класса **Day**.
Их статическая доступность позволяет нам выполнять сравнение с помощью оператора сравнения ссылок `==`

```java
Day day = Day.FRIDAY; 
if (day == Day.FRIDAY) {
    day = Day.SATURDAY;
}
```

---

### Название и порядковый номер элемента enum

Любой enum-класс наследует java.lang.Enum, который содержит ряд методов полезных для всех перечислений.

```java
Day day = Day.WEDNESDAY; 
System.out.println("day.name()=" + day.name());
System.out.println("day.toString()=" + day.toString());
System.out.println("day.ordinal()=" + day.ordinal()); 
```

---

### Получение элемента enum по строковому представлению его имени

Довольно часто возникает задача получить элемент enum по его строковому представлению.
Для этих целей в каждом enum-классе компилятор автоматически создает специальный статический метод `public static EnumClass valueOf(String name)`,
который возвращает элемент перечисления EnumClass с названием, равным name. 

```java
String name = "WEDNESDAY"; 
Day day = Day.valueOf(name);
```

В результате выполнения кода переменная day будет равна `Day.WEDNESDAY`. 
Следует обратить внимание, что если элемент не будет найден, то будет выброшен IllegalArgumentException,
а в случае, если name равен null - NullPointerException. 
Об этом, кстати, часто забывают.
Почему-то многие твердо уверенны, что если функция принимает один аргумент и при некоторых услових выбрасывает IllegalArgumentException,
то при передаче туда null, также будет неприменно выброшен IllegalArgumentException.
Данные методы enum-класс наследует из класса java.lang.Enum

---

### Получение всех элементов перечисления

Иногда необходимо получить список всех элементов enum-класса во время выполнения.
Для этих целей в каждом enum-классе компилятор создает метод `public static EnumClass[] values()`

```java
System.out.println(Arrays.toString(Day.values()));
```

Обратите внимание, что ни метод `valueOf()`, ни метод `values()` не определен в классе _java.lang.Enum_.
Вместо этого они автоматически добавляются компилятором на этапе компиляции enum-класса.

---

### Добавляем свои методы или свойства в enum-класс

У Вас есть возможность добавлять собственные методы или свойства как в enum-класс, так и в его элементы

```java
enum Direction { 
   UP, DOWN;
   
   public Direction opposite() { return this == UP ? DOWN : UP; } 
}

enum Direction { 
    UP { 
        public Direction opposite() { return DOWN; } 
    }, 
    DOWN { 
        public Direction opposite() { return UP; } 
    }; 

    public abstract Direction opposite(); 
}

enum Direction {
    UP(1), DOWN(2);
    
    private int index;

    public Direction(int index) {
        this.index = index;
    }
}
```

---

### Перечисления и параметрический полиморфизм

Перечисление не использует генерики (generics).
Дело в том, что в Java использование генериков в enum запрещено. 
Так следующий пример не скомпилируется:
```java
enum Type<T> {}
```

---

### [Назад к оглавлению](./README.md)
