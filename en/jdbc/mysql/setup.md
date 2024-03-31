# Setup JDBC for MySQL

## Using Gradle

To set up JDBC for MySQL in your Java project using Gradle, follow these steps:

1. **Add MySQL JDBC Driver Dependency**: Open your `build.gradle` file and add the following dependency to include the MySQL JDBC driver:

   ```gradle
   dependencies {
       implementation 'mysql:mysql-connector-java:8.0.27'
   }
   ```

2. **Sync Gradle Project**: After adding the dependency, sync your Gradle project to download the MySQL JDBC driver.

3. **Use JDBC in Your Code**: Now you can use JDBC in your Java code to connect to MySQL, execute queries, and process results. Make sure to refer to the MySQL JDBC driver documentation for usage instructions and examples.

## Using Maven

To set up JDBC for MySQL in your Java project using Maven, follow these steps:

1. **Add MySQL JDBC Driver Dependency**: Open your `pom.xml` file and add the following dependency to include the MySQL JDBC driver:

   ```xml
   <dependencies>
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>8.0.27</version>
       </dependency>
   </dependencies>
   ```

2. **Update Maven Project**: After adding the dependency, update your Maven project to download the MySQL JDBC driver.

3. **Use JDBC in Your Code**: Now you can use JDBC in your Java code to connect to MySQL, execute queries, and process results. Make sure to refer to the MySQL JDBC driver documentation for usage instructions and examples.

That's it! You have now successfully set up JDBC for MySQL in your Java project using Gradle or Maven. You can start using JDBC to interact with MySQL databases in your applications.