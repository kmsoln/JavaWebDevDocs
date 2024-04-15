# Аннотация @Temporal

Аннотация `@Temporal` используется для определения типа данных для даты и времени. Она применяется к полям типа `java.util.Date` и `java.util.Calendar`.

Пример использования аннотации `@Temporal`:

```java

@Entity
@Table(name = "reviews")
public class Review {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Temporal(TemporalType.TIMESTAMP)
    private Date createdDate;
    
    // Другие поля и методы
}
```

В этом примере поле `createdDate` аннотировано как `@Temporal`, что указывает JPA на то, что это поле содержит дату и время. Аннотация `@Temporal` позволяет указать тип данных для даты и времени, такие как `DATE`, `TIME` или `TIMESTAMP`.

`@Temporal` аннотация может быть использована с полями типа `java.util.Date` и `java.util.Calendar`. Она позволяет более гибко настраивать поля в Entity классе для хранения даты и времени в базе данных.

SQL запрос, который Hibernate выполнит для создания таблицы, будет выглядеть примерно так:

```sql
CREATE TABLE reviews (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    created_date TIMESTAMP
);
```

Другие типы, которые поддерживает аннотация `@Temporal`:

- `TemporalType.DATE` - для хранения только даты.
- `TemporalType.TIME` - для хранения только времени.
- `TemporalType.TIMESTAMP` - для хранения даты и времени.
- `TemporalType.TIMESTAMP_WITH_TIMEZONE` - для хранения даты и времени с учетом часового пояса.
- `TemporalType.TIME_WITH_TIMEZONE` - для хранения времени с учетом часового пояса.

# [**Назад**: *Список аннотаций*](entity.md)