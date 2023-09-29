# Вопросы и задания по теме [типы данных](./data_types.md)

Дан код.
- какие из строчек вызывают ошибку компиляции? 
- в каких строчках есть предупреждение?
- какие символы хранятся в переменных типа char (если они не вызывают ошибку компиляции)?

```java
public class Main {
  public static void main(String[] args) {
    byte a = 44;
    byte b = 128;
    byte c = 5 + 7 * 5;

    short d = 123 + 3210;
    short e = d - 1;

    int f = 1024768;
    int g = 455 / 10;
    int h = 78 + 8L;

    long i = 611942;
    long j = '6934930';
    long k = 7684849303l;
    long l = 1234567890123456789;

    double m = 99;
    double n = 122224.56623423;
    double o = 333f;
    double p = 0D;

    float q = 2 * 3;
    float r = 67 / 31;
    float s = 77 * 9d;
    float t = 1.01;
    float u = 5F;

    char v = 'a';
    char w = 115;
    char x = 'f' + 3;
    char y = "a";
    char z = 'z' - 'A';
    char za = 'a' - 'b';
  }
}
```

---

Дан код.
Какие из переменных являются ссылочными?

```java
public class Main {
  public static void main(String[] args) {
      
    double pi = 3.14;
    Cat sheldon = new Cat("Sheldon");
    String message = "Please open the window.";
    int a;
    Integer days = 759;
    
    Pet penny;
    String[][][] test;
    Dog bars = new Dog();
    String greeting = "Hello students.";
    Message onFail;
    
    int[] arr;
    String name;
  }
}
```

---

Дан код.
Какие из строк кода приведут к ошибке компиляции из-за неправильного приведения типов?

```java
public class Main {
    public static void main(String[] args) {
        int i = 3;                      // line 1
        byte b = 1;                     // line 2 
        byte b1 = 1 + 2;                // line 3     
        short s = 304111;               // line 4 
        short s1 = (short) 304111;      // line 5
        b = b1 + 1;                     // line 6 
        b = (byte)  (b1 + 1);           // line 7
        b = -b;                         // line 8 
        b = (byte) -b;                  // line 9
        b1 *= 2;                        // line 10
        b = i;                          // line 11
        b = (byte)  i;                  // line 12
        b += i++;                       // line 13
        float f = 1.1f;                 // line 14
        b /= f;                         // line 15
    }
}
```

---

### [Назад к оглавлению](./README.md)