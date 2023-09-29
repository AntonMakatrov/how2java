# Singleton

Паттерн **Singleton** гарантирует, что у класса есть только один экземпляр, и предоставляет к нему глобальную точку доступа

---

### Область применения

-   В системе должно существовать не более одного экземпляра заданного класса
-   Экземпляр должен быть легко доступен для всех клиентов данного класса
-   Создание объекта on demand, то есть, когда он понадобится первый раз, а не во время инициализации системы.

---

### Реализация

Существует несколько вариантов реализации со своими недостатками и преимуществами.


```java
class Singleton {
    
    private static Singleton instance;
    
    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

```java
class Singleton {
    
    private static Singleton instance;

    private Singleton() {
    }

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

```java
class Singleton {

    private static volatile Singleton instance;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

---

### [Назад к оглавлению](./README.md)