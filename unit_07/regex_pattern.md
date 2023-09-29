# Класс Pattern

Большая часть функциональности по работе с регулярными выражениями в Java сосредоточена в пакете `java.util.regex`.

Само регулярное выражение представляет шаблон для поиска совпадений в строке.
Для задания подобного шаблона и поиска подстрок в строке, которые удовлетворяют данному шаблону,
в Java определены классы `Pattern` и `Matcher`.

Для простого поиска соответствий в классе `Pattern` определен статический метод `boolean matches(String pattern, CharSequence input)`.
Данный метод возвращает **true**, если последовательность символов **input** полностью соответствует шаблону строки **pattern**

```java
import java.util.regex.Pattern;
 
public class StringsApp {
 
    public static void main(String[] args) {
         
        String input = "Hello world";
        boolean found = Pattern.matches("Hello world", input);
        if(found)
            System.out.println("yes");
        else
            System.out.println("no");
    }   
}
```

---

### [Назад к оглавлению](./README.md)