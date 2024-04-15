# Аннотация @ManyToMany

Аннотация `@ManyToMany` используется для определения многие-ко-многим отношения между двумя Entity классами. Отношение многие-ко-многим означает, что одна запись в таблице может быть связана с несколькими записями в другой таблице и наоборот.

Для примера, давайте создадим два Entity класса `Author` и `Book`, которые будут иметь многие-ко-многим отношение друг с другом.

```java
@Entity
@Table(name = "authors")
public class Author {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    
    @ManyToMany
    @JoinTable(
        name = "author_book",
        joinColumns = @JoinColumn(name = "author_id"),
        inverseJoinColumns = @JoinColumn(name = "book_id")
    )
    private List<Book> books;
    
    // Геттеры и сеттеры
}
```

```java
@Entity
@Table(name = "books")
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String title;
    
    @ManyToMany(mappedBy = "books")
    private List<Author> authors;
    
    // Геттеры и сеттеры
}
```

В этом примере класс `Author` имеет поле `books`, которое аннотировано как `@ManyToMany`. Это означает, что у автора может быть много книг. При этом, в таблице `authors` не будет внешнего ключа на таблицу `books`.

Класс `Book` имеет поле `authors`, которое аннотировано как `@ManyToMany(mappedBy = "books")`. Это означает, что у книги может быть много авторов. При этом, в таблице `books` не будет внешнего ключа на таблицу `authors`.

Связь между таблицами укажет Hibernate на то, что в таблице `author_book` будет столбец `author_id`, к которому будет привязан внешний ключ на таблицу `authors`, и столбец `book_id`, к которому будет привязан внешний ключ на таблицу `books`.

SQL запрос, который Hibernate выполнит для создания таблиц, будет выглядеть следующим образом:

```sql
CREATE TABLE authors (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL
);

CREATE TABLE books (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL
);

CREATE TABLE author_book (
    author_id BIGINT,
    book_id BIGINT,
    FOREIGN KEY (author_id) REFERENCES authors(id),
    FOREIGN KEY (book_id) REFERENCES books(id)
);
```

Таким образом, аннотация `@ManyToMany` позволяет определить многие-ко-многим отношение между двумя Entity классами и настроить таблицу, которая будет хранить связи между ними.

# [**Назад**: *Список аннотаций*](entity.md)