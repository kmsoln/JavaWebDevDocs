# UserDetails in Spring Security

In Spring Security, `UserDetails` serves as an interface representing core user information retrieved by the `UserDetailsService`. It encapsulates essential user details such as username, password, authorities, and the status of the user's account. Understanding `UserDetails` is essential for implementing custom user authentication and authorization mechanisms in Spring Security.

## Mission of UserDetails

The primary mission of the `UserDetails` interface is to provide a standardized way to represent user information within Spring Security. It acts as a contract for classes responsible for loading user-specific data for authentication and authorization purposes. By implementing `UserDetails`, developers can create custom user objects that Spring Security can use to authenticate users and apply access control policies.

## Existing Methods in UserDetails

The `UserDetails` interface defines several methods for accessing user information:

- `String getPassword()`: Returns the user's password.
- `String getUsername()`: Returns the user's username.
- `boolean isAccountNonExpired()`: Indicates whether the user's account is non-expired.
- `boolean isAccountNonLocked()`: Indicates whether the user's account is non-locked.
- `boolean isCredentialsNonExpired()`: Indicates whether the user's credentials are non-expired.
- `boolean isEnabled()`: Indicates whether the user's account is enabled.

## Example Usage

### Retrieving UserDetails

When a user attempts to authenticate in a Spring Security-enabled application, the `UserDetailsService` is responsible for loading the `UserDetails` object associated with the provided username. This `UserDetails` object typically contains the user's credentials (e.g., password), authorities (e.g., roles), and other relevant information required for authentication and authorization.

### Implementing UserDetails

To create a custom user object that implements the `UserDetails` interface, you need to provide implementations for its methods. Here's an example of how to implement a custom `UserDetails` class:

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

    // Constructor, getters, and setters

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

### Creating UserDetails Object

Once you have implemented the `UserDetails` interface, you can create instances of your custom user class and populate them with user information. Here's how you can create a `UserDetails` object using the custom implementation:

```java
@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
            .orElseThrow(() -> new UsernameNotFoundException("User not found with username: " + username));

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

In this example, `CustomUserDetailsService` implements the `UserDetailsService` interface to load user-specific data from the `UserRepository`. The `loadUserByUsername` method retrieves a `User` entity from the database and constructs a `UserDetails` object using the provided builder.

### Using UserDetails for Authentication

Once the `UserDetails` object is retrieved, Spring Security utilizes it for authentication purposes. The provided credentials are compared against the stored password, and additional checks such as account expiration and account lockout are performed based on the information provided by the `UserDetails` object.

## Conclusion

`UserDetails` is a fundamental interface in Spring Security that represents user-specific data required for authentication and authorization. By implementing this interface and providing user details, developers can seamlessly integrate their application's user model with Spring Security, enabling robust security features such as authentication, authorization, and access control.