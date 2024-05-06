# Настройка Hibernate в проекте

После того как мы добавили Hibernate в проект, необходимо настроить его.

Есть два пути для того, чтобы это сделать. Первый и наиболее современный, который мы разберем сегодня - использование Java конфигурации (Beans).

При использовании Hibernate 6 появилась возможность настроить его без использования XML файлов. Вместо этого, вы можете использовать Java классы для настройки Hibernate.

Давайте используем класс конфигурации, который мы создали ранее, модифицировав его для настройки Hibernate.

```java
@Configuration
@EnableTransactionManagement
public class HibernateConfig {

    @Bean
    public LocalSessionFactoryBean sessionFactory() {
        LocalSessionFactoryBean sessionFactory = new LocalSessionFactoryBean();
        sessionFactory.setDataSource(dataSource());
        sessionFactory.setHibernateProperties(hibernateProperties());

        return sessionFactory;
    }

    @Bean
    public DataSource dataSource() {
        BasicDataSource dataSource = new BasicDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/dbname");
        dataSource.setUsername("username");
        dataSource.setPassword("password");

        return dataSource;
    }

    private final Properties hibernateProperties() {
        Properties hibernateProperties = new Properties();
        hibernateProperties.setProperty("hibernate.hbm2ddl.auto", "create-drop");
        hibernateProperties.setProperty("hibernate.dialect", "org.hibernate.dialect.MySQL5Dialect");

        return hibernateProperties;
    }
}
```

В этом классе мы создаем бин `sessionFactory`, который представляет собой фабрику сессий Hibernate и является центральным элементом настройки. Мы указываем, что наш источник данных - это `dataSource`, который мы также создаем в этом классе.

В качестве источника данных мы используем базу данных MySQL. Мы указываем URL, имя пользователя и пароль для подключения к базе данных.

Мы также указываем свойства Hibernate, такие как `hibernate.hbm2ddl.auto` и `hibernate.dialect`. Первое свойство указывает Hibernate, что он должен создавать таблицы при запуске приложения и удалять их при остановке. Второе свойство указывает Hibernate, что он должен использовать диалект H2 базы данных. *Эти параметры указывать не обязательно, но полезно знать, что возможность дополнительной настройки в Hibernate есть и делается она вот таким способом*

# [**Следующий урок**: *CRUD*](crud/what-is-crud.md)