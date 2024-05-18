# Проверка роли в Spring Security

В Spring Security можно проверить роль пользователя для доступа к определенным страницам. Есть несколько способов сделать это.

## Использование авторизации внутри метода `securityFilterChain`
Первый - это использование авторизации внутри метода `securityFilterChain`. Для этого используется метод `authorizeHttpRequests`, который принимает лямбда-выражение, в котором можно настроить доступ к страницам.

```java
@EnableWebSecurity
@Configuration
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .authorizeHttpRequests(
                        (auth) -> auth
                                .antMatchers("/admin").hasRole("ADMIN")
                                .antMatchers("/user").hasRole("USER")
                                .anyRequest().authenticated()
                )
                .formLogin(withDefaults());

        return http.build();
    }

    @Bean
    public UserDetailsService userDetailsService() {
        UserDetails user = User.withDefaultPasswordEncoder()
                .username("user")
                .password("password")
                .roles("USER")
                .build();

        UserDetails admin = User.withDefaultPasswordEncoder()
                .username("admin")
                .password("password")
                .roles("ADMIN")
                .build();

        return new InMemoryUserDetailsManager(user, admin);
    }
}
```

Как видите, тут мы модифицировали метод `securityFilterChain`. Теперь мы используем метод `authorizeHttpRequests`, который использует лямбда-выражения для настройки доступа к страницам. Мы разрешили доступ к странице `/admin` только для пользователей с ролью `ADMIN`, а к странице `/user` только для пользователей с ролью `USER`. Для всех остальных запросов доступ разрешен только для аутентифицированных пользователей.

Также, мы модифицировали метод `userDetailsService`, чтобы добавить двух пользователей - `user` и `admin`. Пользователь `user` имеет роль `USER`, а пользователь `admin` имеет роль `ADMIN`.

## Использование аннотаций

Второй способ - использование аннотаций. Для этого можно использовать аннотацию `@PreAuthorize`, которая позволяет ограничить доступ к методам контроллера на основе ролей.

```java
@RestController
public class UserController {

    @PreAuthorize("hasRole('ADMIN')")
    @GetMapping("/admin")
    public String admin() {
        return "Hello, admin
    }

    @PreAuthorize("hasRole('USER')")
    @GetMapping("/user")
    public String user() {
        return "Hello, user!";
    }
}
```

В этом примере мы используем аннотацию `@PreAuthorize` для ограничения доступа к методам контроллера на основе ролей. Метод `admin` доступен только для пользователей с ролью `ADMIN`, а метод `user` доступен только для пользователей с ролью `USER`.

Внутри аннотации `@PreAuthorize` мы используем метод `hasRole`, который проверяет наличие у пользователя указанной роли. Если у пользователя нет этой роли, он не сможет вызвать метод.

# [**Следующий урок**: *Authorities*](role-check.md)