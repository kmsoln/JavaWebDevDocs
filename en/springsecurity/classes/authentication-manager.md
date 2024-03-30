# AuthenticationManager in Spring Security

In Spring Security, the `AuthenticationManager` interface plays a crucial role in authenticating users during the authentication process. It acts as a central orchestrator for handling authentication requests and delegates the authentication task to registered `AuthenticationProvider` instances.

## Mission of AuthenticationManager

The primary mission of `AuthenticationManager` is to verify user identities based on the credentials provided. It manages the authentication flow by invoking registered `AuthenticationProvider` instances to validate user credentials and determine the authentication result. Additionally, it handles authentication-related exceptions and decides whether the authentication was successful or not.

## Example Usage

### Configuration

To use `AuthenticationManager`, it needs to be configured within the Spring Security setup alongside one or more `AuthenticationProvider` instances.

### Example:

```java
@Autowired
private DaoAuthenticationProvider authenticationProvider;

@Bean
public AuthenticationManager authenticationManager() {
    return new ProviderManager(Collections.singletonList(authenticationProvider));
}
```

In this example, `AuthenticationManager` is configured with a single `DaoAuthenticationProvider` instance. You can add more `AuthenticationProvider` instances to support various authentication mechanisms.

### Authentication

During user authentication, Spring Security invokes `AuthenticationManager` to handle authentication requests.

### Example:

```java
@Autowired
private AuthenticationManager authenticationManager;

public void authenticateUser(String username, String password) {
    Authentication authentication = new UsernamePasswordAuthenticationToken(username, password);
    Authentication authenticated = authenticationManager.authenticate(authentication);
    SecurityContextHolder.getContext().setAuthentication(authenticated);
}
```

Here, the `authenticate` method of `AuthenticationManager` is called to authenticate the user using the provided username and password. The resulting `Authentication` object contains the authenticated user details.

## Conclusion

`AuthenticationManager` serves as the backbone of the authentication process in Spring Security-enabled applications. By configuring and utilizing `AuthenticationManager` alongside appropriate `AuthenticationProvider` instances, developers can establish robust authentication mechanisms to validate user identities and ensure secure access to protected resources.

---

# [Next: AuthenticationProvider](authentication-provider.md)