# Сериализация

**Сериализация** представляет процесс записи состояния объекта в поток,
соответственно процесс извлечения или восстановления состояния объекта из потока называется **десериализацией**.
Сериализация очень удобна, когда идет работа со сложными объектами.

---

### Интерфейс Serializable

Сериализовать можно только те объекты, которые реализуют интерфейс `Serializable`.
Этот интерфейс не определяет никаких методов, просто он служит указателем системе,
что объект, реализующий его, может быть сериализован

---

### Сериализация. Класс ObjectOutputStream

Для сериализации объектов в поток используется класс **ObjectOutputStream**.
Он записывает данные в поток.

Для создания объекта **ObjectOutputStream** в конструктор передается поток, в который производится запись:

```java
	
ObjectOutputStream(OutputStream out)
```

Для записи данных **ObjectOutputStream** использует ряд методов, среди которых можно выделить следующие:

- `void close()` закрывает поток
- `void flush()` очищает буфер и сбрасывает его содержимое в выходной поток
- `void write(byte[] buf)` записывает в поток массив байтов 
- `void write(int val)` записывает в поток один младший байт из **val**
- `void writeBoolean(boolean val)` записывает в поток значение **boolean**
- `void writeByte(int val)` записывает в поток один младший байт из **val**
- `void writeChar(int val)` записывает в поток значение типа **char**, представленное целочисленным значением
- `void writeDouble(double val)` записывает в поток значение типа **double**
- `void writeFloat(float val)` записывает в поток значение типа **float**
- `void writeInt(int val)` записывает целочисленное значение **int**
- `void writeLong(long val)` записывает значение типа **long**
- `void writeShort(int val)` записывает значение типа **short**
- `void writeUTF(String str)` записывает в поток строку в кодировке **UTF-8**
- `void writeObject(Object obj)` записывает в поток отдельный объект

Эти методы охватывают весь спектр данных, которые можно сериализовать.

Пример сохранения в файл одиного объекта класса **Person**

```java
import java.io.*;
 
public class Program {
 
    public static void main(String[] args) {
         
        try(ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.dat"))) {
            Person p = new Person("Denis", 33, 178, true);
            oos.writeObject(p);
        } catch(Exception ex) {
            System.out.println(ex.getMessage());
        } 
    } 
}

class Person implements Serializable{
      
    private String name;
    private int age;
    private double height;
    private boolean male;
      
    Person(String name, int age, double height, boolean male){
        this.name = name;
        this.age = age;
        this.height = height;
        this.male = male;
    }

    String getName() {
        return name;
    }

    int getAge() {
        return age;
    }

    double getHeight() {
        return height;
    }

    boolean isMale() { 
        return male;
    }
}
```

---

### Десериализация. Класс ObjectInputStream

Класс **ObjectInputStream** отвечает за обратный процесс - чтение ранее сериализованных данных из потока.
В конструкторе он принимает ссылку на поток ввода

```java
ObjectInputStream(InputStream in)
```

Функционал **ObjectInputStream** сосредоточен в методах, предназначенных для чтения различных типов данных.
Рассмотрим основные методы этого класса:

- `void close()` закрывает поток
- `int skipBytes(int len)` пропускает при чтении несколько байт, количество которых равно **len**
- `int available()` возвращает количество байт, доступных для чтения
- `int read()` считывает из потока один байт и возвращает его целочисленное представление
- `boolean readBoolean()` считывает из потока одно значение **boolean**
- `byte readByte()` считывает из потока один байт
- `char readChar()` считывает из потока один символ **char**
- `double readDouble()` считывает значение типа **double**
- `float readFloat()` считывает из потока значение типа **float**
- `int readInt()` считывает целочисленное значение **int**
- `long readLong()` считывает значение типа **long**
- `short readShort()` считывает значение типа **short**
- `String readUTF()` считывает строку в кодировке **UTF-8**
- `Object readObject()` считывает из потока объект

Пример извлечения из файла выше сохраненного класса **Person**

```java
import java.io.*;
 
public class Program {
 
    public static void main(String[] args) {
        try(ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.dat"))) {
            Person p=(Person)ois.readObject();
            System.out.printf("Name: %s \t Age: %d \n", p.getName(), p.getAge());
        } catch(Exception ex) {
            System.out.println(ex.getMessage());
        }
    } 
}
```

---

### [Назад к оглавлению](./README.md)