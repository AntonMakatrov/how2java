# Анонимные классы (anonymous classes)

**Анонимный внутренний класс** — это внутренний класс, объявленный без имени класса.
В случае анонимных внутренних классов в Java мы объявляем и создаем их в одно и то же время.
Как правило, они используются всякий раз, когда Вам необходимо переопределить метод класса или интерфейса.

Синтаксис анонимного внутреннего класса в Java выглядит следующим образом:

```java
class Test {
    public static void main(String args[]) {
        AnonymousClass an_inner = new AnonymousClass() {
            public void my_method() {
        
            }   
        };
    }
}

```

Следующая программа показывает, как переопределить метод класса с использованием анонимного внутреннего класса

```java
abstract class AnonymousClass {
   public abstract void myMethod();
}

public class Outer_class {
   public static void main(String args[]) {
      AnonymousClass anonClass = new AnonymousClass() {
         public void myMethod() {
            System.out.println("Это пример анонимного внутреннего класса");
         }
      };
      anonClass.mymethod();	
   }
}
```

Точно так же можно переопределить методы конкретного класса, а также интерфейса,
используя анонимный внутренний класс.

---

### Анонимный внутренний класс как аргумент

Как правило, если метод принимает объект интерфейса, абстрактный класс или конкретный класс,
то мы можем реализовать интерфейс, расширить абстрактный класс и передать объект методу.
Если это класс, мы можем напрямую передать его методу.

Но во всех трех случаях Вы можете в Java передать анонимный внутренний класс методу.
Синтаксис передачи анонимного внутреннего класса в качестве аргумента метода:

```java
obj.myMethod(new MyClass() {
    public void doSomething() {

    }
});
```

Пример:

```java
// Интерфейс
interface Message {
   String greet();
}

public class MyClass {
   // Метод, который принимает объект интерфейса Message
   public void displayMessage(Message m) {
      System.out.println(m.greet() + ", это пример анонимного внутреннего класса в качестве аргумента");  
   }

   public static void main(String args[]) {
      // Создание класса
      MyClass obj = new MyClass();

      // Передача анонимного внутреннего класса в качестве аргумента
      obj.displayMessage(new Message() {
         public String greet() {
            return "Привет";
         }
      });
   }
}
```

---

### [Назад к оглавлению](./README.md)