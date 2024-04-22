## Тестирование модульности и управление зависимостями в Java

Тестирование модульности и управление зависимостями являются важными аспектами при разработке программного обеспечения на Java. Они позволяют эффективно управлять зависимостями между компонентами приложения и обеспечивать надежное тестирование каждого модуля независимо.

### Основные концепции тестирования модульности и управления зависимостями в Java

- **Unit Testing:** Тестирование отдельных модулей или компонентов программы для проверки их функциональности в изоляции от других частей системы.

- **Dependency Management:** Управление зависимостями в Java позволяет управлять библиотеками и внешними компонентами, необходимыми для работы приложения, с помощью инструментов таких как Maven или Gradle.

### Применение тестирования модульности и управления зависимостями в Java

- **JUnit Framework:** Для тестирования модульности в Java часто используется фреймворк JUnit, который предоставляет средства для написания и выполнения модульных тестов.

- **Mocking Frameworks:** Для изоляции модулей от их зависимостей при тестировании используются фреймворки для создания заглушек (mocks) и имитаций (stubs) объектов.

- **Dependency Injection:** Применение принципа внедрения зависимостей (Dependency Injection) позволяет эффективно управлять зависимостями между компонентами и облегчает их тестирование.

### Примеры использования тестирования модульности и управления зависимостями в Java

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class ExampleTests {
    
    @Test
    public void testAddition() {
        Calculator calculator = new Calculator();
        assertEquals("Checking addition", 5, calculator.add(2, 3));
    }
    
    @Test
    public void testMocking() {
        Dependency dependency = Mockito.mock(Dependency.class);
        Mockito.when(dependency.getValue()).thenReturn(42);
        MyClass myClass = new MyClass(dependency);
        assertEquals("Check if dependency is properly used", 42, myClass.useDependency());
    }
}
```

### Применение управления зависимостями с использованием Maven

```java
<dependency>
    <groupId>group-id</groupId>
    <artifactId>artifact-id</artifactId>
    <version>1.0.0</version>
</dependency>
```