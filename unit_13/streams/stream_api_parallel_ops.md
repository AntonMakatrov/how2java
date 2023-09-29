# Параллельные операции над массивами
   
В JDK 8 к классу Arrays было добавлено ряд методов, которые позволяют в параллельном режиме совершать обработку элементов массива.
И хотя данные методы формально не входят в Stream API, но реализуют схожую функциональность, что и параллельные потоки:

-   `parallelPrefix()` вычисляет некоторое значение для элементов массива (например, сумму элементов)
-   `parallelSetAll()` устанавливает элементы массива с помощью лямбда-выражения
-   `parallelSort()` сортирует массив

Воспользуемся методом `parallelSetAll()` для установки элементов массива

```java
import java.util.Arrays;

public class Program {
 
    public static void main(String[] args) {
        int[] numbers = initializeArray(6);
        for(int i: numbers) {
            System.out.println(i);
        }
    } 

    public static int[] initializeArray(int size) {
        int[] values = new int[size];
        Arrays.parallelSetAll(values, i -> i * 10);
        return values;
    }
}
```

В метод `Arrays.parallelSetAll()` передается два параметра: изменяемый массив и функция, которая устанавливает элементы массива.
Эта функция перебирает все элементы и в качестве параметра получает индекс текущего перебираемого элемента.
Выражение `i -> i * 10` означает, что по каждому индексу в массиве будет хранится число, равное `i * 10`. 

Рассмотрим более сложный пример. Произведем манипуляции с массивом объектов Phone

```java
class Phone{
     
    private String name;
    private int price;
     
    public Phone(String name, int price) {
        this.name = name;
        this.price = price;
    }
     
    public String getName() {
        return name;
    }
    public void setName(String val) {
        this.name=val;
    }
    public int getPrice() {
        return price;
    }
    public void setPrice(int val) {
        this.price=val;
    }
}

class PhoneTest {

    public static void main(String[] args) {
        Phone[] phones = new Phone[]{new Phone("iPhone", 74000), 
            new Phone("Pixel", 53000),
            new Phone("Samsung Galaxy", 41000),
            new Phone("Nokia", 22000)};
                 
        Arrays.parallelSetAll(phones, i -> {
            phones[i].setPrice(phones[i].getPrice() - 5000); 
            return phones[i];
        });
                 
        for(Phone p: phones) {
            System.out.printf("%s - %d \n", p.getName(), p.getPrice());
        }
    }
}
```

Лямбда-выражение в методе `Arrays.parallelSetAll` представляет блок кода.
И так как лямбда-выражение должно возвращать объект, то нам надо явным образом использовать оператор **return**.
В этом лямбда-выражении опять же функция получает индексы перебираемых элементов,
и по этим индексам мы можем обратиться к элементам массива и их изменить.

---

### Сортировка

Отсортируем массив чисел в параллельном режиме:

```java
int[] nums = {30, -4, 5, 29, 7, -8};
Arrays.parallelSort(nums);
for(int i: nums) {
    System.out.println(i);
}
```

Метод `Arrays.parallelSort()` в качестве параметра принимает массив и сортирует его по возрастанию:

Если же нам надо как-то по-другому отсортировать объекты, например, по модулю числа, или у нас более сложные объекты,
то мы можем создать свой компаратор и передать его в качестве второго параметра в `Arrays.parallelSort()`.

Возьмем выше определенный класс Phone и создадим для него компаратор

```java
import java.util.Arrays;
import java.util.Comparator;

public class Program {
  
    public static void main(String[] args) {
          
        Phone[] phones = new Phone[] {
            new Phone("iPhone", 9400), 
            new Phone("Pixel", 6500),
            new Phone("Samsung Galaxy", 5000),
            new Phone("Nokia", 3200)
        };
         
        Arrays.parallelSort(phones,new PhoneComparator());
        for(Phone p: phones) {
            System.out.println(p.getName());
        }
    }
}

class PhoneComparator implements Comparator<Phone> {
  
    public int compare(Phone a, Phone b){
        return a.getName().toUpperCase().compareTo(b.getName().toUpperCase());
    }
}
```

---

### Метод parallelPrefix

Метод `parallelPrefix()` походит для тех случаев, когда надо получить элемент массива или объект того же типа,
что и элементы массива, который обладает некоторыми признаками.
Например, в массиве чисел это может быть максимальное, минимальное значения и т.д. 

Найдем произведение чисел:

```java
int[] numbers = {1, 2, 3, 4, 5, 6};
Arrays.parallelPrefix(numbers, (x, y) -> x * y);

for(int i: numbers) {
    System.out.println(i);
}
```

Результат:

```
1
2
6
24
120
720
```

Лямбда-выражение из `Arrays.parallelPrefix()`, которое представляет бинарную функцию,
получает два элемента и выполняет над ними операцию.
Результат операции сохраняется и передается в следующий вызов бинарной функции.

---

### [Назад к оглавлению](../README.md)