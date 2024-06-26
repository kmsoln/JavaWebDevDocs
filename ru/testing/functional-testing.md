## Функциональное тестирование в Java

Функциональное тестирование в Java является критически важным этапом в разработке программного обеспечения, целью которого является проверка того, что разработанный код выполняет все заявленные функциональные требования.

### Основные концепции функционального тестирования

- **Основа на требованиях:** Функциональное тестирование основано на требованиях к программному продукту, каждая функция проверяется на соответствие задокументированным спецификациям.

- **Черный ящик:** Тестирование проводится на уровне "черного ящика", т.е. тесты разрабатываются с учетом только внешних спецификаций функций без доступа к внутреннему коду.

- **Автоматизация:** Для функционального тестирования широко используется автоматизация, позволяющая повторять тестовые сценарии при каждом изменении кода без дополнительных затрат времени на ручное тестирование.

### Инструменты для функционального тестирования в Java

- **JUnit:** Хотя JUnit традиционно используется для модульного тестирования, его также можно применять для функционального тестирования отдельных функций или модулей.

- **Selenium:** Для тестирования веб-приложений Selenium позволяет автоматизировать действия в браузере и проверять поведение веб-приложений в различных средах.

- **Cucumber:** Этот инструмент подходит для описания функциональности на языке, близком к естественному. Cucumber использует сценарии, написанные на Gherkin, что делает тесты понятными не только разработчикам, но и заинтересованным лицам не из технической сферы.

### Пример функционального теста на Java с использованием JUnit

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class CalculatorTests {

    @Test
    public void testAddition() {
        Calculator calc = new Calculator();
        assertEquals("Testing addition of two numbers", 10, calc.add(7, 3));
    }
    
    @Test
    public void testSubtraction() {
        Calculator calc = new Calculator();
        assertEquals("Testing subtraction of two numbers", 4, calc.subtract(10, 6));
    }
}

class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }
}
```
