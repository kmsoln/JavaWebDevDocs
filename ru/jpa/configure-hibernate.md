# Настройка Hibernate в проекте

После того, как мы добавили Hibernate в проект, необходимо настроить его.

## Создание файла `hibernate.cfg.xml`

Hibernate использует файл конфигурации `hibernate.cfg.xml` для настройки своего поведения. Этот файл содержит информацию о подключении к базе данных, настройках Hibernate и других параметрах.

Создайте файл `hibernate.cfg.xml` в папке `src/main/resources` вашего проекта и добавьте следующий код:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/mydatabase</property>
        <property name="hibernate.connection.username">root</property>
        <property name="hibernate.connection.password">password</property>
        <property name="hibernate.dialect">org.hibernate.dialect.MySQL8Dialect</property>
        <property name="hibernate.hbm2ddl.auto">update</property>
        <property name="hibernate.show_sql">true</property>
    </session-factory>
</hibernate-configuration>
```

В этом примере мы указали следующие свойства:

- `hibernate.connection.driver_class` - класс JDBC драйвера для вашей базы данных. (В данном случае, MySQL)
- `hibernate.connection.url` - URL подключения к базе данных.
- `hibernate.connection.username` - имя пользователя базы данных. (Во всех базах данных, главный пользователь называется `root`, но например в PostgreSQL это `postgres`)
- `hibernate.connection.password` - пароль вашего пользователя, которого вы указали в предыдущем свойстве.
- `hibernate.dialect` - диалект базы данных. (В данном случае, MySQL8)
- `hibernate.hbm2ddl.auto` - стратегия создания таблиц в базе данных. Подробнее о стратегиях можно прочитать [здесь](hibernate-strategy.md).
- `hibernate.show_sql` - показывать или нет SQL запросы в консоли. Если стоит `true`, то те запросы о которых мы говорили в уроках про аннотации, будут показываться в консоли.

Как только вы завершили настройку `hibernate.cfg.xml`, все entity классы будут автоматически преобразованы в таблицы в базе данных при запуске приложения.

# [**Следующий урок**: *CRUD*](crud/what-is-crud.md)