## Тестирование обработки исключений (Exception Handling) в юнит-тестах на Java

Тестирование обработки исключений в Java помогает убедиться, что ваше приложение адекватно реагирует на ошибки и исключения. В юнит-тестах это особенно важно для проверки того, как код обрабатывает неожиданные ситуации.

### Основные концепции тестирования исключений в Java

- **Try-Catch Blocks:** Обычно исключения обрабатываются в блоках `try-catch`, где код в блоке `try` исполняется, а если возникает исключение, выполнение переходит к соответствующему блоку `catch`.

- **Throwing Exceptions:** Исключения могут быть выброшены с помощью ключевого слова `throw`, что позволяет передавать ошибку выше по стеку вызовов.

### Использование JUnit для тестирования исключений

JUnit предоставляет несколько способов для тестирования исключений:

- **@Test (expected = Exception.class):** Этот параметр аннотации `@Test` позволяет указать, что во время теста ожидается определенное исключение.

- **try-catch idiom:** Традиционный подход с явным использованием блока `try-catch` внутри теста.

- **AssertThrows (JUnit 5):** JUnit 5 ввел метод `assertThrows`, который упрощает тестирование исключений и обеспечивает более чистый код.

### Примеры тестирования исключений в Java

#### Использование @Test (expected)

```java
import org.junit.Test;

public class ExceptionTest {

    @Test(expected = ArithmeticException.class)
    public void testDivisionWithException() {
        int result = 10 / 0; // This should throw ArithmeticException
    }
}
```
#### Использование try-catch idiom

```java
import org.junit.Test;
import static org.junit.Assert.fail;

public class ExceptionTest {

    @Test
    public void testDivisionWithException() {
        try {
            int result = 10 / 0;
            fail("Expected an ArithmeticException to be thrown");
        } catch (ArithmeticException e) {
            // Test passes here
        }
    }
}

```
#### Использование AssertThrows (JUnit 5)

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertThrows;

public class ExceptionTest {

    @Test
    public void testDivisionWithException() {
        assertThrows(ArithmeticException.class, () -> {
            int result = 10 / 0; // This should throw ArithmeticException
        });
    }
}
```


