# Setup JDBC for MongoDB

## Using Gradle

To set up JDBC for MongoDB in your Java project using Gradle, follow these steps:

1. **Add MongoDB JDBC Driver Dependency**: Open your `build.gradle` file and add the following dependency to include the MongoDB JDBC driver:

   ```gradle
   dependencies {
       implementation 'org.mongodb:mongo-java-driver:4.4.3'
   }
   ```

2. **Sync Gradle Project**: After adding the dependency, sync your Gradle project to download the MongoDB JDBC driver.

3. **Use JDBC in Your Code**: Now you can use JDBC in your Java code to connect to MongoDB, execute queries, and process results. Make sure to refer to the MongoDB JDBC driver documentation for usage instructions and examples.

## Using Maven

To set up JDBC for MongoDB in your Java project using Maven, follow these steps:

1. **Add MongoDB JDBC Driver Dependency**: Open your `pom.xml` file and add the following dependency to include the MongoDB JDBC driver:

   ```xml
   <dependencies>
       <dependency>
           <groupId>org.mongodb</groupId>
           <artifactId>mongo-java-driver</artifactId>
           <version>4.4.3</version>
       </dependency>
   </dependencies>
   ```

2. **Update Maven Project**: After adding the dependency, update your Maven project to download the MongoDB JDBC driver.

3. **Use JDBC in Your Code**: Now you can use JDBC in your Java code to connect to MongoDB, execute queries, and process results. Make sure to refer to the MongoDB JDBC driver documentation for usage instructions and examples.

That's it! You have now successfully set up JDBC for MongoDB in your Java project using Gradle or Maven. You can start using JDBC to interact with MongoDB in your applications.