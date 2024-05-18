## Тестирование с использованием библиотеки JUnit в Java

JUnit является одной из наиболее популярных библиотек для написания и выполнения тестов в Java. Она предоставляет простой и эффективный фреймворк для разработки тестовых случаев и управления тестовыми данными.

### Основные возможности JUnit

- **Аннотации:** JUnit предоставляет различные аннотации для определения тестов, такие как `@Test`, `@Before`, `@After`, `@BeforeClass`, `@AfterClass`.
- **Утверждения (Assertions):** Библиотека включает набор функций утверждений, таких как `assertEquals()`, `assertTrue()`, `assertFalse()`, и `assertNotNull()` для проверки ожидаемых результатов.
- **Игнорирование тестов:** Аннотация `@Ignore` позволяет временно отключить выполнение некоторых тестов.
- **Тестирование исключений:** С помощью атрибута `expected` аннотации `@Test` можно проверить, что тест корректно генерирует ожидаемое исключение.

### Написание базового теста с использованием JUnit

Вот простой пример теста на JUnit, который проверяет функциональность сложения двух чисел:

```java
import static org.junit.Assert.*;
import org.junit.Test;

public class CalculatorTest {

    private Calculator calculator = new Calculator();

    @Test
    public void testAddition() {
        assertEquals("Error in addition", 5, calculator.add(2, 3));
    }
}
```
### Управление тестовым окружением
JUnit предоставляет аннотации @Before и @After для настройки и очистки тестового окружения перед и после каждого теста:
```java
import org.junit.*;

public class SetupTest {

    private Database database;

    @Before
    public void setUp() {
        database = new Database();
        database.connect();
    }

    @Test
    public void testConnection() {
        assertTrue(database.isConnected());
    }

    @After
    public void tearDown() {
        database.disconnect();
    }
}

```
### Параметризованные тесты
JUnit позволяет создавать параметризованные тесты, которые могут выполнять одни и те же тесты с различными входными данными:
```java
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.Test;
import static org.junit.Assert.assertEquals;
import java.util.Arrays;
import java.util.Collection;

@RunWith(Parameterized.class)
public class ParameterizedTest {

    private int input;
    private int expected;

    public ParameterizedTest(int input, int expected) {
        this.input = input;
        this.expected = expected;
    }

    @Parameterized.Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
                { 1, 1 }, { 2, 4 }, { 3, 9 }
        });
    }

    @Test
    public void testSquare() {
        assertEquals("Square calculation error", expected, input * input);
    }
}


```