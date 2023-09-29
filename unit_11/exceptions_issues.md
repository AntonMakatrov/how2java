# Вопросы и задания по теме [Exceptions](./exceptions_intro.md)

Что такое Exception?

---

Как обрабатываются исключения, объясните механизм обработки исключений.

---

В чем разница между error и exception?

---

Назовите типы исключений?

---

Можно ли написать только блок try без catch и finally блоков?

---

Дан код:

```java
try {
    printA();   // prints A
    printB();   // prints B
    printC();   // prints C
} catch (Exception e) { 

}
```

предположим ошибка произошла в блоке `printB()`. Что будет выведено на экран?

---

Выполняется ли блок `finally`, если блоки `try` или `catch` возвращают элемент управления?

---

Что такое перебрасывание исключения?

---

Какой класс является суперклассом для всех типов ошибок и исключений?

---

Какие комбинации блоков `try`, `catch` и `finally` допустимы?

---

### [Назад к оглавлению](./README.md)