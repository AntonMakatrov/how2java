# Пример инициализации класса с различными блоками

```java
public class ParentClass {

    static {
        System.out.println("Static block - Parent");
    }

    {
        System.out.println("Block 1 - Parent");
    }

    private int parentValue = initParentValue();
    private static int staticParentValue = initStaticParentValue();

    {
        System.out.println("Block 2 - Parent");
    }

    public ParentClass() {
        System.out.println("constructor - Parent");
    }

    private int initParentValue() {
        System.out.println("parentValue initialization");
        return 1;
    }

    private static int initStaticParentValue() {
        System.out.println("Static parentValue initialization");
        return 1;
    }
}
```

```java
public class ChildClass extends ParentClass {

    static {
        System.out.println("Static block - Child");
    }

    {
        System.out.println("Block 1 - Child");
    }

    private int childValue = initChildValue();
    private static int staticChildValue = initStaticChildValue();

    {
        System.out.println("Block 2 - Child");
    }

    public ChildClass() {
        System.out.println("constructor - Child");
    }

    private int initChildValue() {
        System.out.println("childValue initialization");
        return 1;
    }

    private static int initStaticChildValue() {
        System.out.println("Static childValue initialization");
        return 1;
    }
}
```

```java
public class TestRunner {
    public static void main(String[] args) {
        System.out.println("Start of main() method");
        new ChildClass();
        System.out.println("-----------------------");
        new ChildClass();
        System.out.println("End of main() method");
    }
}
```

Вывод в консоли:

```
Start of main() method
Static block - Parent
Static parentValue initialization
Static block - Child
Static childValue initialization
Block 1 - Parent
parentValue initialization
Block 2 - Parent
constructor - Parent
Block 1 - Child
childValue initialization
Block 2 - Child
constructor - Child
-----------------------
Block 1 - Parent
parentValue initialization
Block 2 - Parent
constructor - Parent
Block 1 - Child
childValue initialization
Block 2 - Child
constructor - Child
End of main() method
```

#

### [Назад к оглавлению](./README.md)