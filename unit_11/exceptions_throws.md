# Оператор throws

Иногда метод, в котором может генерироваться исключение, сам не обрабатывает это исключение.
В этом случае в объявлении метода используется оператор `throws`, который надо обработать при вызове этого метода.
Например, у нас имеется метод вычисления факториала, и нам надо обработать ситуацию, если в метод передается число меньше 1:

```java
public static int getFactorial(int num) throws Exception {
     
    if(num < 1) {
        throw new Exception("The number is less than 1");
    }
    int result = 1;
    for(int i = 1; i <= num; i++) {
        result*=i;
    }
    return result;
}
```

С помощью оператора `throw` по условию выбрасывается исключение.
В то же время метод сам это исключение не обрабатывает с помощью `try..catch`,
поэтому в определении метода используется выражение `throws Exception`.

Теперь при вызове этого метода нам обязательно надо обработать выбрасываемое исключение:

```java

public static void main(String[] args) {
         
    try {
        int result = getFactorial(-6);
        System.out.println(result);
    } catch(Exception ex) {
        System.out.println(ex.getMessage());
    }
} 
```

Без обработки исключение возникнет ошибка компиляции, и нельзя будет скомпилировать программу.

В качестве альтернативы можно и не использовать оператор `throws`, а обработать исключение прямо в методе

```java
public static int getFactorial(int num){
    int result=1;
    try {
        if(num < 1) {
            throw new Exception("The number is less than 1");
        } 
        for(int i = 1; i <= num; i++) {
            result*=i;
        }
    } catch(Exception e) {
        System.out.println(e.getMessage());
        result = num;
    }
    return result;
}
```

---

### [Назад к оглавлению](./README.md)