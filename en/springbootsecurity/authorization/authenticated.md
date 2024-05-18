# Understanding Authorization by Authenticated Users

## Introduction to Authorization by Authenticated Users

Authorization by authenticated users in Spring Security involves granting access to resources only to users who have successfully authenticated themselves. Unlike role-based authorization, which focuses on specific roles assigned to users, authorization by authenticated users verifies whether a user is authenticated before allowing access to protected resources.

## Configuring Authorization by Authenticated Users

### Restrict Access to Authenticated Users
Configure Spring Security to restrict access to certain resources or endpoints only to authenticated users.

### Authentication Requirement
Specify that access to protected resources requires the user to be authenticated, either through form-based authentication, HTTP basic authentication, or other authentication mechanisms supported by Spring Security.

## Best Practices for Authorization by Authenticated Users

### Protect Sensitive Resources
Use authorization by authenticated users to protect sensitive resources and prevent unauthorized access to sensitive data or functionality.

### Consider Additional Authorization Rules
In addition to requiring authentication, consider implementing additional authorization rules or checks based on user roles, permissions, or other factors to enforce fine-grained access control.

### Customize Access Denied Handling
Customize the access denied handling to provide meaningful feedback to users who attempt to access protected resources without authentication. This helps improve user experience and security awareness.

### Test Authentication Logic
Thoroughly test the authentication logic to ensure that only authenticated users are granted access to protected resources. Test various scenarios, including successful authentication, failed authentication, and access attempts by unauthenticated users.

## Example Implementation

### Controller Implementation
```java
@RestController
@RequestMapping("/api")
public class SecureController {

    @GetMapping("/secured")
    @PreAuthorize("isAuthenticated()")
    public String getSecuredResource() {
        return "This is a secured resource accessible only to authenticated users.";
    }
}
```

In this example, the `/api/secured` endpoint is accessible only to authenticated users, as specified by the `@PreAuthorize("isAuthenticated()")` annotation.

### Http Requests Implementation
```java
.authorizeRequests()
    .antMatchers("/secured/**").authenticated()
```

## Conclusion

Authorization by authenticated users ensures that only users who have successfully authenticated themselves are granted access to protected resources. By configuring Spring Security to require authentication for accessing sensitive resources and following best practices, developers can enhance the security of their applications and protect against unauthorized access.

---

# [Next: Role-Based Authorization](role.md)
