## Тестирование JDBC запросов в Java

Тестирование JDBC запросов в Java является важной частью разработки приложений, работающих с базами данных. Это помогает убедиться, что взаимодействие приложения с базой данных происходит корректно и эффективно.

### Основные концепции тестирования JDBC запросов

- **JDBC (Java Database Connectivity):** JDBC предоставляет Java-приложениям универсальный доступ к различным базам данных.

- **Тестирование соединений:** Включает проверку на способность приложения устанавливать и поддерживать соединение с базой данных.

- **Тестирование запросов:** Оценка корректности SQL запросов, их выполнения, а также правильности получаемых результатов.

- **Изоляция тестов:** Важно изолировать тесты от реальной базы данных, используя мокирование или тестовые базы данных.

### Подходы к тестированию JDBC запросов

1. **Использование H2 Database:**
    - Многие разработчики используют встроенную H2 базу данных для тестирования JDBC кода, поскольку она легко интегрируется в тестовую среду и не требует отдельного сервера базы данных.

2. **Mockito или другие библиотеки для мокирования:**
    - Мокирование объектов JDBC, таких как `Connection`, `Statement`, и `ResultSet`, может помочь изолировать тесты от реальной базы данных и сделать их более предсказуемыми.

### Пример теста JDBC запроса с использованием H2

```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;
import java.sql.*;

public class JdbcTesting {
    private Connection connection;

    @Before
    public void setUp() throws Exception {
        // Создаем соединение с H2 базой данных
        connection = DriverManager.getConnection("jdbc:h2:mem:testdb", "sa", "");
        // Инициализируем базу данных
        Statement stmt = connection.createStatement();
        stmt.execute("CREATE TABLE users (id INT PRIMARY KEY, name VARCHAR(255))");
        stmt.execute("INSERT INTO users (id, name) VALUES (1, 'John Doe')");
    }

    @Test
    public void testUserFetch() throws SQLException {
        Statement stmt = connection.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT name FROM users WHERE id = 1");
        assertTrue("Must have at least one row", rs.next());
        assertEquals("John Doe", rs.getString("name"));
        assertFalse("Must have no more than one row", rs.next());
    }

    @After
    public void tearDown() throws Exception {
        connection.close();
    }
}
```

