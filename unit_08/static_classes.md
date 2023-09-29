#### Статические вложенные классы (static nested classes)

**Статический вложенный класс** — это вложенный класс, который является статическим членом внешнего класса.
Доступ к нему возможен без создания экземпляра внешнего класса с использованием других статических элементов.
Как и статические члены, статический вложенный класс не имеет доступа к переменным экземпляра и методам внешнего класса.

Синтаксис статического вложенного класса выглядит следующим образом:

```java
class MyClass {
   static class StaticNestedClass {

   }
}
```

Создание экземпляра статического вложенного класса немного отличается от экземпляра внутреннего класса.

```java
public class Outer {
    
    static class StaticNestedClass {
        public void myMethod() {
            System.out.println("Это мой вложенный класс");
        }
    }
    
    public static void main(String args[]) {
        Outer.StaticNestedClass nested = new Outer.StaticNestedClass();	 
        nested.myMethod();
    }
}
```

---

### [Назад к оглавлению](./README.md)