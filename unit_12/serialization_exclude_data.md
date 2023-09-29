# Исключение данных из сериализации

По умолчанию сериализуются все переменные объекта.
Допустим, мы хотим, чтобы некоторые поля были исключены из сериализации.
Для этого они должны быть объявлены с модификатором **transient**.

К примеру, исключим из сериализации объекта **Person** переменные `height` и `male`

---

# Сохранение и восстановление из файла списка объектов

```java
class Person implements Serializable{
      
    private String name;
    private int age;
    private transient double height;
    private transient boolean male;
      
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

### [Назад к оглавлению](./README.md)