# Примеры использования [массивов](./arrays.md)

При работе с элементами массива часто используют цикл `for` или цикл `for-each`,
потому что все элементы имеют одинаковый тип и известный размер.

Давайте **создадим** массив, **проинициализируем**, найдем **сумму всех элементов** и **максимальное значение элемента**.

Пример:

```java
public class TestArray {

    public static void main(String[] args) {
        //создание и инициализация массива
        double[] myList = {1.9, 2.9, 3.4, 3.5};

        // Вывести на экран все элементы массива
        for (int i = 0; i < myList.length; i++) {
            System.out.print(myList[i] + " ");
        }
        System.out.println();

        // Сумма элементов массива
        double total = 0;
        for (int i = 0; i < myList.length; i++) {
            total += myList[i];
        }
        System.out.println("Sum: " + total);

        // Нахождение среди элементов массива наибольшего
        double max = myList[0];
        for (int i = 1; i < myList.length; i++) {
            if (myList[i] > max) {
                max = myList[i];
            }
        }
        System.out.println("Max. element: " + max);
    }
}
```

---

### [Назад к оглавлению](./README.md)