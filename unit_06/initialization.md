# Инициализация. Блоки инициализации

Для того, чтобы понять, что такое блоки инициализации, сначала разберемся что такое инициализация.

**Инициализация** (от англ. _initialize_, от  _initial_ - "начальный, первоначальный") -
это когда мы впервые задаем переменной какое-либо значение

Например, у нас есть переменная `int counter;`.
Переменная есть, но пока в ней ничего не лежит.
Мы ее не инициализировали - другими словами, не задали начальное, стартовое значение.

Если попытаться вывести её на экран, будет ошибка компиляции

```java
public class Test {
    public static void main(String[] args) {
        int counter;
        System.out.println(counter); // Variable 'counter' might not have been initialized
    }
}
```

Инициализировав переменную и присвоив какое-нибудь значение, ошибка будет исправлена

---

### Привычные способы инициализации

```java
public class Test {
    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5};  // <- 
        int i = 5; // <-
    }
}
```

---

### Инициализация классов

```java
public class Country {
    private String currency;
    private String language;
    private LocalDate created;

    public Country(String currency, String language) {
        this.currency = currency;
        this.language = language;
        created = LocalDate.now();
    }
}
```

---

### Инициализация с помощью блоков

Допустим, что мы хотим задать базовые значения переменных. Можно сделать это так:

```java
public class Country {
    private String currency = "US Dollar";
    private String language = "English";
    private LocalDate created = LocalDate.of(1776, Month.JULY, 4);

    public Country(String currency, String language) {
        this.currency = currency;
        this.language = language;
        created = new Date();
    }
}
```

Но можно воспользоваться блоком инициализации:

```java
public class Country {
    private String currency; 
    private String language;
    private LocalDate created;

    {
        currency = "US Dollar";
        language = "English";
        created = LocalDate.of(1776, Month.JULY, 4);
    }

    public Country(String currency, String language) {
        this.currency = currency;
        this.language = language;
        created = new Date();
    }
}
```

---

### Виды блоков инициализации

Существует всего два типа блоков:

-    нестатический `instance initializer`
-    статический `class initializer`

```java
public class Test {
    {
       // instance initializer
    }
    
    static {
       // class initializer
    }
}
```

статический блок используется для инициализации статических переменных, а обычный  - для всех остальных.

---

### Зачем используются блоки инициализации?

-   делают код читабельнее
-   Внутри блоков инициализации мы можем не только присваивать значения, но и можно писать любые команды.
    Очень похож на метод

---

### [Назад к оглавлению](./README.md)