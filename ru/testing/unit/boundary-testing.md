## Граничное Тестирование (Boundary Testing) в Unit Tests на Java

Граничное тестирование — это метод тестирования программного обеспечения, который сосредотачивается на поведении программы на границах допустимых входных данных. Этот вид тестирования чрезвычайно важен, так как ошибки часто возникают на краевых значениях входных данных.

### Основные принципы граничного тестирования

- **Проверка краевых значений:** Граничное тестирование включает в себя тестирование на минимальных и максимальных значениях, а также на значениях, которые находятся вблизи этих крайних точек.

- **Валидация поведения на границах:** Проверка того, как система обрабатывает ввод на границах допустимых значений, включая обработку исключений и ошибок.

- **Переполнение и аномалии:** Особое внимание уделяется случаям, которые могут вызвать переполнение, подвисание или другие нежелательные эффекты.

### Примеры граничного тестирования в Java с использованием JUnit

Допустим, у нас есть метод, который принимает целое число и возвращает его квадрат. Граничное тестирование для этого метода может включать проверку минимальных и максимальных значений `int`.

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BoundaryTests {

    public int square(int x) {
        return x * x;
    }

    @Test
    public void testSquareAtMinBoundary() {
        assertEquals("Test square at minimum int value", 0, square(Integer.MIN_VALUE));
    }

    @Test
    public void testSquareAtMaxBoundary() {
        assertEquals("Test square at maximum int value", 1, square(Integer.MAX_VALUE));
    }

    @Test
    public void testSquareNearZero() {
        assertEquals("Test square just above zero", 1, square(1));
        assertEquals("Test square just below zero", 1, square(-1));
    }
}
```

### Тестирование особенных случаев
Обработка исключений: Тесты могут также проверять, как методы обрабатывают ошибки или исключительные ситуации при вводе граничных значений.

```java
@Test(expected = ArithmeticException.class)
public void testDivisionByZero() {
    int result = 10 / 0;
}
```

