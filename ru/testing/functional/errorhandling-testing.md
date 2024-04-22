## Тестирование обработки ошибок в Java

Тестирование обработки ошибок — важный аспект функционального тестирования, который направлен на проверку того, как система реагирует на исключительные или нештатные ситуации. В Java это обычно включает проверку правильности работы исключений и механизмов обработки ошибок.

### Основные концепции тестирования обработки ошибок

- **Исключения (Exceptions):** В Java исключения используются для обработки ошибок во время выполнения программы. Исключения могут быть проверяемыми (checked) и непроверяемыми (unchecked).

- **Проверка исключений:** Тестирование должно включать проверку того, корректно ли генерируются и обрабатываются исключения в предполагаемых условиях.

### Применение тестирования обработки ошибок

- **Тестирование с использованием JUnit:** JUnit предлагает возможности для тестирования исключений через аннотацию `@Test` с параметром `expected`, который позволяет указать ожидаемый тип исключения.

- **Try-Catch блоки:** В тестах можно использовать try-catch блоки для более детальной проверки свойств исключений, таких как сообщения об ошибках.

### Примеры тестирования обработки ошибок в Java

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class ErrorHandlingTests {

    @Test(expected = IllegalArgumentException.class)
    public void testForException() {
        MyClass myClass = new MyClass();
        myClass.methodThatShouldThrow(-1);
    }

    @Test
    public void testExceptionMessage() {
        try {
            MyClass myClass = new MyClass();
            myClass.methodThatShouldThrow(-1);
            fail("IllegalArgumentException expected");
        } catch (IllegalArgumentException e) {
            assertEquals("Negative value provided", e.getMessage());
        }
    }
}

class MyClass {
    public void methodThatShouldThrow(int value) {
        if (value < 0) {
            throw new IllegalArgumentException("Negative value provided");
        }
    }
}
```

