# Добавление Hibernate в проект

Для работы с Hibernate, необходимо добавить зависимость в файл `pom.xml`:

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.4.2.Final</version>
</dependency>
```

Также, для работы с Hibernate, необходимо добавить зависимость на JDBC драйвер для вашей базы данных. Например, для MySQL:

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.19</version>
</dependency>
```

Если вы используете Gradle вместо Maven, то добавьте зависимости в файл `build.gradle`:

```gradle
dependencies {
    implementation 'org.hibernate:hibernate-core:5.4.2.Final'
    implementation 'mysql:mysql-connector-java:8.0.19'
}
```

Теперь, когда зависимости добавлены, необходимо настроить Hibernate в вашем проекте.

# [**Следующий урок**: *Настройка Hibernate*](configure-hibernate.md)