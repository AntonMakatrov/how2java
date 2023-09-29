# Тернарный оператор ?:

Тернарный оператор `?:` используется для замены оператора `if-else`.

Синтаксис:

```java
Exp1 ? Exp2 : Exp3;
```

Чтобы определить значение всего выражения, сперва нужно оценить `Exp1`:

- Если значение `Exp1` верно (**true**), то значение `Exp2` будет значением всего выражения
- Если значение `Exp1` ложно (**false**), то вычисляется `Exp3` и его значение становится значением всего выражения

Пример:

```java
public class Test {

    public static void main(String args[]) {
        int x = 30;
        System.out.print(x > 30 ? "x > 30" : "x <= 30");
    }
}
```

---

### [Назад к оглавлению](./README.md)