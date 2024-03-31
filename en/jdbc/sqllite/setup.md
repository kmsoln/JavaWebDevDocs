# Setup JDBC for SQLite

## Using Gradle

To set up JDBC for SQLite in your Java project using Gradle, follow these steps:

1. **Add SQLite JDBC Driver Dependency**: Open your `build.gradle` file and add the following dependency to include the SQLite JDBC driver:

   ```gradle
   dependencies {
       implementation 'org.xerial:sqlite-jdbc:3.36.0.3'
   }
   ```

2. **Sync Gradle Project**: After adding the dependency, sync your Gradle project to download the SQLite JDBC driver.

3. **Use JDBC in Your Code**: Now you can use JDBC in your Java code to connect to SQLite, execute queries, and process results. Make sure to refer to the SQLite JDBC driver documentation for usage instructions and examples.

## Using Maven

To set up JDBC for SQLite in your Java project using Maven, follow these steps:

1. **Add SQLite JDBC Driver Dependency**: Open your `pom.xml` file and add the following dependency to include the SQLite JDBC driver:

   ```xml
   <dependencies>
       <dependency>
           <groupId>org.xerial</groupId>
           <artifactId>sqlite-jdbc</artifactId>
           <version>3.36.0.3</version>
       </dependency>
   </dependencies>
   ```

2. **Update Maven Project**: After adding the dependency, update your Maven project to download the SQLite JDBC driver.

3. **Use JDBC in Your Code**: Now you can use JDBC in your Java code to connect to SQLite, execute queries, and process results. Make sure to refer to the SQLite JDBC driver documentation for usage instructions and examples.

That's it! You have now successfully set up JDBC for SQLite in your Java project using Gradle or Maven. You can start using JDBC to interact with SQLite databases in your applications.