## Параметризованное тестирование в Java

Параметризованное тестирование в Java позволяет выполнять один и тот же тест с различными наборами данных, что повышает эффективность и область покрытия тестирования. Это особенно полезно при проверке функций с разными входными значениями.

### Основные концепции параметризованного тестирования

- **Параметризованные тесты:** В Java параметризованные тесты могут быть реализованы с помощью JUnit. Эти тесты позволяют задать исходные данные и ожидаемые результаты в виде коллекции объектов.

- **Использование аннотаций:** JUnit предоставляет аннотации, такие как `@RunWith` и `@Parameters`, для определения параметризованных тестов.

### Применение параметризованного тестирования в Java

- **JUnit Framework:** Версия JUnit 4 предоставляет поддержку параметризованных тестов с помощью аннотации `@RunWith(Parameterized.class)`.

- **JUnit 5:** В JUnit 5 параметризация достигается с помощью `@ParameterizedTest` вместе с источниками аргументов, такими как `@ValueSource`, `@MethodSource`, `@CsvSource` и др.

### Примеры использования параметризованного тестирования в Java

#### Пример с JUnit 4

```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;
import java.util.Arrays;
import java.util.Collection;

@RunWith(Parameterized.class)
public class ParameterizedTestExample {

    private int input;
    private int expected;

    public ParameterizedTestExample(int input, int expected) {
        this.input = input;
        this.expected = expected;
    }

    @Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
            { 1, 2 },
            { 2, 3 },
            { 3, 4 },
            { 4, 5 }
        });
    }

    @Test
    public void testAddOne() {
        assertEquals(expected, input + 1);
    }
}
```
### Пример с JUnit 5
```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.ValueSource;

public class ParameterizedTestExampleJUnit5 {

    @ParameterizedTest
    @ValueSource(ints = { 1, 2, 3, 4 })
    public void testAddOneJUnit5(int input) {
        assertEquals(input + 1, 2);
    }
}

```

