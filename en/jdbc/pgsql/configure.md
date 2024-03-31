# Configure JDBC for PostgreSQL

After successfully adding the PostgreSQL JDBC driver dependency to your project, you need to configure the connection to PostgreSQL. Follow these steps to configure PostgreSQL in your Java project:

1. **Obtain PostgreSQL Connection String**: The PostgreSQL connection string includes details such as the hostname, port number, database name, and authentication credentials (if required). You can obtain this connection string from your PostgreSQL server administrator or from a cloud provider if you are using a managed PostgreSQL service.

2. **Add Connection String to Your Application**: Once you have the connection string, add it to your Java application where you establish the JDBC connection to PostgreSQL.

3. **Configure JDBC Connection**: Use the obtained connection string to configure your JDBC connection in your Java code. Here's an example of how you can configure the JDBC connection using the PostgreSQL JDBC driver:

   ### Using application.properties

   If you're using Spring Boot or a similar framework that supports externalized configuration through `application.properties` or `application.yml`, you can configure the PostgreSQL connection directly from your configuration file. Follow these steps:

    1. **Obtain PostgreSQL Connection String**: Obtain the PostgreSQL connection string containing the necessary information about the PostgreSQL server's location, authentication details, and other parameters.

    2. **Add Connection String to application.properties**: Open your `application.properties` file and add the PostgreSQL connection string using the appropriate property key. Here's an example:

       ```properties
       # PostgreSQL connection string
       spring.datasource.url=jdbc:postgresql://hostname:5432/databaseName
 
       # Database credentials
       spring.datasource.username=username
       spring.datasource.password=password
       ```

       Replace `"hostname"`, `"databaseName"`, `"username"`, and `"password"` with the appropriate values for your PostgreSQL server.

    3. **Use the Connection in Your Application**: With the PostgreSQL connection configured in `application.properties`, you can now use it in your application code without explicitly configuring the JDBC connection. Spring Boot's auto-configuration will automatically set up the JDBC connection using the properties specified in `application.properties`.

    4. **Test the Connection**: Run your application to verify that the PostgreSQL connection is established successfully. Ensure that you can execute queries or perform other database operations as needed.

   By following these steps and configuring the PostgreSQL connection in `application.properties`, you can seamlessly integrate PostgreSQL into your Java application using JDBC.

### Using application class
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class PostgreSQLConnection {
    public static void main(String[] args) {
        // PostgreSQL connection string
        String connectionString = "jdbc:postgresql://hostname:5432/databaseName";

        // Database credentials
        String username = "username";
        String password = "password";

        // Establish JDBC connection
        try {
            Connection connection = DriverManager.getConnection(connectionString, username, password);

            // Connection established successfully
            System.out.println("Connected to PostgreSQL!");
            
            // Use the connection for executing queries or other database operations
            // ...
            
            // Don't forget to close the connection when done
            connection.close();
        } catch (SQLException e) {
            // Handle connection errors
            e.printStackTrace();
        }
    }
}
```

Replace `"hostname"`, `"databaseName"`, `"username"`, and `"password"` with the appropriate values for your PostgreSQL server.

4. **Test the Connection**: After configuring the connection, run your Java application to test if the connection to PostgreSQL is established successfully. Ensure that you can execute queries or perform other database operations as needed.

By following these steps, you can configure JDBC for PostgreSQL in your Java project and establish a connection to your PostgreSQL database.
