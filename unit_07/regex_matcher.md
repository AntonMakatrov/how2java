# Класс Matcher

Как правило, для поиска соответствий применяется класса **Matcher**. Рассмотрим основные методы класса **Matcher**:

- `boolean matches()` возвращает **true**, если вся строка совпадает с шаблоном
- `boolean find()` возвращает **true**, если в строке есть подстрока, которая совпадает с шаблоном, и переходит к этой подстроке
- `String group()` возвращает подстроку, которая совпала с шаблоном в результате вызова метода `find()`.
Если совпадение отсутствует, то метод генерирует исключение **IllegalStateException**.
- `int start()` возвращает индекс текущего совпадения
- `int end()` возвращает индекс следующего совпадения после текущего
- `String replaceAll(String str)` заменяет все найденные совпадения подстрокой **str** и возвращает измененную строку с учетом замен

Чтобы использовать класс **Matcher**, вначале надо создать объект **Pattern** с помощью статического метода `compile()`,
который позволяет установить шаблон:

```java
Pattern pattern = Pattern.compile("Hello world");

String input = "Hello world! Hello Java!";

Matcher matcher = pattern.matcher(input);
```

В качестве шаблона выступает строка **"Hello world"**. Метод `compile()` возвращает объект **Pattern**,
который можно использовать.

В классе **Pattern** также определен метод `matcher(String input)`, который в качестве параметра принимает строку,
где надо проводить поиск, и возвращает объект Matcher:


Затем у объекта **Matcher** вызывается метод `matches()` для поиска соответствий шаблону в тексте:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class StringsApp {
 
    public static void main(String[] args) {
         
        String input ="Hello world";
        Pattern pattern = Pattern.compile("Hello world");
        Matcher matcher = pattern.matcher(input);
        boolean found = matcher.matches();
        if(found)
            System.out.println("no");
        else
            System.out.println("yes");
    }   
}
```

Рассмотрим более функциональный пример с нахождением не полного соответствия, а отдельных совпадений в строке.
Допустим, мы хотим найти в строке все вхождения слова Java.

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class StringsApp {
 
    public static void main(String[] args) {
         
        String input = "Hello Java! Hello JavaScript! JavaSE 8.";
        Pattern pattern = Pattern.compile("Java(\\w*)");
        Matcher matcher = pattern.matcher(input);
        while(matcher.find())
            System.out.println(matcher.group());
    }   
}
```

В исходной строке это три слова: **Java**, **JavaScript** и **JavaSE**.
Для этого применим шаблон `Java(\\w*)`.
Данный шаблон использует синтаксис регулярных выражений.
Слово **Java** в начале говорит о том, что все совпадения в строке должны начинаться на Java.
Выражение `(\\w*)` означает, что после **Java** в совпадении может находиться любое количество алфавитно-цифровых символов.
Выражение `\w` означает алфавитно-цифровой символ, а звездочка после выражения указывает на неопределенное их количество -
их может быть один, два, три или вообще не быть.
И чтобы java не рассматривала `\w` как эскейп-последовательность, как `\n`, то выражение экранируется еще одним слешем.

Далее применяется метод `find()` класса **Matcher**, который позволяет переходить к следующему совпадению в строке.
Первый вызов этого метода найдет первое совпадение в строке, второй вызов найдет второе совпадение и т.д.
С помощью цикла `while(matcher.find())` мы можем пройтись по всем совпадениям.
Каждое совпадение мы можем получить с помощью метода `matcher.group()`.

### Замена в строке

Сделаем замену всех совпадений с помощью метода `replaceAll()`

```java
String input = "Hello Java! Hello JavaScript! JavaSE 8.";
Pattern pattern = Pattern.compile("Java(\\w*)");
Matcher matcher = pattern.matcher(input);
String newStr = matcher.replaceAll("Groovy");
System.out.println(newStr);    // "Hello Groovy! Hello Groovy! Groovy 8."
```

В классе String также имеется метод `replaceAll()` с подобным действием:

```java
String input = "Hello Java! Hello JavaScript! JavaSE 8.";
String myStr =input.replaceAll("Java(\\w*)", "Groovy");
System.out.println(myStr); // Hello Groovy! Hello Groovy! Groovy 8.
```

### Разделение строки на лексемы

С помощью метода `String[] split(CharSequence input)` класса **Pattern** можно разделить строку на массив подстрок по определенному разделителю.
Например, нужно выделить из строки отдельные слова:

```java
import java.util.regex.Pattern;
 
public class StringsApp {
 
    public static void main(String[] args) {
        String input = "Hello Java! Hello JavaScript! JavaSE 8.";
        Pattern pattern = Pattern.compile("[ ,.!?]+");
        String[] words = pattern.split(input);
        for(String word : words) {
            System.out.println(word);
        }
    }   
}
```

При применении метода `split()` **все символы-разделители(delimiter) удаляются**.

В классе String также имеется метод `split()` с подобным действием:

```java
public class StringsApp {
 
    public static void main(String[] args) {
        String input = "Hello Java! Hello JavaScript! JavaSE 8.";
        String[] words = input.split("[ ,.!?]+");
        for(String word : words) {
            System.out.println(word);
        }
    }   
}
```

---

### [Назад к оглавлению](./README.md)