# Сохранение и восстановление из файла списка объектов

```java
import java.io.*;
import java.util.ArrayList;
  
public class Program {
     
    public static void main(String[] args) {
         
        String filename = "people.dat";
        // создадим список объектов, которые будем записывать
        ArrayList<Person> people = new ArrayList<>();
        people.add(new Person("Tom", 30, 175, false));
        people.add(new Person("Frodo", 33, 178, true));
          
        try(ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(filename))) {
            oos.writeObject(people);
            System.out.println("Saved to file.");
        } catch(Exception ex) {
            System.out.println(ex.getMessage());
        } 
          
        // десериализация в новый список
        ArrayList<Person> newPeople= new ArrayList<Person>();
        try(ObjectInputStream ois = new ObjectInputStream(new FileInputStream(filename))) {
            newPeople=((ArrayList<Person>)ois.readObject());
        } catch(Exception ex){
            System.out.println(ex.getMessage());
        } 

        for(Person p : newPeople) {
            System.out.printf("Name: %s \t Age: %d \n", p.getName(), p.getAge());
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

### [Назад к оглавлению](./README.md)
