# Настройка Thymeleaf в проекте

Чтобы начать использовать библиотеку в вашем проекте, вам нужно добавить зависимость в файл `pom.xml` вашего проекта. Чтобы подключить Thymeleaf, добавьте следующую зависимость в раздел `dependencies` файла `pom.xml`:

```xml 
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

Если вы используете Gradle Groovy, добавьте следующую строку в раздел `dependencies` файла `build.gradle`:

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
}
```

После добавления зависимости, Thymeleaf будет доступен в вашем проекте. Теперь вы можете использовать его для создания динамических веб-страниц.

# [**Следующий урок**: *Синтаксис выражений Thymeleaf]()