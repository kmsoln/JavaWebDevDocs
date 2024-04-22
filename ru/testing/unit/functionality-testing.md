## Unit Testing и Functionality Testing в Java

Unit testing и Functionality Testing являются важными аспектами разработки программного обеспечения, позволяющими обеспечить надежность и функциональность кода. В Java, эти виды тестирования часто реализуются с помощью популярных фреймворков, таких как JUnit.

### Unit Testing в Java

Unit testing фокусируется на проверке наименьших тестируемых частей программы, таких как методы и классы, чтобы убедиться в их корректной работе в изоляции от остальной части системы.

#### Примеры Unit Testing:

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class CalculatorTests {
    
    @Test
    public void testAddition() {
        Calculator calculator = new Calculator();
        assertEquals("Addition should be correct", 5, calculator.add(2, 3));
    }
}
```
В этом примере класс Calculator тестируется для проверки функциональности метода сложения.

### Functionality Testing в Java
Functionality Testing, или функциональное тестирование, направлено на проверку того, что различные части приложения работают в соответствии с его функциональными требованиями.

Примеры Functionality Testing:
```java
import org.junit.Test;
import static org.junit.Assert.*;

public class UserManagementTests {

    @Test
    public void testUserCreation() {
        User user = new User("username", "password");
        assertEquals("Username should match", "username", user.getUsername());
        assertNotNull("Password should be encrypted and not null", user.getEncryptedPassword());
    }
}
```
В этом примере тестируется создание пользователя, проверяя, что имя пользователя сохраняется корректно и что пароль пользователя шифруется и не равен null.


