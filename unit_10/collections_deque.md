# Очереди. Интерфейс Deque

Интерфейс `Deque` расширяет вышеописанный интерфейс `Queue` и определяет поведение двунаправленной очереди,
которая работает как обычная однонаправленная очередь, либо как стек, действующий по принципу **LIFO** (последний вошел - первый вышел).

Интерфейс Deque определяет следующие методы:

-   `void addFirst(E obj)` добавляет элемент в начало очереди
-   `void addLast(E obj)` добавляет элемент **obj** в конец очереди
-   `E getFirst()` возвращает без удаления элемент из головы очереди.
    Если очередь пуста, генерирует исключение **NoSuchElementException**
-   `E getLast()` возвращает без удаления последний элемент очереди.
    Если очередь пуста, генерирует исключение **NoSuchElementException**
-   `boolean offerFirst(E obj)` добавляет элемент **obj** в самое начало очереди.
    Если элемент удачно добавлен, возвращает **true**, иначе - **false**
-   `boolean offerLast(E obj)` добавляет элемент obj в конец очереди.
    Если элемент удачно добавлен, возвращает **true**, иначе - **false**
-   `E peekFirst()` возвращает без удаления элемент из начала очереди.
    Если очередь пуста, возвращает значение **null**
-   `E peekLast()` возвращает без удаления последний элемент очереди.
    Если очередь пуста, возвращает значение **null**
-   `E pollFirst()` возвращает с удалением элемент из начала очереди.
    Если очередь пуста, возвращает значение **null**
-   `E pollLast()` возвращает с удалением последний элемент очереди.
    Если очередь пуста, возвращает значение **null**
-   `E pop()` возвращает с удалением элемент из начала очереди.
    Если очередь пуста, генерирует исключение **NoSuchElementException**
-   `void push(E element)` добавляет элемент в самое начало очереди
-   `E removeFirst()` возвращает с удалением элемент из начала очереди.
    Если очередь пуста, генерирует исключение **NoSuchElementException**
-   `E removeLast()` возвращает с удалением элемент из конца очереди.
    Если очередь пуста, генерирует исключение **NoSuchElementException**
-   `boolean removeFirstOccurrence(Object obj)` удаляет первый встреченный элемент **obj** из очереди.
    Если удаление произшло, то возвращает **true**, иначе возвращает **false**.
-   `boolean removeLastOccurrence(Object obj)` удаляет последний встреченный элемент **obj** из очереди.
    Если удаление произшло, то возвращает **true**, иначе возвращает **false**.

Таким образом, наличие методов **pop()** и **push()** позволяет классам, реализующим этот элемент, действовать в качестве стека.
В тоже время имеющийся функционал также позволяет создавать двунаправленные очереди,
что делает классы, применяющие данный интерфейс, довольно гибкими.

---

### [Назад к оглавлению](./README.md)
