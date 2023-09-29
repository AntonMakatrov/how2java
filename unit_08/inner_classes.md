# Внутренние классы

Создать внутренний класс в Java довольно просто - нужно написать класс внутри класса.
В отличие от класса, внутренний класс может быть закрытым (private), и после того,
как внутренний класс объявлен закрытым, он не может быть доступен из объекта вне класса.

Ниже приведен пример создания внутреннего класса и получения доступа к нему.
В данном примере мы делаем внутренний класс private и получаем доступ к классу с помощью метода.

```java
class OuterDemoClass {

    int num;
    
    // Внутренний класс
    private class InnerDemoClass {
        public void print() {
            System.out.println("Это внутренний класс");
        }
    }
    
    // Доступ к внутреннему классу из метода
    void displayInnerClass() {
        InnerDemoClass inner = new InnerDemoClass();
        inner.print();
    }
}
   
public class MyTestClass {

    public static void main(String args[]) {
        // Создание внешнего класса
        OuterDemoClass outer = new OuterDemoClass();
        
        // Доступ к методу displayInnerClass()
        outer.displayInnerClass();
    }
}   
```

`OuterDemoClass` – внешний класс  
`InnerDemoClass` – внутренний класс  
`displayInnerClass()` – метод, внутри которого мы создаем внутренний класс.
Этот метод вызывается из основного метода

---

#### Доступ к частным (private) членам

Как упоминалось ранее, внутренние классы также используются в Java для доступа к закрытым членам класса.
Предположим, у класса есть private члены.
Для доступа к ним напишите в нем внутренний класс, верните частные члены из метода внутри внутреннего класса, 
скажем, методом **getValue()** и, наконец, из другого класса
(из которого Вы хотите получить доступ к закрытым членам) вызовите метод **getValue()** внутреннего класса.

Чтобы создать экземпляр внутреннего класса, сначала Вам необходимо создать экземпляр внешнего класса.
После этого, используя объект внешнего класса, Вы можете создать экземпляр внутреннего класса.

```java
OuterDemoClass outer = new OuterDemoClass();
OuterDemoClass.InnerDemoClass inner = outer.new InnerDemoClass();
```

Следующий пример показывает, как получить доступ к закрытым членам класса с использованием внутреннего класса.

```java
class OuterDemoClass {
    // Частная переменная внешнего класса
    private int num = 2018;  
    
    // Внутренний класс
    public class InnerDemoClass {
        public int getNum() {
            System.out.println("Это метод getNum внутреннего класса");
            return num;
        }
    }
}

public class MyTestClass {

   public static void main(String args[]) {
      // Создание внешнего класса
      OuterDemoClass outer = new OuterDemoClass();
      
      // Создание внутреннего класса
      OuterDemoClass.InnerDemoClass inner = outer.new InnerDemoClass();
      System.out.println(inner.getNum());
   }
}
```

---

### [Назад к оглавлению](./README.md)