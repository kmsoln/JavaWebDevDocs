# Аннотации @Embeddable и @Embedded

Аннотация `@Embedded` используется для определения встраиваемого объекта, который будет сохранен в той же таблице, что и Entity класс.

Пример использования аннотации `@Embedded`:

```java
@Embeddable
public class Address {
    private String street;
    private String city;
    private String zipCode;
    
    // Геттеры и сеттеры
}

@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    
    @Embedded
    private Address address;
    
    // Другие поля и методы
}
```

В этом примере класс `Address` аннотирован как `@Embeddable`, что указывает JPA на то, что это встраиваемый объект. Поле `address` в классе `User` аннотировано как `@Embedded`, что указывает Hibernate на то, что это поле должно быть сохранено в той же таблице, что и Entity класс.

Hibernate создаст таблицу `users` следующим образом:

```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    street VARCHAR(255),
    city VARCHAR(255),
    zip_code VARCHAR(10)
);
```

Как видим, самого объекта `Address` в таблице не будет, вместо этого его поля будут встроены в таблицу `users`.

# [**Назад**: *Список аннотаций*](entity.md)