# Работа с числами

- [Константы](#Константы)
- [Основные методы для работы с числами](#Основные-методы-для-работы-с-числами)
  - [Округление чисел](#Округление-чисел)
  - [Тригонометрические методы](#Тригонометрические-методы)
  - [Преобразование строки в число](#Преобразование-строки-в-число)
  - [Преобразование числа в строку](#Преобразование-числа-в-строку)
  - [Форматированный вывод чисел](#Форматированный-вывод-чисел)
  - [Генерация псевдослучайных чисел](#Генерация-псевдослучайных-чисел)
  - [Бесконечность и значение NaN](#Бесконечность-и-значение-NaN)

### Константы

Для хранения неизменных данных в Java предназначены константы. Они будут встречаться на протяжении всего курса.
Подробнее о них можно прочитать [здесь](../unit_02/variables.md#Статические-переменные-или-переменные-класса).

Для численных типов данных существуют константы диапазона и размера в байтах.
Найти их можно в соответствующих [классах-оболочках]()

Пример:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Byte.MIN_VALUE);             // -128
        System.out.println(Byte.MAX_VALUE);             // 127
        System.out.println(Byte.BYTES);                 // 1
        
        System.out.println(Short.MIN_VALUE);            // -32 768
        System.out.println(Short.MAX_VALUE);            // 32 767
        System.out.println(Short.BYTES);                // 2
        
        System.out.println(Integer.MIN_VALUE);          //-2 147 483 648
        System.out.println(Integer,MAX_VALUE);          // 2 147 483 647
        System.out.println(Integer.BYTES);              // 4
        
        System.out.println(Long.MIN_VALUE);             // -9 223 372 036 854 775 808
        System.out.println(Long.MAX_VALUE);             // 9 223 372 036 854 775 807
        System.out.println(Long.BYTES);                 // 8
        
        System.out.println((int)Character.MIN_VALUE);   // 0
        System.out.println((int)Character.MAX_VALUE);   // 65 535
        System.out.println(Character.BYTES);            // 2

        System.out.println(Float.MIN_VALUE);            // 1.4 E-45
        System.out.printIn(Float.MAX_VALUE);            // 3.4028235 E38
        System.out.println(Float.BYTES);                // 4
        
        System.out.println(Double.MIN_VALUE);           // 4.9 E-324
        System.out.println(Double.MAX_VALUE);           // 1.7976931348623157 E308
        System.out.println(Double.BYTES);               // 8
    }
}
```

Так же полезные математические числовые константы можно встретить в классе `java.lang.Math`.

Пример:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Math.PI);    // число Пи
        System.out.println(Math.E);     // число Эйлера
    }
}
```

---

### Основные методы для работы с числами


Для работы с числами предназначены следующие методы из класса `java.lang.Math`:

- `abs(a)` возвращает абсолютное значение числа `а`
- `pow(a, b)` возводит число `a` в степень `b`
- `sqrt(a)` квадратный корень числа `a`
- `exp(a)` экспонента числа `a`
- `log(a)` натуральный логарифм числа `a`
- `log10(a)` десятичный логарифм числа `a`
- `max(a, b)` максимальное значение из чисел `a` и `b`
- `min(a, b)` минимальное значение из чисел `a` и `b`

Пример:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Math.abs(-1));           // 1

        System.out.println(Math.pow(10, 2));        // 100.0
        System.out.println(Math.pow(3.0, 3.0));     // 27.0

        System.out.println(Math.max(10, 3));        // 10
        System.out.println(Math.min(10, 3));        // 3
    }
}
```

---

### Округление чисел

Для округления чисел предназначены следующие методы из класса `java.lang.Math`:

- `ceil(a)` — возвращает значение, округленное до ближайшего большего значения
- `floor(a)` — значение, округленное до ближайшего меньшего значения
- `round(a)` — возвращает число, округленное до ближайшего меньшего целого — для чисел с дробной частью меньше `0.5`,
  или значение, округленное до ближайшего большего целого — для чисел с дробной частью больше или равной `0.5`

Пример:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Math.ceil(1.49));    // 2.0
        System.out.println(Math.ceil(1.5));     // 2.0 
        System.out.println(Math.ceil(1.51));    // 2.0

        System.out.println(Math.floor(1.49));   // 1.0
        System.out.println(Math.floor(1.5));    // 1.0
        System.out.println(Math.floor(1.51));   // 1.0

        System.out.println(Math.round(1.49));   // 1
        System.out.println(Math.round(1.5));    // 2 
        System.out.println(Math.round(1.51));   // 2
    }
}
```

---

### Тригонометрические методы

В языке Java доступны следующие основные тригонометрические методы:

- `sin(a)` синус
- `cost(a)` косинус
- `tan(a)` тангенс
- `asin(a)` арксинус
- `acost(a)` арккосинус
- `atan(a)` арктангенс
- `toRadians(a)` преобразует градусы в радианы
- `toDegrees(a)` преобразует радианы в градусы

Пример:

```java
public class Main {
    public static void main(String[] args) {
      System.out.println(Math.sin(Math.toRadians(90.0)));   // 1.0
      System.out.println(Math.toRadians(180.0));            // 3.141592653589793
      System.out.println(Math.toDegrees(Math.PI));          // 180.0
    }
}
```

---

### Преобразование строки в число

В языке Java числа могут быть представлены в виде строки.
Чтобы в дальнейшем использовать эти числа, необходимо выполнить преобразование строки в число.
Для этого предназначены следующие методы:

- `Byte.parseByte()` возвращает целое число типа `byte`
- `Short.parseShort()` возвращает целое число типа `short`
- `Integer.parseInt()` возвращает целое число типа `int`
- `Long.parseLong()` возвращает целое число типа `long`
- `Float.parseFloat()` возвращает вещественное типа типом `float`
- `Double.parseDouble()` возвращает вещественное типа типом `double`

Вторым параметром (`radix`) можно задавать систему счисления.

Пример:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Byte.parseByte("119"));              // 119 - десятичная система по умолчанию
        System.out.println(Byte.parseByte("01110111", 2));      // 119 - двоичная система
      
        System.out.println(Byte.parseShort("119"));             // 119
        System.out.println(Byte.parseShort("01110111", 2));     // 119

        System.out.println(Byte.parseInt("119"));               // 119
        System.out.println(Byte.parseInt("01110111", 2));       // 119

        System.out.println(Byte.parseLong("119"));              // 119L
        System.out.println(Byte.parseLong("01110111", 2));      // 119L

        System.out.println(Byte.parseFloat("119.5"));           // 119.5
        System.out.println(Byte.parseFloat("119.5e2"));         // 11950.0 

        System.out.println(Byte.parseDouble("119.5"));          // 119.5
        System.out.println(Byte.parseDouble("119.5e2"));        // 11950.0 
    }
}
```

---

### Преобразование числа в строку

Чтобы преобразовать число в строку, достаточно выполнить операцию конкатенации (объединение строк).
Если один из операндов не является строкой, то производится его автоматическое преобразование в строку.

Однако конкатенация выполняется очень медленно.
Вместо конкатенации лучше использовать метод `String.valueOf()`.

Для преобразования числа в строку можно также воспользоваться следующими методами:

- `toString()` этот метод есть у всех классов
- `toBinaryString()` возвращает строковое представление целого числа в двоичной системе
- `toOctalString()` возвращает строковое представление целого числа в восьмеричной системе
- `toHexString()` возвращает строковое представление целого числа в шестнадцатеричной системе

Пример:

```java
public class Main {
    public static void main(String[] args) {
        int х = 100;
        double у = 1.8;
        
        String s1 = "х = " + х;                   // s1 = "x = 100"
        String s2 = String.valueOf(y);            // s2 = "1.8"

        String s3 = Integer.toString(x);          // s3 = "100"
        String s4 = Double.toString(y);           // s4 = "1.8"
        
        String s5 = Integer.toBinaryString(119);  // s5 = "1110111"
        String s6 = Integer.toOctaistring(119);   // s6 = "167"
        String s7 = Integer.toHexstring(119);     // s7 = "77"

        //для отрицательных чисел
        String s8 = Integer.toString(-119, 2);    // s8 = -1110111
        String s9 = Integer.toBinaryString(-119); // s9 = 11111111111111111111111110001001
    }
}
```

---

### Форматированный вывод чисел

Для форматированного вывода чисел предназначен метод `System.out.printf()` для вывода в консоль или метод `String.format()`

Пример:

```java
public class Main {
    public static void main(String[] args) {
        int x = 123;
        double y = 10.5125189;

        // число занимает 2 или более знаков
        String s1 = String.format("%2d", 123);      // s1 = "123"
        // число занимает 5 или более знаков
        String s2 = String.format("%5d", 123);      // s2 = "  123" число

        // не более 4 знаков после запятой
        String s3 = String.format("y = %.4f", y);   // s3 = "y = 10.5125"
        // не более 3 знаков после запятой
        String s4 = String.format("y = %.3f", y);   // s4 = "y = 10.513"
        // число занимает 6 или более знаков и не более 2 знаков после запятой (появился впереди пробел)
        String s5 = String.format("y = %6.2f", y);  // s5 = "y =  10.51"
    }
}
```

---

### Генерация псевдослучайных чисел

Для генерации случайных чисел в языке Java предназначен метод `Math.random()`.
Метод возвращает псевдослучайное число, которое больше или равно (`>=`) значению `0.0` и меньше (`<`) значения `1.0` (промежуток `[0.0; 1.0)`).

Для генерации псевдослучайных чисел можно также воспользоваться классом `java.util.Random`.

Пример:

```java
import java.util.Random;

public class Main {
    public static void main(String[] args) {
        System.out.println(Math.random());    // 0.9716780632629719
        System.out.println(Math.random());    // 0.32302953237853427
        System.out.println(Math.random());    // 0.779069650193378

        // В промежутке [0; 9]
        System.out.println((int)(Math.random() * 10));
        // В промежутке [15; 18]
        System.out.println((int)(Math.random() * 4) + 15);
        // В промежутке [-100; 100]
        System.out.println((int)(Math.random() * 201) - 100);

        
        Random r = new Random();

        // В диапазоне int
        System.out.println(r.nextInt());      // 288354376
        // В промежутке [0; 4]
        System.out.println(r.nextInt(5));     // 4
        // В диапазоне long
        System.out.println(r.nextLong());     // 207806838985576L
        // В промежутке [0.0; 1.0)
        System.out.println(r.nextFloat());    // 0.2868402
        System.out.println(r.nextDouble());   // 0.3770044403409455
        // boolean значение
        System.out.println(r.nextBoolean());  // false
    }
}
```

---

### Бесконечность и значение NaN

Целочисленное деление на `0` приведет к ошибке при выполнении программы.
С вещественными числами все обстоит несколько иначе.
Деление вещественного числа на `0.0` приведет к значению `+Infinity` или `-Infinity` (бесконечность);
Деление вещественного числа `0.0` на `0.0` — к значению `NaN` (нет числа)

Пример:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Double.POSITIVE_INFINITY);         // Infinity
        System.out.println(Double.NEGATIVE_INFINITY);         //-Infinity
        System.out.println(Double.NaN);                       // NaN

        System.out.println(10.0 / 0);                         // Infinity
        System.out.println(-10.0 / 0);                        // -Infinity
        System.out.println(0.0 / 0);                          // NaN

        System.out.println(Double.isInfinite(10.0 /1.0));     // false
        System.out.println(Double.isInfinite(-10.0 / 0.0));   // true
        System.out.println(Double.isFinite(0.0 / 0.0));       // false

        System.out.println(Double.isFinite(10.0 /1.0));       // true
        System.out.println(Double.isFinite(-10.0 / 0.0));     // false
        System.out.println(Double.isFinite(0.0 / 0.0));       // false

        System.out.println(Double.isNaN(10.0 /0.0));          // false
        System.out.println(Double.isNaN(0.0 /0.0));           // true
    }
}
```

---

### [Назад к оглавлению](./README.md)