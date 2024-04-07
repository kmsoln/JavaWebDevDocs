# Добавление JPA в проект

Для работы с JPA, необходимо, как всегда, сначала его импортировать в проект. Для этого добавьте зависимость в файл `pom.xml`:

```xml
<dependency>
    <groupId>javax.persistence</groupId>
    <artifactId>javax.persistence-api</artifactId>
    <version>2.2</version>
</dependency>
```

Также, нам необходима реализация JPA. В качестве реализации мы будем использовать Hibernate. Добавьте зависимость на Hibernate в файл `pom.xml`:

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.4.2.Final</version>
</dependency>
```

Если вы используете Gradle вместо Maven, то добавьте зависимости в файл `build.gradle`:

```gradle
dependencies {
    implementation 'javax.persistence:javax.persistence-api:2.2'
    implementation 'org.hibernate:hibernate-core:5.4.2.Final'
}
```

Теперь, когда зависимости добавлены, необходимо настроить JPA в вашем проекте. 

# [**Следующий урок**: *Понимание архитектуры JPA*](architecture-jpa.md)
