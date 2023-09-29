# Вопросы и задания по теме [переменные, типы переменных, объявление и инициализация](./variables.md)

Дан код.
- Какое количество переменных в данном коде?
- какие из переменных являются `локальные`/`экземпляра класса`/`константами`?
- в какой момент выполнения программы будет проинициализирована переменная `lastResult`?

```java
public class Calculator {

    public static final double PI = 3.14;

    private static final String LABEL = "Площадь круга равна с радиусом ";

    double lastResult;

    int add(int a, int b) {
        return a + b;
    }

    int minus(int a, int b) {
        int c = a - b;
        lastResult = c;
        return c;
    }

    int multiply(int a, int b) {
        int multiply = a * b;
        lastResult = multiply;
        return multiply;
    }

    int divide(int a, int b) {
        return a / b;
    }

    double areaOfCircle(double radius) {
        double result = PI * radius * radius;
        lastResult = result;
        return result;
    }

    public static void main(String[] args) {
        int r;
        Calculator calculator = new Calculator();
        r = 5;
        double s = calculator.areaOfCircle(r);
        calculator.add(5, 9);
        int divide = calculator.divide(4, 5);

        System.out.println(LABEL + r + " равна " + s);
    }
}
```

---

### [Назад к оглавлению](./README.md)