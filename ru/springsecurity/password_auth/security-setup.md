# Настройка Spring Security в проекте

Для начала, нам нужно добавить зависимость `spring-boot-starter-security` в наш проект. Эта зависимость нужна, чтобы включить Spring Security в нашем проекте.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

Или в файл `build.gradle`:

```gradle
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-security'
}
```

Теперь, когда мы добавили зависимость, Spring Security будет включен в нашем проекте. Но это еще не все. Нам нужно настроить Spring Security, чтобы он работал так, как нам нужно. Давайте начнем с настройки аутентификации.

# [**Следующий урок**: *Настройка аутентификации*](authentication-setup.md)