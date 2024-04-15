# Аннотация @OneToOne

Аннотация `@OneToOne` используется для определения один-к-одному отношения между двумя Entity классами. Однако, в отличие от `@OneToMany` и `@ManyToOne`, `@OneToOne` не требует наличия внешнего ключа в одной из таблиц. Вместо этого, одна из таблиц содержит ссылку на другую таблицу.

Давайте рассмотрим пример сущности `Review` и сущности `User`. Предположим, что у нас есть отзыв, который может быть оставлен только одним пользователем. В этом случае, мы можем использовать аннотацию `@OneToOne` для определения отношения между этими двумя сущностями:

```java
@Entity
@Table(name = "reviews")
public class Review {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(name = "review_text", length = 1000, nullable = false)
    private String text;
    
    @OneToOne
    private User user;
    
    // Другие поля и методы
}
```

В этом примере поле `user` аннотировано как `@OneToOne`, что указывает JPA на то, что это поле содержит один-к-одному отношение с сущностью `User`. При этом, в таблице `reviews` не будет внешнего ключа на таблицу `users`.

Связь между таблицами укажет Hibernate на то, что в таблице `reviews` будет столбец, к которому будет привязан внешний ключ на таблицу `users`. При этом это никак не затронет таблицу `users`.

SQL запрос, который Hibernate выполнит для создания таблицы, будет выглядеть следующим образом:

```sql
CREATE TABLE reviews (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    review_text VARCHAR(1000) NOT NULL,
    user_id BIGINT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

# [**Назад**: *Список аннотаций*](entity.md)