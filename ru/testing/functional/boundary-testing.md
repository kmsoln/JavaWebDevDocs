## Граничное тестирование (Boundary Testing) в Java

Граничное тестирование — это метод тестирования функциональности программы, который фокусируется на проверке поведения программы на границах допустимых входных значений. Этот тип тестирования особенно важен для выявления ошибок в обработке граничных условий, которые часто являются источником багов.

### Основные концепции граничного тестирования

- **Определение границ:** Граничные значения определяются для каждого входного параметра. Это могут быть минимальные и максимальные допустимые значения, а также значения, находящиеся сразу за этими границами.

- **Тестирование вокруг границ:** Тесты должны проверять не только значения на границах, но и значения непосредственно за ними, чтобы проверить реакцию системы на недопустимые входы.

- **Тестирование переполнений:** Важно проверять, как система обрабатывает случаи переполнений, например, когда вводимое значение превышает максимально возможное для данного типа данных.

### Примеры граничного тестирования в Java

Допустим, у нас есть функция, которая принимает возраст пользователя как целое число и возвращает `true`, если возраст находится в допустимом диапазоне от 18 до 65 лет. Мы напишем несколько тестовых случаев для проверки границ этого диапазона:

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class AgeValidatorTest {
    
    @Test
    public void testAgeAtLowerBoundary() {
        assertTrue("Age at lower boundary should be valid", AgeValidator.isValidAge(18));
    }

    @Test
    public void testAgeBelowLowerBoundary() {
        assertFalse("Age below lower boundary should be invalid", AgeValidator.isValidAge(17));
    }

    @Test
    public void testAgeAtUpperBoundary() {
        assertTrue("Age at upper boundary should be valid", AgeValidator.isValidAge(65));
    }

    @Test
    public void testAgeAboveUpperBoundary() {
        assertFalse("Age above upper boundary should be invalid", AgeValidator.isValidAge(66));
    }
}

public class AgeValidator {
    public static boolean isValidAge(int age) {
        return age >= 18 && age <= 65;
    }
}
```
