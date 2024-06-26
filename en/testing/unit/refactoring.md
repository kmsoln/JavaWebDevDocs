## Рефакторинг в контексте юнит-тестирования в Java

Рефакторинг кода в Java — это процесс изменения внутренней структуры программы, не затрагивая её функциональности, с целью улучшения понимания кода, уменьшения его сложности или улучшения производительности. В контексте юнит-тестирования, рефакторинг может помочь сделать код более тестируемым, улучшить читаемость тестов и обеспечить лучшее покрытие тестами.

### Важность рефакторинга при юнит-тестировании

- **Улучшение тестируемости кода:** Рефакторинг может выявить скрытые зависимости и сложные для тестирования участки кода, что позволяет их изолировать или упростить.

- **Повышение читаемости тестов:** Хорошо структурированные и читаемые тесты упрощают поддержку и расширение тестового покрытия в будущем.

- **Обеспечение надёжности приложения:** Рефакторинг с активным использованием тестов обеспечивает, что изменения в коде не влияют на его функциональность.

### Шаги рефакторинга в юнит-тестировании

1. **Оценка тестируемости кода:** Анализируйте код на предмет зависимостей, которые затрудняют тестирование, например, тесно связанные компоненты.

2. **Написание или обновление тестов:** Перед изменением кода убедитесь, что для него написаны соответствующие юнит-тесты, которые полностью покрывают его функциональность.

3. **Проведение рефакторинга:** Вносите изменения в код, стараясь не влиять на его функциональность. Регулярно запускайте тесты, чтобы убедиться, что изменения не привели к регрессии.

4. **Повторная оценка и доработка тестов:** После рефакторинга возможно потребуется обновить тесты, чтобы они отражали изменения в коде.

### Примеры рефакторинга для улучшения тестируемости кода

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

// Рефакторинг с целью упрощения тестирования
public class Calculator {
    private final Logger logger;

    public Calculator(Logger logger) {
        this.logger = logger;
    }

    public int add(int a, int b) {
        int result = a + b;
        logger.log("Adding " + a + " + " + b + " = " + result);
        return result;
    }
}

// Тест после рефакторинга
public class CalculatorTests {
    @Test
    public void testAdd() {
        Logger mockLogger = mock(Logger.class);
        Calculator calc = new Calculator(mockLogger);
        assertEquals(5, calc.add(2, 3));
        verify(mockLogger).log("Adding 2 + 3 = 5");
    }
}
```

