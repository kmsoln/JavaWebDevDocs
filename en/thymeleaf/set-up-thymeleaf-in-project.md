## Setting up Thymeleaf in a Spring Boot Project

To integrate Thymeleaf into your Spring Boot project, follow the steps below based on your build tool. Make sure to choose the Thymeleaf version that aligns with your Spring Boot version for optimal compatibility.

### Maven Setup:

**Add Thymeleaf Dependencies in your `pom.xml` file:**

```xml
<!-- Spring Boot Starter Thymeleaf -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>

<!-- Thymeleaf and Thymeleaf-Spring6 integration -->
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-spring6</artifactId>
</dependency>
```

### Groovy Gradle Setup:

**Add Thymeleaf Dependencies in your `build.gradle` file:**

```groovy
// Spring Boot Starter Thymeleaf
implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'

// Thymeleaf and Thymeleaf-Spring6 integration
implementation 'org.thymeleaf:thymeleaf-spring6'
```

### Note on Version Compatibility:

Ensure version compatibility between Thymeleaf and Spring Boot. Align the version numbers in the dependencies (`spring-boot-starter-thymeleaf` and `thymeleaf-spring6`) with your Spring Boot version. Refer to official documentation for both Spring Boot and Thymeleaf to select the appropriate versions for a seamless integration.