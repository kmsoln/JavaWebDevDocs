# Фреймворки для ORM

## Популярные фреймворки для ORM

### 1. Hibernate

**Описание:**
Hibernate - один из наиболее известных и широко используемых фреймворков ORM для языка Java. Он предоставляет мощные инструменты для отображения объектов на таблицы базы данных и автоматического выполнения операций CRUD.

**Пример использования:**
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String username;
    private String email;
    // Getters and setters
}

// Использование Hibernate для сохранения пользователя в базу данных
Session session = HibernateUtil.getSessionFactory().openSession();
Transaction transaction = session.beginTransaction();

User user = new User();
user.setUsername("JohnDoe");
user.setEmail("john@example.com");

session.save(user);

transaction.commit();
session.close();
```

### 2. Spring Data JPA
**Описание:**
Spring Data JPA - это часть Spring Framework, которая облегчает работу с базами данных, используя JPA (Java Persistence API) в сочетании с Spring.

**Пример использования:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
}

// Использование Spring Data JPA для сохранения пользователя в базу данных
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    @Transactional
    public void saveUser(User user) {
        userRepository.save(user);
    }
}

```

### 3. MyBatis
   **Описание:**
   MyBatis - это фреймворк ORM, который позволяет разработчикам писать SQL-запросы в XML или аннотациях Java, обеспечивая гибкость и контроль над SQL.

**Пример использования:**
```java
@Mapper
public interface UserMapper {
    @Insert("INSERT INTO users (username, email) VALUES (#{username}, #{email})")
    void insert(User user);
}

    // Использование MyBatis для сохранения пользователя в базу данных
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(Resources.getResourceAsStream("mybatis-config.xml"));
try (SqlSession session = sqlSessionFactory.openSession()) {
        UserMapper userMapper = session.getMapper(UserMapper.class);
        User user = new User();
        user.setUsername("JohnDoe");
        user.setEmail("john@example.com");
        userMapper.insert(user);
        session.commit();
        }

```
## [К оглавлению](references.md)