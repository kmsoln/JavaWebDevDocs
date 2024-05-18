# AuthenticationSuccessHandler in Spring Security

In Spring Security, `AuthenticationSuccessHandler` is an interface responsible for handling successful authentication events. It allows developers to define custom logic that should be executed when a user successfully authenticates, such as redirecting to a specific page, logging authentication events, or setting custom HTTP headers.

## Mission of AuthenticationSuccessHandler

The primary mission of `AuthenticationSuccessHandler` is to provide developers with a hook to execute custom behavior after a user successfully authenticates. This can include actions such as redirecting users to a designated landing page, sending custom HTTP responses, or performing additional processing based on the authentication context.

## Example Usage

### Implementing Custom AuthenticationSuccessHandler

Developers can create custom implementations of `AuthenticationSuccessHandler` to define behavior for handling successful authentication events.

### Example:

```java
@Component
public class CustomAuthenticationSuccessHandler implements AuthenticationSuccessHandler {

    @Override
    public void onAuthenticationSuccess(HttpServletRequest request, HttpServletResponse response, Authentication authentication) throws IOException, ServletException {
        // Custom logic to execute after successful authentication
        response.getWriter().println("Hello, " + userDetails.getUsername() + "! You have successfully logged in.");
        response.sendRedirect("/dashboard");
        
        
    }
}
```

In this example, `CustomAuthenticationSuccessHandler` implements the `AuthenticationSuccessHandler` interface and overrides the `onAuthenticationSuccess` method to redirect users to the "/dashboard" page after successful authentication.

### Configuring AuthenticationSuccessHandler

To use `AuthenticationSuccessHandler`, configure it in the Spring Security configuration to be invoked upon successful authentication events.

### Example:

```java
@Autowired
private CustomAuthenticationSuccessHandler authenticationSuccessHandler;

@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .formLogin()
            .successHandler(authenticationSuccessHandler)
            // Other form login configurations...
}
```

In this example, `CustomAuthenticationSuccessHandler` is injected into the Spring Security configuration and configured as the success handler for form-based authentication.


## Conclusion

`AuthenticationSuccessHandler` provides developers with a flexible mechanism to define custom behavior after successful user authentication events. By implementing custom `AuthenticationSuccessHandler` implementations or using built-in ones provided by Spring Security, developers can tailor the authentication success handling to meet the specific requirements of their applications.

---

# [Next: AuthenticationFailureHandler](authentication-failure-handler.md)
