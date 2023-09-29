# Буферизация символьных потоков. Классы BufferedWriter и BufferedReader

---

### Запись текста через буфер и BufferedWriter

Класс `BufferedWriter` записывает текст в поток, предварительно буферизируя записываемые символы,
тем самым снижая количество обращений к физическому носителю для записи данных.

Конструкторы класса **BufferedWriter**:

```java
BufferedWriter(Writer out) 
BufferedWriter(Writer out, int sz)
```

В качестве параметра он принимает поток вывода, в который надо осуществить запись. Второй параметр указывает на размер буфера.

Пример записи в файл

```java
import java.io.*;
 
public class Program {
  
    public static void main(String[] args) {
        try(BufferedWriter bw = new BufferedWriter(new FileWriter("file.txt"))) {
            String text = "Hello World!\nHello guys! We are learning IO.";
            bw.write(text);
        } catch(IOException ex) {
            System.out.println(ex.getMessage());
        } 
    } 
}
```

---

### Чтение текста и BufferedReader

Класс `BufferedReader` считывает текст из символьного потока ввода, буферизируя прочитанные символы.
Использование буфера призвано увеличить производительность чтения данных из потока.

Конструкторы класса **BufferedReader**:

```java
BufferedReader(Reader in) 
BufferedReader(Reader in, int sz) 
```

Второй конструктор, кроме потока ввода, из которого производится чтение,
также определяет размер буфера, в который будут считываться символы.

Так как **BufferedReader** наследуется от класса **Reader**,
то он может использовать все те методы для чтения из потока, которые определены в **Reader**.
И также **BufferedReader** определяет свой собственный метод `readLine()`, который позволяет считывать из потока построчно.

Пример использования **BufferedReader** с посимвольным чтением

```java
import java.io.*;
 
public class Program {
    public static void main(String[] args) {
        try(BufferedReader br = new BufferedReader (new FileReader("file.txt"))) {
           // чтение посимвольно
            int c;
            while((c=br.read())!=-1) {
                System.out.print((char)c);
            }
        } catch(IOException ex) {
            System.out.println(ex.getMessage());
        } 
    } 
}
```

Пример использования **BufferedReader** с построчным чтением

```java
import java.io.*;
 
public class Program {
    public static void main(String[] args) {
        try(BufferedReader br = new BufferedReader (new FileReader("file.txt"))) {
            //чтение построчно
            String s;
            while((s=br.readLine()) != null) {
                System.out.println(s);
            }
        } catch(IOException ex) {
            System.out.println(ex.getMessage());
        } 
    } 
}
```

---

### Считывание с консоли в файл

Для считывания с консоли в файл будет использовать оба класса BufferedReader и BufferedWriter.

```java
import java.io.*;
 
public class Program {
 
    public static void main(String[] args) {
         
        try(BufferedReader br = new BufferedReader (new InputStreamReader(System.in)); 
                BufferedWriter bw = new BufferedWriter(new FileWriter("file.txt"))) {
           // чтение построчно
            String text;
            while(!(text=br.readLine()).equals("quit")){
                  
                bw.write(text + "\n");
                bw.flush();
            }
        }
        catch(IOException ex){
              
            System.out.println(ex.getMessage());
        } 
    }   
}
```

Здесь объект **BufferedReader** устанавливается для чтения с консоли с помощью объекта `new InputStreamReader(System.in)`.
В цикле **while** считывается введенный текст.
И пока пользователь не введет строку `quit`, объект **BufferedWriter** будет записывать текст файл.

---

### [Назад к оглавлению](./README.md)