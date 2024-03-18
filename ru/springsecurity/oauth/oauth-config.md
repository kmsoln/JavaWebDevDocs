## Создание конфигурации сервера авторизации

Для демонстрации работы OAuth 2.0, реализуем авторизацию через Google в нашем проекте. В целом, полученные знания можно будет использовать для настройки авторизации через любой другой сервер авторизации, такой как Facebook, Яндекс и т.д.

Для того, как начать писать код, нам необходимо зарегистрировать наше приложение в Google, потому что сервер не будет принимать наши запросы без ключей доступа, токенов и прочих данных, которые превращают наши запросы из "запросов из неопределенного источника" в запросы от конкретного приложения.

Для того чтобы узнать как это сделать, перейдите [сюда](google-app.md).

После того как вы зарегистрировали приложение, вам необходимо создать конфигурацию для сервера авторизации. Для этого создайте класс `AuthorizationServerConfig` в пакете `config`:

```java
@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
                .withClient("client_id")
                .secret(passwordEncoder().encode("secret"))
                .authorizedGrantTypes("authorization_code")
                .scopes("read")
                .redirectUris("http://localhost:8080/login-success");
    }

    @Override
    public void configure(AuthorizationServerEndpointsConfigurer endpoints) throws Exception {
        endpoints.authenticationManager(authenticationManager);
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

В этом классе мы настраиваем наш сервер авторизации. Мы указываем, что наш сервер авторизации будет работать в режиме `inMemory`, то есть все данные о клиентах, которые могут получить доступ к нашему серверу, будут храниться в памяти. Это упрощение для демонстрации работы OAuth 2.0, в реальных проектах данные обычно хранятся в других местах, таких как база данных или файлы.

На место `client_id` и `secret` вставьте данные, которые вы получили при регистрации приложения в Google. Также укажите `redirectUris` - это адрес, на который будет перенаправлен пользователь после успешной авторизации.

`scopes` - это разрешения, которые мы запрашиваем у пользователя. Подробнее о разрешениях [тут](scopes.md).

`authenticationManager` - это менеджер аутентификации, который будет использоваться для проверки пользовательских данных. Мы его настроим позже.

Теперь у нас есть сервер авторизации, который будет работать в режиме `inMemory`. В следующем уроке мы настроим OAuth конфигурацию.

[**Следующий урок**: *Настройка OAuth конфига*](oauth-config.md)