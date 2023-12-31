# Дженерики (generics)

Обобщения или generics (обобщенные типы и методы) позволяют нам уйти от жесткого определения используемых типов.
Рассмотрим проблему, в которой они нам могут понадобиться.

Допустим, мы определяем класс для представления банковского счета.
К примеру, он мог бы выглядеть следующим образом:

```java
class Account {
     
    private int id;
    private int sum;
     
    Account(int id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public int getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```

Класс Account имеет два поля: id - уникальный идентификатор счета и sum - сумма на счете.

В данном случае идентификатор задан как целочисленное значение, например, 1, 2, 3, 4 и так далее.
Однако также нередко для идентификатора используются и строковые значения.
И числовые, и строковые значения имеют свои плюсы и минусы.
И на момент написания класса мы можем точно не знать, что лучше выбрать для хранения идентификатора - строки или числа.
Либо, возможно, этот класс будет использоваться другими разработчиками, которые могут иметь свое мнение по данной проблеме.
Например, в качестве типа id они захотят использовать какой-то свой класс.

И на первый взгляд мы можем решить данную проблему следующим образом: задать id как поле типа Object, который является универсальным и базовым суперклассом для всех остальных типов:

```java
public class Program{
      
    public static void main(String[] args) {
          
        Account acc1 = new Account(2334, 5000); // id - число
        int acc1Id = (int)acc1.getId();
        System.out.println(acc1Id);
         
        Account acc2 = new Account("sid5523", 5000);    // id - строка
        System.out.println(acc2.getId());
    }
}

class Account{
     
    private Object id;
    private int sum;
     
    Account(Object id, int sum){
        this.id = id;
        this.sum = sum;
    }
    
    public Object getId() { return id; }
        public int getSum() { return sum; }
        public void setSum(int sum) { this.sum = sum; }
}
```

В данном случае все замечательно работает.
Однако в данном случае мы сталкиваемся с проблемой безопасности типов.
Например, в следующем случае мы получим ошибку:

```java
Account acc1 = new Account("2345", 5000);
int acc1Id = (int)acc1.getId(); // java.lang.ClassCastException
System.out.println(acc1Id);
```

Проблема может показаться искуственной, так как в данном случае мы видим,
что в конструктор передается строка, поэтому вряд ли будет пытаться преобразовать к типу int.
Однако в процессе разработки мы можем не знать, какой именно тип представляет значение в id,
 и при попытке получить число в данном случае мы столкнемся с исключением java.lang.ClassCastException.

Писать для каждого отдельного типа свою версию класса Account тоже не является хорошим решением,
так как в этом случае мы вынуждены повторяться.

Эти проблемы были призваны устранить обобщения или generics.
Обобщения позволяют не указывать конкретный тип, который будет использоваться.
Поэтому определим класс Account как обобщенный:

```java
class Account<T>{
     
    private T id;
    private int sum;
     
    Account(T id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public T getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```

С помощью буквы T в определении класса class Account<T> мы указываем,
что данный тип T будет использоваться этим классом.
Параметр T в угловых скобках называется универсальным параметром, так как вместо него можно подставить любой тип.
При этом пока мы не знаем, какой именно это будет тип: String, int или какой-то другой.
Причем буква T выбрана условно, это может и любая другая буква или набор символов.

После объявления класса мы можем применить универсальный параметр T:
так далее в классе объявляется переменная этого типа, которой затем присваивается значение в конструкторе.

Метод getId() возвращает значение переменной id, но так как данная переменная представляет тип T, 
то данный метод также возвращает объект типа T: public T getId().

Используем данный класс:

```java
public class Program {
      
    public static void main(String[] args) {
          
        Account<String> acc1 = new Account<String>("2345", 5000);
        String acc1Id = acc1.getId();
        System.out.println(acc1Id);
         
        Account<Integer> acc2 = new Account<Integer>(2345, 5000);
        Integer acc2Id = acc2.getId();
        System.out.println(acc2Id);
    }
}

class Account<T>{
     
    private T id;
    private int sum;
     
    Account(T id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public T getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```

При определении переменной даннного класса и создании объекта после имени класса в угловых скобках нужно указать,
какой именно тип будет использоваться вместо универсального параметра.
При этом надо учитывать, что они работают только с объектами, но не работают с примитивными типами.
То есть мы можем написать Account<Integer>, но не можем использовать тип int или double, например, Account<int>.
Вместо примитивных типов надо использовать классы-обертки: Integer вместо int, Double вместо double и т.д.

Например, первый объект будет использовать тип String, то есть вместо T будет подставляться String:

```java
Account<String> acc1 = new Account<String>("2345", 5000);
```

В этом случае в качестве первого параметра в конструктор передается строка.

А второй объект использует тип int (Integer):

```java
Account<Integer> acc2 = new Account<Integer>(2345, 5000);
```

### Обобщенные интерфейсы

Интерфейсы, как и классы, также могут быть обобщенными.
Создадим обобщенный интерфейс Accountable и используем его в программе:

```java
public class Program {
      
    public static void main(String[] args) {
          
        Accountable<String> acc1 = new Account("1235rwr", 5000);
        Account acc2 = new Account("2373", 4300);
        System.out.println(acc1.getId());
        System.out.println(acc2.getId());
    }
}
interface Accountable<T>{
    T getId();
    int getSum();
    void setSum(int sum);
}
class Account implements Accountable<String>{
     
    private String id;
    private int sum;
     
    Account(String id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public String getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```

При реализации подобного интерфейса есть две стратегии.
В данном случае реализована первая стратегия, когда при реализации для универсального параметра интерфейса задается конкретный тип,
как например, в данном случае это тип String.
Тогда класс, реализующий интерфейс, жестко привязан к этому типу.

Вторая стратегия представляет определение обобщенного класса
который также использует тот же универсальный параметр:

```java
public class Program{
      
    public static void main(String[] args) {
          
        Account<String> acc1 = new Account<String>("1235rwr", 5000);
        Account<String> acc2 = new Account<String>("2373", 4300);
        System.out.println(acc1.getId());
        System.out.println(acc2.getId());
    }
}
interface Accountable<T>{
    T getId();
    int getSum();
    void setSum(int sum);
}
class Account<T> implements Accountable<T>{
     
    private T id;
    private int sum;
     
    Account(T id, int sum){
        this.id = id;
        this.sum = sum;
    }
     
    public T getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```

### Обобщенные методы

Кроме обобщенных типов можно также создавать обобщенные методы,
которые точно также будут использовать универсальные параметры. 

```java
public class Program {
      
    public static void main(String[] args) {
          
        Printer printer = new Printer();
        String[] people = {"Tom", "Alice", "Sam", "Kate", "Bob", "Helen"};
        Integer[] numbers = {23, 4, 5, 2, 13, 456, 4};
        printer.<String>print(people);
        printer.<Integer>print(numbers);
    }
}
 
class Printer {
     
    public <T> void print(T[] items){
        for(T item: items){
            System.out.println(item);
        }
    }
}
```

Особенностью обобщенного метода является использование универсального параметра
в объявлении метода после всех модификаторов и перед типом возвращаемого значения.

```java
public <T> void print(T[] items)
```

Затем внутри метода все значения типа T будут представлять данный универсальный параметр.

При вызове подобного метода перед его именем в угловых скобках указывается,
какой тип будет передаваться на место универсального параметра:

```java
printer.<String>print(people);
printer.<Integer>print(numbers);
```

### Использование нескольких универсальных параметров

Мы можем также задать сразу несколько универсальных параметров:

```java
public class Program {
      
    public static void main(String[] args) {
        Account<String, Double> acc1 = new Account<String, Double>("354", 5000.87);
        String id = acc1.getId();
        Double sum = acc1.getSum();
        System.out.printf("Id: %s  Sum: %f \n", id, sum);
    }
}
class Account<T, S> {
     
    private T id;
    private S sum;
     
    Account(T id, S sum){
        this.id = id;
        this.sum = sum;
    }
     
    public T getId() { return id; }
    public S getSum() { return sum; }
    public void setSum(S sum) { this.sum = sum; }
}
```

В данном случае тип String будет передаваться на место параметра T, а тип Double - на место параметра S.

### Обобщенные конструкторы

Конструкторы как и методы также могут быть обобщенными.
В этом случае перед конструктором также указываются в угловых скобках универсальные параметры:

```java
public class Program {
      
    public static void main(String[] args) {
        Account acc1 = new Account("cid2373", 5000);
        Account acc2 = new Account(53757, 4000);
        System.out.println(acc1.getId());
        System.out.println(acc2.getId());
    }
}
 
class Account{
     
    private String id;
    private int sum;
     
    <T>Account(T id, int sum){
        this.id = id.toString();
        this.sum = sum;
    }
     
    public String getId() { return id; }
    public int getSum() { return sum; }
    public void setSum(int sum) { this.sum = sum; }
}
```

В данном случае конструктор принимает параметр id, который представляет тип T.
В конструкторе его значение превращается в строку и сохраняется в локальную переменную.

### Шаблоны аргументов

Шаблон аргументов указывается символом `?` и представляет собой неизвестный тип.

```java
boolean sameAvg(Stats<?> ob)
```

Знак вопроса заменяет Object и мы можем использовать любой класс, 
который в любом случае будет происходить от Object.

Мы можем ограничить диапазон объектов, указав суперкласс.

```java
public void addItems(ArrayList<? extends Animal> list)
```

В этом случае можно использовать классы, которые могут быть наследниками Animal - Dog, Cat.
А String или Integer вы уже не сможете использовать.

Отдельно стоит упомянуть новинку JDK 7, позволяющую сократить код.

```java
MyClass<Integer, String> mcObj = new MyClass<Integer, String>(33, "Meow"); // старый способ в JDK 6
MyClass<Integer, String> mcObj = new MyClass<>(33, "Meow"); // новый способ в JDK 7
```

**Помните**! что нельзя создать экземпляр типа параметра.

```java
class Gen {
    T ob;
    
    Gen() {
        ob = new T(); // Недопустимо
    }
}
```

---

### [Назад к оглавлению](./README.md)

