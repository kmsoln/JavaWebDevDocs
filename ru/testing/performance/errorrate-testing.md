## Тестирование частоты ошибок (Error Rate Testing) в Java

Тестирование частоты ошибок (Error Rate Testing) является частью нагруженного тестирования, которое направлено на оценку стабильности и надежности приложения путем измерения частоты возникновения ошибок в процессе его выполнения.

### Основные аспекты тестирования частоты ошибок

- **Определение критериев:** Определите, какие типы ошибок будут учитываться во время тестирования, например, ошибки времени выполнения, исключения, сбои системы.

- **Мониторинг и логирование:** Важно обеспечить адекватный мониторинг и логирование приложения, чтобы точно отслеживать и записывать все возникающие ошибки.

- **Анализ частоты ошибок:** После сбора данных ошибках необходимо анализировать их частоту и контекст, чтобы определить узкие места и возможные точки улучшения.

### Инструменты и библиотеки для тестирования частоты ошибок в Java

- **JUnit и AssertJ:** Используйте библиотеки JUnit для написания тестов и AssertJ для более выразительных утверждений, включая проверку исключений.

- **Log4j или SLF4J:** Используйте библиотеки логирования, такие как Log4j или SLF4J, для записи ошибок и другой важной информации во время выполнения тестов.

### Пример теста частоты ошибок в Java

```java
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ExpectedException;
import static org.junit.Assert.*;

public class ErrorRateTest {

    @Rule
    public ExpectedException thrown = ExpectedException.none();

    @Test
    public void testMethodThatThrowsRuntimeException() {
        thrown.expect(RuntimeException.class);
        thrown.expectMessage("Expected Exception");

        methodThatThrowsRuntimeException();
    }

    private void methodThatThrowsRuntimeException() {
        throw new RuntimeException("Expected Exception");
    }

    @Test
    public void testErrorFrequency() {
        int errorCount = 0;
        int attempts = 1000;

        for (int i = 0; i < attempts; i++) {
            try {
                // Пример метода, который может вызвать ошибку
                methodThatMayFail();
            } catch (Exception e) {
                errorCount++;
            }
        }

        double errorRate = (double) errorCount / attempts;
        assertTrue("Error rate too high", errorRate <= 0.1);
    }

    private void methodThatMayFail() {
        if (Math.random() < 0.05) { // 5% вероятность ошибки
            throw new RuntimeException("Random Failure");
        }
    }
}
```

