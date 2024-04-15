# Аннотация @JoinColumn

Аннотация `@JoinColumn` используется для определения столбца, который будет использоваться для ассоциации между Entity классами. Эта аннотация используется вместе с аннотациями `@OneToOne`, `@OneToMany`, `@ManyToOne` и `@ManyToMany`.

Давайте рассмотрим пример сущности `Review` и сущности `User`. Предположим, что у нас есть отзыв, который может быть оставлен несколькими пользователями. В этом случае, мы можем использовать аннотацию `@ManyToOne` для определения отношения между этими двумя сущностями:

```java
@Entity
@Table(name = "reviews")
public class Review {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "review_text", length = 1000, nullable = false)
    private String text;

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;

    // Другие поля и методы
}

@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "user_name", nullable = false)
    private String name;

    // Другие поля и методы
}
```

В этом примере поле `user` аннотировано как `@ManyToOne`, что указывает JPA на то, что это поле содержит многие-к-одному отношение с сущностью `User`. При этом, в таблице `reviews` будет столбец `user_id`, к которому будет привязан внешний ключ на таблицу `users`.

SQL запрос, который Hibernate выполнит для создания таблиц, будет выглядеть следующим образом:

```sql
CREATE TABLE reviews (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    review_text VARCHAR(1000) NOT NULL,
    user_id BIGINT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_name VARCHAR(255) NOT NULL
);
```

# [**Назад**: *Список аннотаций*](entity.md)