# UserDetails в Spring Security

В Spring Security `UserDetails` выступает в качестве интерфейса, представляющего основную информацию о пользователе, получаемую через `UserDetailsService`. Он инкапсулирует основные данные о пользователе, такие как имя пользователя, пароль, права доступа и состояние учетной записи пользователя. Понимание `UserDetails` необходимо для реализации пользовательской аутентификации и авторизации в Spring Security.

## Миссия UserDetails

Основная миссия интерфейса `UserDetails` заключается в предоставлении стандартизированного способа представления информации о пользователе в Spring Security. Он служит контрактом для классов, ответственных за загрузку данных о пользователе для целей аутентификации и авторизации. Реализуя `UserDetails`, разработчики могут создавать пользовательские объекты, которые Spring Security может использовать для аутентификации пользователей и применения политик контроля доступа.

## Существующие методы в UserDetails

Интерфейс `UserDetails` определяет несколько методов для доступа к информации о пользователе:

- `String getPassword()`: Возвращает пароль пользователя.
- `String getUsername()`: Возвращает имя пользователя.
- `boolean isAccountNonExpired()`: Указывает, истек ли срок действия учетной записи пользователя.
- `boolean isAccountNonLocked()`: Указывает, заблокирована ли учетная запись пользователя.
- `boolean isCredentialsNonExpired()`: Указывает, истекли ли учетные данные пользователя.
- `boolean isEnabled()`: Указывает, включена ли учетная запись пользователя.

## Пример использования

### Получение UserDetails

Когда пользователь пытается аутентифицироваться в приложении, включенном в Spring Security, `UserDetailsService` отвечает за загрузку объекта `UserDetails`, связанного с предоставленным именем пользователя. Этот объект `UserDetails` обычно содержит учетные данные пользователя (например, пароль), права доступа (например, роли) и другую актуальную информацию, необходимую для аутентификации и авторизации.

### Реализация UserDetails

Чтобы создать пользовательский объект, который реализует интерфейс `UserDetails`, необходимо предоставить реализации его методов. Вот пример реализации пользовательского класса `UserDetails`:

```java
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;
import java.util.Collection;

public class CustomUserDetails implements UserDetails {

    private String username;
    private String password;
    private Collection<? extends GrantedAuthority> authorities;
    private boolean accountNonExpired;
    private boolean accountNonLocked;
    private boolean credentialsNonExpired;
    private boolean enabled;

    // Конструктор, геттеры и сеттеры

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return authorities;
    }

    @Override
    public String getPassword() {
        return password;
    }

    @Override
    public String getUsername() {
        return username;
    }

    @Override
    public boolean isAccountNonExpired() {
        return accountNonExpired;
    }

    @Override
    public boolean isAccountNonLocked() {
        return accountNonLocked;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return credentialsNonExpired;
    }

    @Override
    public boolean isEnabled() {
        return enabled;
    }
}
```

### Создание объекта UserDetails

После реализации интерфейса `UserDetails` можно создавать экземпляры пользовательского класса и заполнять их информацией о пользователе. Вот как можно создать объект `UserDetails` с использованием пользовательской реализации:

```java
@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
            .orElseThrow(() -> new UsernameNotFoundException("Пользователь с именем пользователя " + username + " не найден"));

        return userdetails.User.withUsername(user.getUsername())
            .password(user.getPassword())
            .authorities(user.getRoles())
            .accountExpired(!user.isAccountNonExpired())
            .accountLocked(!user.isAccountNonLocked())
            .credentialsExpired(!user.isCredentialsNonExpired())
            .disabled(!user.isEnabled())
            .build();
    }
}
```

В этом примере `CustomUserDetailsService` реализует интерфейс `UserDetailsService` для загрузки данных о пользователе из `UserRepository`. Метод `loadUserByUsername` извлекает сущность `User` из базы данных и конструирует объект `UserDetails` с использованием предоставленного

 строителя.

### Использование UserDetails для аутентификации

После получения объекта `UserDetails` Spring Security использует его для аутентификации. Предоставленные учетные данные сравниваются с хранимым паролем, и выполняются дополнительные проверки, такие как проверка срока действия учетной записи и блокировка учетной записи, на основе информации, предоставленной объектом `UserDetails`.

## Заключение

`UserDetails` является основным интерфейсом в Spring Security, представляющим информацию о пользователе, необходимую для аутентификации и авторизации. Реализуя этот интерфейс и предоставляя сведения о пользователе, разработчики могут плавно интегрировать модель пользователя своего приложения с Spring Security, обеспечивая надежные функции безопасности, такие как аутентификация, авторизация и контроль доступа.

---

# [Далее: UserDetailsService](user-details-service.md)
