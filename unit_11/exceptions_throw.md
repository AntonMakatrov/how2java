# Оператор throw

Чтобы сообщить о выполнении исключительных ситуаций в программе, можно использовать оператор `throw`.
То есть с помощью этого оператора мы сами можем создать исключение и вызвать его в процессе выполнения.
Например, после ввода числа нужно чтобы число было меньше 50

```java
 
import java.util.Scanner;
public class FirstApp {
 
    public static void main(String[] args) {
        try {
            Scanner in = new Scanner(System.in);
            int x = in.nextInt();
            if(x >= 50){
               throw new Exception("Number must be less than 50");
           }
        } catch(Exception ex) {
            System.out.println(ex.getMessage());
        }
    }   
}
```

Здесь для создания объекта исключения используется конструктор класса `Exception`, в который передается сообщение об исключении.
И если число х окажется больше 49, то будет выброшено исключение и управление перейдет к блоку `catch`.

В блоке `catch` мы можем получить сообщение об исключении с помощью метода `getMessage()`.

---

### [Назад к оглавлению](./README.md)