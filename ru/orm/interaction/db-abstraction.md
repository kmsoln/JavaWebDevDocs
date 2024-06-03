# Абстракции базы данных в ORM

Database Abstraction - это концепция, используемая в объектно-реляционном отображении (ORM), которая предоставляет уровень абстракции над базой данных, позволяя разработчикам взаимодействовать с ней, используя объектно-ориентированные конструкции.

## Основные принципы Database Abstraction в ORM:

1. **Уровень абстракции**: ORM предоставляет разработчикам высокоуровневый интерфейс для работы с базой данных, скрывая сложности написания SQL-запросов.

2. **Объектно-ориентированный подход**: Разработчики могут оперировать базой данных, используя объекты и методы, что делает код более понятным и поддерживаемым.

3. **Сокрытие деталей реализации**: ORM скрывает от разработчика детали реализации базы данных, такие как тип используемой СУБД и специфичные для нее особенности.

## Примеры использования Database Abstraction в ORM (на примере Java):

### Создание сущности:

```java
@Entity
public class User {
    @Id
    private Long id;
    private String username;
    private String email;
    // Геттеры и сеттеры
}
```
### Взаимодействие с базой данных:
```java
public class Main {
    public static void main(String[] args) {
        EntityManagerFactory entityManagerFactory = Persistence.createEntityManagerFactory("example-unit");
        EntityManager entityManager = entityManagerFactory.createEntityManager();

        // Начало транзакции
        entityManager.getTransaction().begin();

        // Создание нового пользователя
        User user = new User();
        user.setId(1L);
        user.setUsername("example_user");
        user.setEmail("user@example.com");

        // Сохранение пользователя в базе данных
        entityManager.persist(user);

        // Завершение транзакции
        entityManager.getTransaction().commit();

        // Закрытие EntityManager
        entityManager.close();
        entityManagerFactory.close();
    }
}

```

В приведенном примере ORM абстрагирует базу данных и позволяет создавать и сохранять объекты User без написания SQL-запросов.

### Преимущества Database Abstraction в ORM:
- #### Упрощение разработки: ORM позволяет разработчикам работать с базой данных на уровне объектов, что упрощает процесс разработки и поддержки приложений.

- #### Повышение безопасности: ORM предотвращает SQL-инъекции и другие уязвимости, связанные с неправильным формированием SQL-запросов.

- #### Поддержка кросс-платформенности: ORM позволяет писать приложения, которые могут работать с различными СУБД без изменения кода.

## [К оглавлению](../references.md)