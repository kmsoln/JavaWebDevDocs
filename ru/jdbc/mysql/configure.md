# Настройка JDBC для MySQL

После успешного добавления зависимости от драйвера JDBC для MySQL в ваш проект, вам нужно настроить соединение с MySQL. Следуйте этим шагам, чтобы настроить MySQL в вашем проекте Java:

1. **Получение строки подключения к MySQL**: Строка подключения к MySQL содержит такие сведения, как имя хоста, номер порта, имя базы данных и учетные данные аутентификации (если требуется). Вы можете получить эту строку подключения у администратора вашего сервера MySQL или у облачного провайдера, если вы используете управляемый сервис MySQL.

2. **Добавление строки подключения в ваше приложение**: Как только у вас есть строка подключения, добавьте ее в ваше приложение Java, где вы устанавливаете соединение JDBC с MySQL.

3. **Настройка JDBC-соединения**: Используйте полученную строку подключения для настройки вашего JDBC-соединения в вашем Java-коде. Вот пример того, как вы можете настроить JDBC-соединение с помощью драйвера JDBC для MySQL:

   ### Использование application.properties

   Если вы используете Spring Boot или аналогичный фреймворк, поддерживающий внешнюю конфигурацию через `application.properties` или `application.yml`, вы можете настроить соединение с MySQL непосредственно из вашего файла конфигурации. Следуйте этим шагам:

    1. **Получение строки подключения к MySQL**: Получите строку подключения к MySQL, содержащую необходимую информацию о местонахождении сервера MySQL, учетных данных аутентификации и другие параметры.

    2. **Добавление строки подключения в application.properties**: Откройте ваш файл `application.properties` и добавьте строку подключения к MySQL, используя соответствующий ключ свойства. Вот пример:

       ```properties
       # Строка подключения к MySQL
       spring.datasource.url=jdbc:mysql://hostname:3306/databaseName
 
       # Учетные данные для базы данных
       spring.datasource.username=username
       spring.datasource.password=password
       ```

       Замените `"hostname"`, `"databaseName"`, `"username"` и `"password"` на соответствующие значения для вашего сервера MySQL.

    3. **Использование соединения в вашем приложении**: После того как соединение с MySQL настроено в `application.properties`, вы можете использовать его в коде вашего приложения, не явно настраивая JDBC-соединение. Автоконфигурация Spring Boot автоматически настроит JDBC-соединение с использованием свойств, указанных в `application.properties`.

    4. **Проверка соединения**: Запустите ваше приложение, чтобы убедиться, что соединение с MySQL установлено успешно. Убедитесь, что вы можете выполнить запросы или выполнить другие операции с базой данных по мере необходимости.

   Следуя этим шагам и настраивая соединение с MySQL в `application.properties`, вы можете без проблем интегрировать MySQL в ваше Java-приложение с помощью JDBC.

### Использование класса приложения
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class MySQLConnection {
    public static void main(String[] args) {
        // Строка подключения к MySQL
        String connectionString = "jdbc:mysql://hostname:3306/databaseName";

        // Учетные данные для базы данных
        String username = "username";
        String password = "password";

        // Установка JDBC-соединения
        try {
            Connection connection = DriverManager.getConnection(connectionString, username, password);

            // Соединение установлено успешно
            System.out.println("Подключено к MySQL!");
            
            // Используйте соединение для выполнения запросов или других операций с базой данных
            // ...
            
            // Не забудьте закрыть соединение при завершении
            connection.close();
        } catch (SQLException e) {
            // Обработка ошибок соединения
            e.printStackTrace();
        }
    }
}
```

Замените `"hostname"`, `"databaseName