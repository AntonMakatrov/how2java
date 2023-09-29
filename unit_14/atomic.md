# Атомарные корректоры полей

При увеличении или уменьшении значения примитива в многопоточной среде гораздо выгоднее использовать
один из новых атомарных классов из пакета `java.util.concurrent.atomic`, чем писать свой собственный синхронизированный блок кода.
Атомарные классы гарантируют выполнение определенных операций, таких как увеличение и уменьшение,
обновление или добавление значения, потокобезопасным способом.
В перечень атомарных классов входят классы **AtomicInteger**, **AtomicBoolean**, **AtomicLong**, **AtomicIntegerArray** и т.п.

Проблема использования атомарных классов состоит в том, что все операции класса,
включая `get()`, `set()` и семейство операций **get-set**, оказываются атомарными.
Это означает, что операции **read** и **write**, которые не изменяют значения атомарной переменной, ―
это не просто важные, а синхронизированные операции read-update-write.
Если требуется более детальное управление развертыванием синхронизированного кода,
то обходной путь заключается в использовании атомарного корректора полей.

---

### Использование атомарных обновлений

Атомарные корректоры полей, такие как **AtomicIntegerFieldUpdater**, **AtomicLongFieldUpdater** и **AtomicReferenceFieldUpdater**,
по сути, представляют собой оболочку **volatile**-поля.
Они используются внутри библиотек Java-классов.
Эти корректоры не нашли широкого применения в коде приложений, но избегать их нет никаких причин.

Пример класса, использующего атомарные корректоры для изменения названия книги

```java
import java.util.concurrent.atomic.AtomicReferenceFieldUpdater;

public class BookTest {
    private volatile Book currentBook;
 
    private static final AtomicReferenceFieldUpdater<BookTest,Book> updater =
            AtomicReferenceFieldUpdater.newUpdater(BookTest.class, Book.class, "currentBook");
 
    public Book getCurrentBook() {
        return currentBook;
    }
 
    public void setCurrentBook(Book currentBook) {
        updater.compareAndSet(this, this.currentBook, currentBook); //this.currentBook = currentBook;
    }
}

class Book {
    private String name;
    public Book() { }
    public Book(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
```

Класс BookTest предоставляет свое свойство currentBook обычным образом, с помощью методов `get()` и `set()`,
но метод `set()` делает нечто особенное.
Вместо того чтобы просто присвоить свою внутреннюю ссылку **Book** указанному объекту **Book**, он использует AtomicReferenceFieldUpdater.

---

### AtomicReferenceFieldUpdater

В Javadoc класс **AtomicReferenceFieldUpdater** определяется следующим образом:

Основанная на отражении _reflection-based_ утилита, которая обеспечивает атомарное обновление указанных опорных **volatile**-полей указанных классов.
Этот класс предназначен для использования в атомарных структурах данных, где несколько опорных полей одного и того же узла независимо подлежат атомарному обновлению.
Класс AtomicReferenceFieldUpdater создается с помощью вызова его статического метода `newUpdater()`, принимающего три параметра:

-   класс объекта, содержащий поле (BookTest.class)
-   класс объекта, подлежащий атомарному обновлению (Book.class)
-   имя поля, подлежащего атомарному обновлению

Реальная выгода здесь заключается в том, что метод `getCurrentBook()` выполняется без всякой синхронизации,
в то время как `setCurrentBook()` выполняется как атомарная операция.

---

### [Назад к оглавлению](./README.md)