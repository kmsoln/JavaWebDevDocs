# Начало работы с ORM (Object-Relational Mapping)

Для начала работы с ORM (Object-Relational Mapping) вам понадобится определиться с выбором библиотеки ORM для вашего проекта. В Java одной из самых популярных библиотек ORM является Hibernate. Давайте рассмотрим, как начать использовать Hibernate для работы с базой данных.

## Шаг 1: Добавление зависимостей

Добавьте зависимости на Hibernate в файл `pom.xml`, если вы используете Maven:

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.5.7.Final</version> <!-- Указать актуальную версию -->
</dependency>
```
Для Gradle добавьте следующую зависимость в файл build.gradle:

```gradle
implementation 'org.hibernate:hibernate-core:5.5.7.Final' // Указать актуальную версию
```

## Шаг 2: Настройка Hibernate
Создайте файл конфигурации Hibernate (hibernate.cfg.xml), который содержит информацию о вашей базе данных, такую как URL, имя пользователя и пароль. Пример файла конфигурации:
```xml
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/mydatabase</property>
        <property name="hibernate.connection.username">username</property>
        <property name="hibernate.connection.password">password</property>
        <!-- Другие настройки -->
    </session-factory>
</hibernate-configuration>

```

## Шаг 3: Создание сущностей
Определите классы-сущности, которые представляют таблицы в вашей базе данных. Например:
```java
import javax.persistence.*;

        @Entity
        @Table(name = "employees")
        public class Employee {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;

        private String firstName;
        private String lastName;
        private double salary;

        // Геттеры и сеттеры
        }

```

## Шаг 4: Использование сессии Hibernate
Теперь вы готовы использовать Hibernate для взаимодействия с базой данных. Создайте сессию Hibernate и выполняйте необходимые операции, такие как сохранение, чтение, обновление и удаление сущностей.
```java
import org.hibernate.Session;
        import org.hibernate.SessionFactory;
        import org.hibernate.cfg.Configuration;

        public class Main {
        public static void main(String[] args) {
        // Создание фабрики сессий
        SessionFactory sessionFactory = new Configuration()
        .configure("hibernate.cfg.xml")
        .addAnnotatedClass(Employee.class)
        .buildSessionFactory();

        // Получение сессии
        Session session = sessionFactory.getCurrentSession();

        try {
        // Начало транзакции
        session.beginTransaction();

        // Пример операции: сохранение сущности
        Employee employee = new Employee();
        employee.setFirstName("John");
        employee.setLastName("Doe");
        employee.setSalary(1000.0);
        session.save(employee);

        // Фиксация транзакции
        session.getTransaction().commit();
        } finally {
        // Закрытие сессии и фабрики сессий
        session.close();
        sessionFactory.close();
        }
        }
        }

```
## [К оглавлению](references.md)