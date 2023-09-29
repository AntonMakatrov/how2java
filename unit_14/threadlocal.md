# Внутрипоточные переменные(ThreadLocal)

Если надо сохранить один экземпляр переменной для всех экземпляров класса, можно использовать статические переменные класса.
Если надо сохранить экземпляр переменной для каждого потока, можно использовать внутрипоточные переменные (**ThreadLocal**).
**ThreadLocal** переменные отличаются от обычных переменных тем,
что у каждого потока свой собственный, индивидуально инициализируемый экземпляр переменной,
доступ к которой он получает через методы `get()` или `set()`.

Предположим, вы разрабатываете многопоточный трассировщик кода,
чьей целью является однозначное определение пути каждого потока через ваш код.
Проблема в том, что вам необходимо скоординировать несколько методов в нескольких классах через несколько потоков.
Без **ThreadLocal** это было бы трудноразрешимо.
Когда поток начинал бы выполняться, было бы необходимо сгенерировать уникальный маркер для идентификации его трассировщиком,
а потом передавать этот маркер каждому методу при трассировке.

С **ThreadLocal** это проще.
Поток инициализирует **ThreadLocal** переменную в начале выполнения,
а затем обращается к нему из каждого метода в каждом классе,
и переменная при этом будет хранить трассировочную информацию только для исполняемого в данный момент времени потока.
Когда его выполнение завершится, поток может передать свою индивидуальную запись о трассировке объекту управления,
ответственному за поддержание всех записей.

Использование **ThreadLocal** имеет смысл, когда вам необходимо хранить экземпляры переменной для каждого потока.

Пример использования **ThreadLocal** - доказательство того,
что каждый поток имеет свою собственную копию переменной **ThreadLocal**

```java
import java.text.SimpleDateFormat;
import java.util.Random;

public class ThreadLocalExample implements Runnable {

    // SimpleDateFormat is not thread-safe, so give one to each thread
    private static final ThreadLocal<SimpleDateFormat> formatter = new ThreadLocal<SimpleDateFormat>() {
        @Override
        protected SimpleDateFormat initialValue() {
            return new SimpleDateFormat("yyyyMMdd HHmm");
        }
    };
    
    public static void main(String[] args) throws InterruptedException {
        ThreadLocalExample obj = new ThreadLocalExample();
        for(int i=0 ; i<10; i++) {
            Thread t = new Thread(obj, "" + i);
            Thread.sleep(new Random().nextInt(1000));
            t.start();
        }
    }

    @Override
    public void run() {
        System.out.println("Thread Name= " + Thread.currentThread().getName() + " default; Formatter = " + formatter.get().toPattern());
        try {
            Thread.sleep(new Random().nextInt(1000));
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        formatter.set(new SimpleDateFormat());
        System.out.println("Thread Name= " + Thread.currentThread().getName()+"; Formatter = " + formatter.get().toPattern());
    }

}
```

---

### Реализация потокобезопсного контеста пользователя серверного API

```java
public class SecurityContextHolder {
	
	private static final ThreadLocal<User> threadLocalUser = new ThreadLocal<>();
	
	public static User getLoggedUser() {
		return threadLocalScope.get();
	}
	
	public static void setLoggedUser(User user) {
		threadLocalScope.set(user);
	}   
}
```

---

### [Назад к оглавлению](./README.md)