Операции сведения. Методы findFirst и findAny

Метод `findFirst()` извлекает из потока первый элемент,
а `findAny()` извлекает случайный объект из потока (нередко так же первый)

```java
ArrayList<String> names = new ArrayList<String>();
names.addAll(Arrays.asList(new String[]{"Tom", "Sam", "Bob", "Alice"}));
 
Optional<String> first = names.stream()
    .findFirst();
System.out.println(first.get());    // Tom
 
Optional<String> any = names.stream()
    .findAny();
System.out.println(first.get());    // Tom
```

---

### [Назад к оглавлению](../../README.md)