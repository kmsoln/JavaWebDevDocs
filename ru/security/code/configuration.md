# Настройка Spring Security

Для настройки Spring Security в проекте Spring, необходимо создать класс конфигурации, который наследуется
от `WebSecurityConfigurerAdapter`. Этот класс позволяет настроить безопасность приложения, определяя правила доступа к
различным URL и ресурсам.

```java

@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .antMatchers("/", "/home").permitAll()
                .anyRequest().authenticated()
                .and()
                .formLogin()
                .loginPage("/login")
                .permitAll()
                .and()
                .logout()
                .permitAll();
    }

    @Bean
    @Override
    public UserDetailsService userDetailsService() {
        UserDetails user =
                User.withDefaultPasswordEncoder()
                        .username("user")
                        .password("password")
                        .roles("USER")
                        .build();

        return new InMemoryUserDetailsManager(user);
    }
}
```

Код выше представлен только для примера, чтобы показать класс, который наследуется от `WebSecurityConfigurerAdapter`.
Именно такой класс вы будете создавать всякий раз, когда будете настраивать Spring Security в Spring. Как видим, все
основные методы для настройки безопасности определены заранее в `WebSecurityConfigurerAdapter`, и нам нужно лишь
наследовать их и переопределить.

В методе `configure` производится настройка правил доступа к URL. Обратите внимание, что мы используем [структуру
цепочки методов](../../springboot/method-chain.md) для настройки правил доступа.

Также, после того, как мы закончили настройку одного объекта, мы вызываем метод `and()`, чтобы перейти к настройке
следующего.

Помимо метода `configure`, можно переопределить и другие методы:
- [configure(WebSecurity web)](config-methods/web-security-configure.md) - используется для настройки фильтров безопасности
- [configure(HttpSecurity http)](config-methods/http-security-configure.md) - используется для настройки правил доступа к URL
- [configure(AuthenticationManagerBuilder auth)](config-methods/authentication-manager-configure.md) - используется для настройки аутентификации

