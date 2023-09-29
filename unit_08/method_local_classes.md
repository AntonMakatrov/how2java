# Локальные внутренние классы (method local classes)

В Java возможно написание класса внутри метода - это и есть локальный тип.
Как и локальные переменные, возможности внутреннего класса ограничены в рамках метода.

Локальный метод внутреннего класса может быть создан только внутри метода, где определяется внутренний класс.

Пример программы, показывающий как использовать локальный внутренний класс

```java
public class OuterClass {

    // Метод экземпляра внешнего класса
    void myMethod() {
        int num = 888;

        // Локальный внутренний класс 
        class MethodInner_Demo {
            public void print() {
                System.out.println("Это метод внутреннего класса: " + num);	   
            }   
        }
        // Конец внутреннего класса
        	   
        // Доступ к локальному внутреннему классу
        MethodInner_Demo inner = new MethodInner_Demo();
        inner.print();
    }
    
    public static void main(String args[]) {
        OuterClass outer = new OuterClass();
        outer.myMethod();	   	   
    }
}
```

---

### [Назад к оглавлению](./README.md)