# Управление объектами в ORM: Запросы

## Введение

В объектно-реляционном отображении (ORM) объекты программного обеспечения могут быть привязаны к записям в базе данных, что позволяет управлять данными в базе с использованием объектно-ориентированного подхода. Одним из ключевых аспектов работы с ORM является выполнение запросов к базе данных для извлечения, изменения или удаления данных. В данном разделе мы рассмотрим как ORM обеспечивает управление запросами.

## Запросы в ORM

### Основные операции

1. **Выполнение пользовательских SQL-запросов**

    - ORM позволяет разработчикам выполнять пользовательские SQL-запросы напрямую через фреймворк ORM.
    - Это предоставляет гибкость для выполнения сложных операций с базой данных, которые не покрываются стандартными методами CRUD.

### Пример в Java

```java
import javax.persistence.EntityManager;
import javax.persistence.Query;
import javax.persistence.Persistence;

public class Main {
    public static void main(String[] args) {
        EntityManager entityManager = Persistence.createEntityManagerFactory("your-persistence-unit").createEntityManager();

        // Пример выполнения SQL-запроса через ORM
        Query query = entityManager.createNativeQuery("SELECT * FROM users WHERE age > :age", User.class);
        query.setParameter("age", 18);
        List<User> users = query.getResultList();

        for (User user : users) {
            System.out.println(user.getName());
        }
    }
}
```

## Дополнительные аспекты запросов в ORM
### Использование JPA Criteria API
**Построение запросов программным путем**

- JPA Criteria API предоставляет возможность строить запросы к базе данных программным путем, используя объектно-ориентированный подход.
- Это позволяет создавать запросы без написания явного SQL, что делает код более гибким и понятным.

#### Пример:
```java
import javax.persistence.EntityManager;
import javax.persistence.criteria.CriteriaBuilder;
import javax.persistence.criteria.CriteriaQuery;
import javax.persistence.criteria.Root;
import javax.persistence.Persistence;
import java.util.List;

public class Main {
public static void main(String[] args) {
EntityManager entityManager = Persistence.createEntityManagerFactory("your-persistence-unit").createEntityManager();
CriteriaBuilder criteriaBuilder = entityManager.getCriteriaBuilder();
CriteriaQuery<User> criteriaQuery = criteriaBuilder.createQuery(User.class);
Root<User> root = criteriaQuery.from(User.class);
criteriaQuery.select(root).where(criteriaBuilder.gt(root.get("age"), 18));
List<User> users = entityManager.createQuery(criteriaQuery).getResultList();

        for (User user : users) {
            System.out.println(user.getName());
        }
    }
}
```