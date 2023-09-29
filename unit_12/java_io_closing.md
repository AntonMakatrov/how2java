# Закрытие потоков

При завершении работы с потоком его надо закрыть с помощью метода `close()`, который определен в интерфейсе **Closeable**. 
Метод `close()` имеет следующее определение:

```java
void close() throws IOException
```

Этот интерфейс уже реализуется в классах InputStream и OutputStream, а через них и во всех классах потоков.

При закрытии потока освобождаются все выделенные для него ресурсы, например, файл.
В случае, если поток окажется не закрыт, может происходить утечка памяти.

Есть два способа закрытия файла.
Первый традиционный заключается в использовании блока `try..catch..finally`.

```java
import java.io.*;
 
public class Program {
 
    public static void main(String[] args) {
         
        FileInputStream fin=null;
        try
        {
            fin = new FileInputStream("file.txt");
           
            int i=-1;
            while((i=fin.read())!=-1){
                System.out.print((char)i);
            }
        } catch(IOException ex) {
            System.out.println(ex.getMessage());
        } 
        finally{
            try{
                if(fin!=null) {
                    fin.close();
                } 
            } catch(IOException ex){
                System.out.println(ex.getMessage());
            }
        }  
    } 
}
```

Поскольку при открытии или считывании файла может произойти ошибка ввода-вывода, то код считывания помещается в блок **try**.
И чтобы быть уверенным, что поток в любом случае закроется,
даже если при работе с ним возникнет ошибка, вызов метода `close()` помещается в блок finally.
И, так как метод `close()` также в случае ошибки может генерировать исключение **IOException**,
то его вызов также помещается во вложенный блок `try..catch`

Начиная с Java 7 можно использовать еще один способ, который автоматически вызывает метод `close()`.
Этот способ заключается в использовании конструкции `try-with-resources` (try-с-ресурсами).
Данная конструкция работает с объектами, которые реализуют интерфейс **java.lang.AutoCloseable**.
Так как все классы потоков реализуют интерфейс **Closeable**, который в свою очередь наследуется от **AutoCloseable**,
то их также можно использовать в данной конструкции

Предыдущий пример с использованием конструкции `try-with-resources`:

```java
import java.io.*;
 
public class Program {
 
    public static void main(String[] args) {
        try(FileInputStream fin = new FileInputStream("file.txt")) {
            int i=-1;
            while((i=fin.read()) != -1){
                System.out.print((char)i);
            }   
        } catch(IOException ex){
            System.out.println(ex.getMessage());
        } 
    } 
}
```

Синтаксис конструкции:

```java
try(название_класса имя_переменной = конструктор_класса)
```

Данная конструкция также не исключает использования блоков **catch**.

После окончания работы в блоке **try** у ресурса (в данном случае у объекта **FileInputStream**) автоматически вызывается метод `close()`.

Если нам надо использовать несколько потоков, которые после выполнения надо закрыть, то мы можем указать объекты потоков через точку с запятой

```java
try(FileInputStream fin=new FileInputStream("file.txt"); 
      FileOutputStream fos = new FileOutputStream("new_filetxt")) {
    
}
```

---

### [Назад к оглавлению](./README.md)