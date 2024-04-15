# Аннотация @EmbeddedId

Аннотация `@EmbeddedId` используется для определения составного первичного ключа. Составной первичный ключ состоит из нескольких полей, которые вместе образуют первичный ключ. Эти поля могут быть примитивными типами, встраиваемыми объектами или их комбинацией.

Пример использования `@EmbeddedId`:

```java
@Embeddable
public class UserId implements Serializable {
    private Long departmentId;
    private Long employeeId;
    
    // Геттеры и сеттеры
}

@Entity
@Table(name = "users")
public class User {
    @EmbeddedId
    private UserId id;
    
    private String name;
    
    // Другие поля и методы
}
```

В этом примере класс `UserId` аннотирован как `@Embeddable`, что указывает JPA на то, что это встраиваемый объект. Поле `id` в классе `User` аннотировано как `@EmbeddedId`, что указывает Hibernate на то, что это поле является составным первичным ключом.

Hibernate создаст таблицу `users` следующим образом:

```sql
CREATE TABLE users (
    department_id BIGINT,
    employee_id BIGINT,
    name VARCHAR(255) NOT NULL,
    PRIMARY KEY (department_id, employee_id)
);
```

Как видим, в таблице `users` будет составной первичный ключ, который будет состоять из полей `department_id` и `employee_id`.

# [**Назад**: *Список аннотаций*](entity.md)