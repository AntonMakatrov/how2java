# Ссылки на методы. Ссылки на конструкторы

### Ссылки на метод как параметры методов

Начиная с JDK 8 в Java можно в качестве параметра в метод передавать ссылку на другой метод.
В принципе данный способ аналогичен передаче в метод лямбда-выражения.

Ссылка на метод передается в виде `имя_класса::имя_статического_метода` (если метод статический) или 
`объект_класса::имя_метода` (если метод нестатический). Рассмотрим на примере:

```java
interface Expression {
    boolean isEqual(int n);
}

class ExpressionHelper {

    static boolean isEven(int n) {
        return n % 2 == 0;
    }

    static boolean isPositive(int n) {
        return n > 0;
    }
}
public class LambdaApp {
 
    public static void main(String[] args) {
        int[] nums = { -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5};
        System.out.println(sum(nums, ExpressionHelper::isEven));
        
        Expression e = ExpressionHelper::isPositive;
        System.out.println(sum(nums, e));
    } 

    private static int sum (int[] numbers, Expression func) {
        int result = 0;
        for(int i : numbers) {
            if (func.isEqual(i)) {
                result += i;
            }
        }
        return result;
    }
}
```

Определен функциональный интерфейс `Expression`, который имеет один метод и
класс `ExpressionHelper`, который содержит два статических метода.
Их можно было определить и в основном классе программы.

В основном классе программы LambdaApp определен метод sum(),
который возвращает сумму элементов массива, соответствующих некоторому условию.
Условие передается в виде объекта функционального интерфейса Expression.

В методе main два раза вызываем метод sum, передавая в него один и тот же массив чисел, но разные условия.

При первом вызове метода _sum_ на место второго параметра передается `ExpressionHelper::isEven`,
то есть ссылка на статический метод isEven() класса ExpressionHelper.
При этом методы, на которые идет ссылка, должны совпадать по параметрам и результату с методом функционального интерфейса.

При втором вызове метода _sum_ отдельно создается объект Expression, который затем передается в метод.
Использование ссылок на методы в качестве параметром аналогично использованию лямбда-выражений.

Если нам надо вызвать нестатические методы, то в ссылке вместо имени класса применяется имя объекта этого класса

```java
interface Expression {
    boolean isEqual(int n);
}
 
class ExpressionHelper {
     
    boolean isEven(int n) {
        return n % 2 == 0;
    }
}
public class LambdaApp {
 
    public static void main(String[] args) {
        int[] nums = { -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5 };
        ExpressionHelper exprHelper = new ExpressionHelper();
        System.out.println(sum(nums, exprHelper::isEven));
    } 
     
    private static int sum (int[] numbers, Expression func) {
        int result = 0;
        for(int i : numbers) {
            if (func.isEven(i)) {
                result += i;
            }
        }
        return result;
    }
}
```

### Ссылки на конструкторы

Подобным образом мы можем использовать конструкторы: `название_класса::new`

```java
interface UserBuilder {
    User create(String name);
}

class User {
     
    private String name;

    String getName() {
        return name;
    }
     
    User(String name) {
        this.name = name;
    }
}

public class LambdaApp {
 
    public static void main(String[] args) {
        UserBuilder userBuilder = User::new;
        User user = userBuilder.create("Tom");
        System.out.println(user.getName());
    }
}
```

При использовании конструкторов методы функциональных интерфейсов должны принимать тот же список параметров,
что и конструкторы класса, и должны возвращать объект данного класса.

---

### [Назад к оглавлению](./README.md)