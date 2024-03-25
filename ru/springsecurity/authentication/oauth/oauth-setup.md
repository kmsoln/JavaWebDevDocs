# Настройка OAuth 2.0 в проекте Spring

Для того, чтобы использовать OAuth в Spring, нам необходимо добавить зависимость `spring-security-oauth2` в наш проект. Это можно сделать, добавив следующую зависимость в файл `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.security.oauth</groupId>
    <artifactId>spring-security-oauth2</artifactId>
    <version>2.3.4.RELEASE</version>
</dependency>
```

Или в файл `build.gradle`:

```gradle
dependencies {
    implementation 'org.springframework.security.oauth:spring-security-oauth2:2.3.4.RELEASE'
}
```

Теперь, когда мы добавили зависимость, мы можем начать настраивать наш проект для использования OAuth. Давайте начнем с создания конфигурации для нашего сервера авторизации.

# [**Следующий урок**: *OAuth Конфиг*](oauth-config.md)
