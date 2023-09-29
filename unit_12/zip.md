# Работа с ZIP-архивами

Кроме общего функционала для работы с файлами Java предоставляет функциональность для работы с таким видом файлов как zip-архивы.
Для этого в пакете `java.util.zip` определены два класса - `ZipInputStream` и `ZipOutputStream`

---

### ZipOutputStream. Запись архивов

Для создания архива используется класс **ZipOutputStream**.
Для создания объекта **ZipOutputStream** в его конструктор передается поток вывода:

```java
ZipOutputStream(OutputStream out)
```

Для записи файлов в архив для каждого файла создается объект **ZipEntry**,
в конструктор которого передается имя архивируемого файла.
А чтобы добавить каждый объект **ZipEntry** в архив, применяется метод `putNextEntry()`.

Пример создания архива:

```java
import java.io.*;
import java.util.zip.*;
  
public class Program {
  
    public static void main(String[] args) {
        try(ZipOutputStream zout = new ZipOutputStream(new FileOutputStream("file.zip"));
                FileInputStream fis= new FileInputStream("file.txt")) {
            ZipEntry entry = new ZipEntry("file.txt");
            zout.putNextEntry(entry);
            // содержимое файла в массив byte
            byte[] buffer = new byte[fis.available()];
            fis.read(buffer);
            // добавление содержимого
            zout.write(buffer);
            // закрытие записи
            zout.closeEntry();
        } catch(Exception ex) {
            System.out.println(ex.getMessage());
        } 
    } 
}
```

После добавления объекта **ZipEntry** в поток нам также надо добавить в него и содержимое файла.
Для этого используется метод write, записывающий в поток массив байтов: `zout.write(buffer);`.
В конце надо закрыть **ZipEntry** с помощью метода `closeEntry()`.
После этого можно добавлять в архив новые файлы - все вышеописанные действия для каждого нового файла повторяются.

---

### Чтение архивов. ZipInputStream

Для чтения архивов применяется класс **ZipInputStream**. 
В конструкторе он принимает поток, указывающий на zip-архив:

```java
ZipInputStream(InputStream in)
```

Для считывания файлов из архива **ZipInputStream** использует метод `getNextEntry()`,
который возвращает объект **ZipEntry**.
Объект **ZipEntry** представляет отдельную запись в zip-архиве. 

Пример чтения архива:

```java
import java.io.*;
import java.util.zip.*;
  
public class Program {
    public static void main(String[] args) {
        try(FileInputStream fileInputStream = new FileInputStream("output.zip");
                ZipInputStream zipInputStream = new ZipInputStream(fileInputStream)) {
            for (ZipEntry entry = zipInputStream.getNextEntry(); entry != null; entry = zipInputStream.getNextEntry()) {
                // название файла
                String name = entry.getName(); 
                // размер в байтах
                long size=entry.getSize();  
                System.out.printf("File name: %s \t File size: %d \n", name, size);
                 
                // распаковка
                FileOutputStream fileOutputStream = new FileOutputStream("new_" + name);
                for (int c = zipInputStream.read(); c != -1; c = zipInputStream.read()) {
                    fileOutputStream.write(c);
                }
                fileOutputStream.flush();
                zipInputStream.closeEntry();
                fileOutputStream.close();
            }
        } catch(Exception ex) {
            System.out.println(ex.getMessage());
        } 
    } 
}
```

**ZipInputStream** в конструкторе получает ссылку на поток ввода.
И затем в цикле выводятся все файлы и их размер в байтах, которые находятся в данном архиве.
Затем данные извлекаются из архива и сохраняются в новые файлы,
которые находятся в той же папке и начинаются с `new_`.

---

### [Назад к оглавлению](./README.md)