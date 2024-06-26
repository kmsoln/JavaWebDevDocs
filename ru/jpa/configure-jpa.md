# Настройка JPA

После того как мы импортировали JPA в проект, необходимо настроить источники данных с которыми будет работать наше
приложение.

Для этого мы будем использовать application.properties файл, который находится в папке `src/main/resources`. В этом
файле мы определим настройки подключения к базе данных.

## Настройка подключения к базе данных

Для настройки подключения к базе данных, добавьте следующие параметры в файл `application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/testing
spring.datasource.username=postgres
spring.datasource.password=admin
```

В этом примере мы настраиваем подключение к базе данных. Мы указываем строку соединения, имя пользователя и пароль для
подключения к базе данных. 

Помимо этих настроек, необходимо также указать настройки JPA. Для этого добавьте следующие параметры в файл

`application.properties`:

```properties
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.data.jpa.repositories.enabled=true
```

В этом примере мы указываем стратегию создания таблиц в базе данных, вывод SQL запросов в консоль и возможность 
использования репозиториев JPA.

Это необходимо для того, чтобы JPA могла создавать таблицы в базе данных, выполнять SQL запросы и работать с репозиториями.

То, что показано в этом уроке - это базовая настройка JPA в проекте. Поговорим о настройках подробнее

# [**Следующий урок**: *Архитектура JPA*](architecture-jpa.md)
