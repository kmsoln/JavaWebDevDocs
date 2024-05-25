# Метод WebSecurityConfigurerAdapter#configure(AuthenticationManagerBuilder auth)

Этот метод используется для настройки аутентификации пользователей. Вы можете определить, как пользователи будут
аутентифицироваться, будь то в памяти, в базе данных, через LDAP и т.д.

Например, напишем приложение для аутентификации пользователей в памяти:

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
    auth
        .inMemoryAuthentication()
            .withUser("user").password("password").roles("USER");
}
```

В приведенном выше примере:

- Метод `inMemoryAuthentication()` начинает настройку аутентификации в памяти.
- Мы добавили пользователя с именем `user`, паролем `password` и ролью `USER`.
- После добавления пользователя, мы можем добавить еще пользователей, если это необходимо.

Это стандартная настройка, которую можно использовать в большинстве приложений. Однако, если вам нужно настроить
дополнительные параметры, вот еще несколько методов, которые вы можете использовать:
1. inMemoryAuthentication()
    - withUser() - добавление пользователя
    - password() - добавление пароля
    - roles() - добавление ролей
    - authorities() - добавление прав доступа
    - accountExpired() - настройка срока действия аккаунта
    - accountLocked() - настройка блокировки аккаунта
    - credentialsExpired() - настройка срока действия учетных данных
    - disabled() - настройка отключения аккаунта
2. jdbcAuthentication()
    - dataSource() - настройка источника данных
    - usersByUsernameQuery() - запрос для получения пользователя по имени
    - authoritiesByUsernameQuery() - запрос для получения прав доступа по имени пользователя
    - groupAuthoritiesByUsername() - запрос для получения прав доступа группы по имени пользователя
    - rolePrefix() - префикс роли
3. ldapAuthentication()
    - userSearchBase() - база поиска пользователей
    - userSearchFilter() - фильтр поиска пользователей
    - groupSearchBase() - база поиска групп
    - groupSearchFilter() - фильтр поиска групп
    - groupRoleAttribute() - атрибут роли группы
    - rolePrefix() - префикс роли
    - roleAuthorities() - права доступа роли
    - userDnPatterns() - шаблоны DN пользователей
    - userAttributes() - атрибуты пользователя
    - groupRoleAttribute() - атрибут роли группы
    - groupSearchFilter() - фильтр поиска групп
    - groupSearchBase() - база поиска групп
    - groupRoleAttribute() - атрибут роли группы

# [**Назад**: *Конфигурация Spring*](../configuration.md)

