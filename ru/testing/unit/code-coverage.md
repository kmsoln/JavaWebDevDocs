## Тестирование: Unit Testing и Code Coverage в Java

Unit Testing (модульное тестирование) и Code Coverage (покрытие кода тестами) являются важными аспектами разработки программного обеспечения в Java, обеспечивающими высокое качество и надежность кода.

### Основные концепции Unit Testing и Code Coverage

- **Unit Testing:** Процесс тестирования отдельных компонентов программы (юнитов) для проверки их корректности. Каждый юнит тестируется изолированно от других, что позволяет точно определить источники ошибок.

- **Code Coverage:** Метрика, которая измеряет процент кода программы, покрытого тестами. Она помогает определить, какие части кода не были протестированы, что особенно важно для обеспечения надежности и стабильности программы.

### Инструменты для Unit Testing и Code Coverage в Java

- **JUnit:** Самый популярный фреймворк для написания модульных тестов в Java. JUnit предоставляет аннотации и методы для описания тестов и проверки утверждений.

- **Jacoco:** Один из ведущих инструментов для анализа покрытия кода в Java. Jacoco интегрируется с сборщиками проектов, такими как Maven и Gradle, и предоставляет детальные отчеты о покрытии кода.

- **Mockito:** Библиотека для создания моков (подделок объектов) в Java, которая широко используется в модульном тестировании для изоляции тестируемых компонентов.

### Пример теста с использованием JUnit и Jacoco для анализа покрытия

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.*;

public class CalculatorTest {
    
    @Test
    public void testAddition() {
        Calculator calculator = new Calculator();
        assertEquals("Checking addition", 5, calculator.add(2, 3));
    }
}

// Класс Calculator для примера
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

### Настройка Jacoco для анализа покрытия с Maven
Добавьте следующий плагин в ваш pom.xml:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.5</version>
            <executions>
                <execution>
                    <goals>
                        <goal>prepare-agent</goal>
                    </goals>
                </execution>
                <execution>
                    <id>report</id>
                    <phase>prepare-package</phase>
                    <goals>
                        <goal>report</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>

```

