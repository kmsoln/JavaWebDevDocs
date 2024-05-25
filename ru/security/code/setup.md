# Добавление Spring Security в Spring проект

Для добавления Spring Security в проект Spring, вам достаточно добавить его в проект как зависимость:


Maven:
```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-web</artifactId>
    <version>5.4.6</version>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-config</artifactId>
    <version>5.4.6</version>
</dependency>
  ```

Gradle:
```gradle
implementation 'org.springframework.security:spring-security-web:5.4.6'
implementation 'org.springframework.security:spring-security-config:5.4.6'
```

# [**Следующий урок**: *Настройка Spring Security*](configuration.md)
