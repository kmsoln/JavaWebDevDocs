# Аннотация @Transient

Аннотация `@Transient` используется для пометки поля, которое не должно быть сохранено в базе данных. То есть при создании таблицы, Hibernate будет игнорировать это поле.

Пример использования аннотации `@Transient`:

```java
@Entity
@Table(name = "reviews")
public class Review {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(name = "review_text", length = 1000, nullable = false)
    private String text;
    
    @Transient
    private List<User> viewers;
    
    // Другие поля и методы
}
```

В этом примере поле `viewers` (пользователи которые сейчас просматривают отзыв) аннотировано как `@Transient`, что указывает JPA на то, что это поле не должно быть сохранено в базе данных. При создании таблицы `reviews`, Hibernate будет игнорировать это поле.

`@Transient` аннотация может быть использована для различных целей, например, для временных полей, которые не должны быть сохранены в базе данных, или для полей, которые должны быть вычислены динамически.

То есть, SQL запрос, который Hibernate создаст для создания таблицы, будет выглядеть следующим образом:

```sql
CREATE TABLE reviews (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    review_text VARCHAR(1000) NOT NULL
);
```

# [**Назад**: *Список аннотаций*](entity.md)