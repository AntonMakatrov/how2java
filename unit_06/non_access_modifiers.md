# Модификаторы дополнительного функционала (Non-Access Modifiers)

Java предоставляет ряд модификаторов не для доступа, а для реализации многих других функциональных возможностей:

-   Модификатор `static` применяется для создания методов и переменных класса
-   Модификатор `final` используется для завершения реализации классов, методов и переменных
-   Модификатор `abstract` необходим для создания абстрактных классов и методов
-   Модификаторы `synchronized` и `volatile` используются в Java для потоков

---

### static

-   Переменные
    -   используется для создания переменных, которые будут существовать независимо от каких-либо экземпляров, созданных для класса
    -   Только одна копия переменной static в Java существует вне зависимости от количества экземпляров класса
    -   Статические переменные также известны как переменные класса. В Java локальные переменные не могут быть объявлены статическими (static)
-   Методы
    -   используется для создания методов, которые будут существовать независимо от каких-либо экземпляров, созданных для класса
    -   В Java статические методы или методы static не используют какие-либо переменные экземпляра любого объекта класса, они определены
    -   Методы static принимают все данные из параметров и что-то из этих параметров вычисляется без ссылки на переменные

Переменные и методы класса могут быть доступны с использованием имени класса, за которым следует точка и имя переменной или метода.

```java
public class Counter {

    private static int num = 0;

    protected static int getCount() {
        return num;
    }

    private static void addItem() {
        num++;
    }

    Counter() {
        Counter.addItem(); 
    }

    public static void main(String[] arguments) {
        System.out.println("Создано " + Counter.getCount() + " экземпляров класса");
        for (int i = 0; i < 500; ++i) {
            new Counter();
        }
        System.out.println("Создано " + Counter.getCount() + " экземпляров класса");
    }
}
```

---

### final

Используется для завершения реализации:
-   переменных
    -   может быть инициализирована только один раз
    -   ссылочная final переменная никогда не может быть назначена для обозначения другого объекта.  
        Однако данные внутри объекта могут быть изменены. Состояние объекта может быть изменено, но не его ссылка
-   методов
    -   не может быть переопределен любым подклассом и предотвращает метод от изменений в подклассе
-   классов
    -   предотвращает класс от быть подклассом.
    -   ни один класс не может наследовать любую функцию из класса final
 
```java
public final class Test { // class
    
  final int value = 10; // var
  
  public static final int WIDTH = 6;  // const
  
  static final String TITLE = "Developer"; // const
  
  public void changeValue() { // что произойдет при выполнении это метода?
     value = 12; 
  }
  
  public final void changeName() { // method
     
  }
  
}
```

С переменными в Java модификатор final часто используется со static, чтобы сделать константой переменную класса.

---

### abstract

используется для создания абстрактных:
-   методов
    -   никогда не могут быть final или strict
    -   реализация обеспечивается подклассом
    -   заканчивается точкой с запятой
-   классов
    -   нельзя создать экземпляр этого класса
    -   единственная цель abstract класса - быть расширенным
    -   не может быть одновременно abstract и final
    -   класс содержащий абстрактные методы, должен быть объявлен как abstract
    -   не обязан содержать абстрактные методы
    -   может содержать как абстрактные методы, а также и обычные

```java
abstract class SuperClass {
    private double price;
    private String model;
    private String year;
    public abstract void doSomething();
    public abstract void changeSomething(int k);
}

class SubClass extends SuperClass {
    void doSomething() {

    }
   
    void changeSomething(int k) {
    
    }
}

```

---

### synchronized

-   используется для потоков
-   используется для указания того, что метод может быть доступен только одним потоком одновременно
-   может быть применен с любым из четырех модификаторов уровня доступа.

Пример

```java
public synchronized void showDetails() {

}
```

---

### transient

-   указывает виртуальной машине Java (JVM), чтобы пропустить определённую переменную при сериализации объекта, содержащего её.
-   включён в оператор, что создает переменную, предшествующего класса или типа данных переменной.

Пример

```java
public transient int limit = 55;
```

---

### volatile

-   используется для потоков
-   используется, чтобы позволить знать JVM, что поток доступа к переменной всегда должен объединять свою собственную копию переменной с главной копией в памяти.
-   доступ к переменной volatile синхронизирует все кэшированные скопированные переменные в оперативной памяти. 
-   может быть применен только к переменным экземпляра, которые имеют тип объект или private
-   ссылка на объект volatile может быть null

```java
public class MyRunnable implements Runnable {
    
    private volatile boolean active;
 
    public void run() {
        active = true;
        while (active){ // 1
           
        }
    }
    
    public void stop() {
        active = false; //2
    }
}
```

Как правило, _run()_ вызывается в одном потоке, а _stop()_ вызывается из другого потока.
Если в `1` используется кэшированное значение active, то цикл не может остановиться, пока не будет установлено active false в `2`

---

### [Назад к оглавлению](./README.md)
