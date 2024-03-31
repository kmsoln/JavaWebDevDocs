# Configure JDBC for MongoDB

After successfully adding the MongoDB JDBC driver dependency to your project, you need to configure the connection to MongoDB. Follow these steps to configure MongoDB in your Java project:

1. **Obtain MongoDB Connection String**: In MongoDB, the connection string contains information about the MongoDB server's location, authentication details, and other parameters. You typically obtain this connection string from your MongoDB server administrator or from a cloud provider if you are using a managed MongoDB service.

2. **Add Connection String to Your Application**: Once you have the connection string, add it to your Java application where you establish the JDBC connection to MongoDB. The connection string follows a specific format and includes details such as the hostname, port number, database name, and authentication credentials (if required).

3. **Configure JDBC Connection**: Use the obtained connection string to configure your JDBC connection in your Java code. Here's an example of how you can configure the JDBC connection using the MongoDB JDBC driver:

   ### Using application.properties

   If you're using Spring Boot or a similar framework that supports externalized configuration through `application.properties` or `application.yml`, you can configure the MongoDB connection directly from your configuration file. Follow these steps:

    1. **Obtain MongoDB Connection String**: As mentioned earlier, obtain the MongoDB connection string containing the necessary information about the MongoDB server's location, authentication details, and other parameters.

    2. **Add Connection String to application.properties**: Open your `application.properties` file and add the MongoDB connection string using the appropriate property key. The format of the connection string follows the JDBC URL format. Here's an example:

       ```properties
       # MongoDB connection string
       spring.datasource.url=jdbc:mongodb://hostname:27017/databaseName
 
       # Database credentials (if required)
       spring.datasource.username=username
       spring.datasource.password=password
       ```

       Replace `"hostname"`, `"databaseName"`, `"username"`, and `"password"` with the appropriate values for your MongoDB server.

    3. **Use the Connection in Your Application**: With the MongoDB connection configured in `application.properties`, you can now use it in your application code without explicitly configuring the JDBC connection. Spring Boot's auto-configuration will automatically set up the JDBC connection using the properties specified in `application.properties`.

    4. **Test the Connection**: Run your application to verify that the MongoDB connection is established successfully. Ensure that you can execute queries or perform other database operations as needed.

   By following these steps and configuring the MongoDB connection in `application.properties`, you can seamlessly integrate MongoDB into your Java application using JDBC.

### Using application class
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class MongoDBConnection {
    public static void main(String[] args) {
        // MongoDB connection string
        String connectionString = "jdbc:mongodb://hostname:27017/databaseName";

        // Database credentials (if required)
        String username = "username";
        String password = "password";

        // Establish JDBC connection
        try {
            Connection connection;
            if (username != null && password != null) {
                connection = DriverManager.getConnection(connectionString, username, password);
            } else {
                connection = DriverManager.getConnection(connectionString);
            }

            // Connection established successfully
            System.out.println("Connected to MongoDB!");
            
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

Replace `"hostname"`, `"databaseName"`, `"username"`, and `"password"` with the appropriate values for your MongoDB server.

4. **Test the Connection**: After configuring the connection, run your Java application to test if the connection to MongoDB is established successfully. Ensure that you can execute queries or perform other database operations as needed.

By following these steps, you can configure JDBC for MongoDB in your Java project and establish a connection to your MongoDB database.