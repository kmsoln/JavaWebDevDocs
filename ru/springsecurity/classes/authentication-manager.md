# AuthenticationManager в Spring Security

В Spring Security интерфейс `AuthenticationManager` играет ключевую роль в процессе аутентификации пользователей. Он выступает в качестве центрального организатора обработки запросов на аутентификацию и делегирует задачу аутентификации зарегистрированным экземплярам `AuthenticationProvider`.

## Миссия AuthenticationManager

Основная миссия `AuthenticationManager` заключается в проверке идентификаторов пользователей на основе предоставленных учетных данных. Он управляет потоком аутентификации, вызывая зарегистрированные экземпляры `AuthenticationProvider` для проверки учетных данных пользователя и определения результата аутентификации. Кроме того, он обрабатывает исключения, связанные с аутентификацией, и принимает решение о том, была ли аутентификация успешной или нет.

## Пример использования

### Конфигурация

Для использования `AuthenticationManager` его необходимо сконфигурировать в рамках настройки Spring Security вместе с одним или несколькими экземплярами `AuthenticationProvider`.

### Пример:

```java
@Autowired
private DaoAuthenticationProvider authenticationProvider;

@Bean
public AuthenticationManager authenticationManager() {
    return new ProviderManager(Collections.singletonList(authenticationProvider));
}
```

В этом примере `AuthenticationManager` настроен с одним экземпляром `DaoAuthenticationProvider`. Вы можете добавить больше экземпляров `AuthenticationProvider` для поддержки различных механизмов аутентификации.

### Аутентификация

Во время аутентификации пользователя Spring Security вызывает `AuthenticationManager` для обработки запросов на аутентификацию.

### Пример:

```java
@Autowired
private AuthenticationManager authenticationManager;

public void authenticateUser(String username, String password) {
    Authentication authentication = new UsernamePasswordAuthenticationToken(username, password);
    Authentication authenticated = authenticationManager.authenticate(authentication);
    SecurityContextHolder.getContext().setAuthentication(authenticated);
}
```

Здесь вызывается метод `authenticate` `AuthenticationManager` для аутентификации пользователя с использованием предоставленного имени пользователя и пароля. Результатирующий объект `Authentication` содержит аутентифицированные данные пользователя.

## Заключение

`AuthenticationManager` является основой процесса аутентификации в приложениях, использующих Spring Security. Путем настройки и использования `AuthenticationManager` вместе с соответствующими экземплярами `AuthenticationProvider` разработчики могут создать надежные механизмы аутентификации для проверки идентификации пользователей и обеспечения безопасного доступа к защищенным ресурсам.

---

# [Далее: AuthenticationProvider](authentication-provider.md)
