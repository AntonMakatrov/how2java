# Примеры использования [string](./string.md)

### Длина строки

Методы, используемые для получения информации об объекте, известны как методы доступа.
Один из методов доступа, который можно использовать со строками является метод `length()`,
он возвращает количество символов, содержащихся в строковом объекте.

Ниже представлен пример метода length(), который поможет определить длину строки.

```java
public class Test {
    public static void main(String args[]) {
        String s = "Я стану отличным программистом!";
        int len = s.length();
        System.out.println( "Длина строки: " + len + " символ.");
    }
}
```

### Объединение строк в Java

```java
string1.concat(string2);      // метод для объединения двух строк
"My name is ".concat("Oleg"); // concat() со строковыми литералами
"Hello" + " world" + "!"      // наиболее распространенный способ
```

```java
public class Test {
    public static void main(String args[]) {
        String string1 = "отличным ";
        System.out.println("Я стану " + string1 + "программистом!");
    }
}
```

### Создание формата строк

Класс строк в Java обладает методом `format()`, который возвращает строковый объект.

Использование строкового статического метода `format()` позволяет создавать строку нужного формата,
который можно использовать повторно, в отличие от одноразовых операторов **System.out.print**

```java
System.out.printf("Значение переменной float = " +
                   "%f, пока значение integer " +
                   "переменная = %d, и string " +
                   "= %s", floatVar, intVar, stringVar);

String fs = String.format("Значение переменной float = " +
                   "%f, пока значение integer " +
                   "переменная = %d, и string " +
                   "= %s", floatVar, intVar, stringVar);
System.out.println(fs);
```

---

### [Назад к оглавлению](./README.md)