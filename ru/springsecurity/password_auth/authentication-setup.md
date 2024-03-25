# Конфиг Spring Security

Для настройки конфига Spring Security, нам нужно создать класс, в котором мы будем определять настройки. Он может иметь любое имя и расположение, но обычно его называют `SecurityConfig` и помещают в пакет `config`.

Вообще, этот класс будет использоваться для любых настроек Spring Security, будь то настройка аутентификации, авторизации или других настроек.

В нашем случае, нам надо настроить аутентификацию с логином и паролем. Для этого нам нужно переопределить метод `configure(AuthenticationManagerBuilder auth)`. В этом методе мы можем настроить аутентификацию.
Напомню, что для написания кода мы используем Spring6 и если какие-то методы не работают, то нужно посмотреть документацию к вашей версии Spring или обновить версию Spring до 6.

Для любых настроек в Spring используется система бинов. Мы можем использовать аннотацию `@Bean` для их создания. Более подробно о бинах можно почитать [тут](../../common/beans.md).

В нашем примере мы будем использовать InMemory авторизацию для простоты. Но в реальном проекте, конечно, лучше использовать базу данных, о которой мы поговорим в будущем.

```java
@EnableWebSecurity
@Configuration
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .authorizeHttpRequests(
                        (auth) -> auth.anyRequest().permitAll()
                )
                .httpBasic(withDefaults())
                .formLogin(configurer -> {
                    configurer
                            .loginPage("/login")
                            .permitAll()
                            .successHandler((request, response, authentication) -> {
                                response.sendRedirect("success?message=You logged in successfully!");
                            })
                            .failureHandler(((request, response, exception) -> {
                                response.sendRedirect("problem?message=Wrong login or password");
                            }));
                })
                .authenticationProvider(authenticationProvider());

        return http.build();
    }

    @Bean
    public DaoAuthenticationProvider authenticationProvider() {
        DaoAuthenticationProvider provider = new DaoAuthenticationProvider(passwordEncoder());

        provider.setUserDetailsService(userDetailsService());

        return provider;
    }

    @Bean
    public UserDetailsService userDetailsService() {
        return new InMemoryUserDetailsManager();
    }

    @Bean
    public BCryptPasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

В этом коде мы создаем класс `SecurityConfig`, который помечен аннотацией `@Configuration`. Это означает, что Spring будет использовать этот класс для настройки.

Мы также помечаем его аннотацией `@EnableWebSecurity`, чтобы сообщить Spring, что это конфигурация Spring Security, именно класс с этой аннотацией будет искать Spring при запуске нашего приложения и инициализации настроек безопасности.

Процесс настройки в Spring организован так, чтобы это выглядело максимально просто и наглядно. Обычно это структура `method chaining`, при помощи которой Spring собирает данные и настраивает систему. То какие данные ему передать выбирает программист, используя эти самые методы.

Перед тем, как продолжить, советую почитать что такое [method chaining (цепочка вызовов)](../../common/method-chain.md).

Итак, в нашем коде мы создаем бин `securityFilterChain`, который возвращает объект `http`, который мы настраиваем. Мы разрешаем все запросы, используя метод `anyRequest().permitAll()`, что означает, что все запросы разрешены.

Мы также настраиваем базовую аутентификацию и форму входа. В случае успешной аутентификации, мы перенаправляем пользователя на страницу `success`, а в случае ошибки - на страницу `problem`. Что делает этот код конкретно не так важно, главное понимать, что он обрабатывает успех и ошибку логина, перенаправляя пользователя на нужные страницы.

Мы также создаем бин `authenticationProvider`, который возвращает объект `DaoAuthenticationProvider`. `DaoAuthenticationProvider` - это класс, который наследуется от AuthenticationProvider и используется для настройки источника данных для аутентификации. 

То есть суть в том, чтобы указать откуда берутся данные для авторизации и каким образом они там хранятся. Например, в конструкторе мы используем `passwordEncoder`. Это отдельный бин, который отвечает за настройку шифрования паролей. В нашем случае, это BCryptPasswordEncoder. Зачем нам нужно шифровать пароли, можно почитать [тут](password-hashing.md).

Далее, мы создаем бин `userDetailsService`, который возвращает объект `InMemoryUserDetailsManager`. Этот класс используется для хранения пользователей в оперативной памяти.

`userDetailsService` мы также устанавливаем в `authenticationProvider`, чтобы он знал откуда брать пользователей для аутентификации.

Вот и все. Теперь у нас есть настроенный Spring Security, который использует InMemory хранилище для пользователей и BCrypt для шифрования паролей, но ты мог заметить, что мы еще ни сказали не слова о регистрации пользователей. Об этом мы поговорим в следующем уроке.

# [**Следующий урок**: *Регистрация*](in-memory-registration.md)