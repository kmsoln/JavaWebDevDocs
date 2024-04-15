# Аннотация @OneToMany

Аннотация `@OneToMany` используется для определения один-ко-многим отношения между двумя Entity классами. Это означает, что один объект Entity может иметь много связанных объектов Entity. Например, один пользователь может иметь много отзывов.

Давайте рассмотрим пример сущностей `Product`, которая будет связана с сущностью `Review` из предыдущего примера. Одна сущность `Product` может иметь много отзывов, поэтому мы можем использовать аннотацию `@OneToMany` для определения этого отношения:

```java
@Entity
@Table(name = "products")
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(name = "product_name", nullable = false)
    private String name;
    
    @OneToMany
    private List<Review> reviews;
    
    // Другие поля и методы
}
```

В этом примере поле `reviews` аннотировано как `@OneToMany`, что указывает JPA на то, что это поле содержит один-ко-многим отношение с сущностью `Review`. При этом, в таблице `products` не будет внешнего ключа на таблицу `reviews`.

Связь между таблицами укажет Hibernate на то, что в таблице `reviews` будет столбец, к которому будет привязан внешний ключ на таблицу `products`.

По сути сейчас этот Entity класс описывает таблицу, которую на языке запросов SQL можно создать следующим образом:

```sql
CREATE TABLE products (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(255) NOT NULL
);

CREATE TABLE reviews (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    review_text VARCHAR(1000) NOT NULL,
    product_id BIGINT,
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

Кстати говоря, Hibernate будет использовать как раз примерно такие запросы для создания таблиц, просто будет строить их самостоятельно на основе описания Entity классов.

# [**Назад**: *Список аннотаций*](entity.md)


