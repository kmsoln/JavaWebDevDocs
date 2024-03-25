# Цепочка вызовов

Термин `method chaining` означает, что при вызове метода, он возвращает после своего выполнения объект, который его вызвал. Это позволяет вызывать методы один за другим, что упрощает настройку.

Например, вспомним такой код из [Урока про конфиг Spring Security](../springsecurity/password_auth/authentication-setup.md):

```java
http
    .authorizeHttpRequests(
        (auth) -> auth.anyRequest().permitAll()
    )
    .httpBasic(withDefaults())
    .formLogin(configurer -> {
        configurer
            .loginPage("/login")
            .permitAll()
            .successHandler((request, response, authentication) -> {
                response.sendRedirect("success?message=You logged in successfully!");
            })
            .failureHandler(((request, response, exception) -> {
                response.sendRedirect("problem?message=Wrong login or password");
            }));
    })
    .authenticationProvider(authenticationProvider());
```

В нашем коде, мы сначала вызываем метод `authorizeHttpRequests`, который на свое место возвращает тот же самый объект `http`, который его вызвал и мы можем сразу же вызвать другой нужный нам метод, что мы и делаем, вызывая метод `httpBasic`.

При желании, мы могли бы переставить все эти методы местами и это не было бы проблемой, потому что все эти методы принадлежат одному объекту `http`.

Такой подход позволяет нам настраивать Spring Security очень просто и наглядно.

Рассмотрим еще один пример. Напишем класс для настройки объекта `Person`, используя `method chaining`:

```java
public class Person {
    private String name;
    private int age;
    private String city;

    public Person name(String name) {
        this.name = name;
        return this;
    }

    public Person age(int age) {
        this.age = age;
        return this;
    }

    public Person city(String city) {
        this.city = city;
        return this;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", city='" + city + '\'' +
                '}';
    }

    public static void main(String[] args) {
        Person person = new Person()
            .name("John")
            .age(25)
            .city("New York");

        System.out.println(person);
    }
}
```

Как видишь у нашего класса три поля `name`, `age` и `city`, и три метода `name`, `age` и `city`, которые возвращают объект `Person`. Таким образом, мы можем вызывать эти методы один за другим, что делает код более читаемым и понятным.

Это мы и делаем в методе `main`, где создаем объект `Person` и сразу же вызываем методы `name`, `age` и `city`, чтобы задать значения полям объекта.

Такой подход, по сути, позволяет нам выполнять сложные действия `в одну строку`, что упрощает и уменьшает код, делая его более понятным.