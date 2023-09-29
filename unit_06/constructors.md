# Конструктор класса

При обсуждении вопроса класса, одной из наиболее важных подтем в Java является конструктор.

Каждый класс имеет конструктор.

**Конструкторы** - это специальные методы, которые вызывается при создании объекта.
Они имеют такое же название, как и класс.
Они создают новый объект определенного класса.

Если мы не напишем его или, например, забудем, компилятор создаст его по умолчанию для этого класса.

Каждый раз, когда в Java создается новый объект, будет вызываться по меньшей мере один конструктор.
Главное правило является то, что они должны иметь то же имя, что и класс, который может иметь более одного конструктора.

Примеры конструктора:

```java
public class Puppy {
    public Puppy() {
        // пустой конструктор
    }

    public Puppy(String name) {
        // конструктор c параметром name
    }
}
```

---

### Виды конструкторов

Существуют два вида конструкторов - явные и неявные.
Если ничего не прописать в коде класса, все равно можно "сконструировать" объект этого класса.

---

### Какие преимущества дает явное прописывание конструктора?

Появляется возможность регулировать, какие параметры и в каком количестве нужно задать для создания объекта определенного класса

```java
public class Test {
    public static void main(String[] args) {
        Puppy puppy = new Puppy();
        Scanner scanner = new Scanner(System.in);
        Puppy sparky = new Puppy("Sparky");
    }
}
```

Меньше строчек кода и улучшение читабельности класса

```java
public class Dog {

    private Sting name;
    private int age;

    public Dog() {
    }

    public Dog(Sting name, int age) {
        this.name = name;
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.setAge(3);
        dog.setName("Rusty");
        
        Dog dog2 = new Dog("Persey", 2);
    }
}
```

---

### [Назад к оглавлению](./README.md)