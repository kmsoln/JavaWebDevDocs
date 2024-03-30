# PasswordEncoder in Spring Security

In Spring Security, the `PasswordEncoder` interface plays a pivotal role in encoding and verifying passwords securely. It provides a standardized approach to hash passwords, ensuring their protection from unauthorized access. Understanding `PasswordEncoder` is essential for implementing robust authentication mechanisms and safeguarding user credentials effectively.

## Mission of PasswordEncoder

The primary objective of the `PasswordEncoder` interface is to ensure the secure storage and verification of user passwords. It enables developers to encode plain-text passwords into hashed formats before storing them, enhancing security by preventing exposure of sensitive user data. When authenticating users, `PasswordEncoder` facilitates comparison between hashed passwords and provided plain-text passwords, ensuring authentication integrity without compromising security.

## Example Usage

### Using PasswordEncoder

To utilize a `PasswordEncoder`, developers typically choose an implementation provided by Spring Security, such as `BCryptPasswordEncoder` or `Pbkdf2PasswordEncoder`. These implementations utilize robust cryptographic algorithms for secure password hashing.

### Example:

```java
@Bean
public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}
```

In this example, a `BCryptPasswordEncoder` is configured as a `@Bean` within the Spring application context. This implementation employs the BCrypt hashing algorithm, known for its security and strength.

### Encoding Passwords

When creating or updating user accounts, developers can leverage the `PasswordEncoder` to hash plain-text passwords securely before storing them.

### Example:

```java
@Autowired
private PasswordEncoder passwordEncoder;

public void createUser(String username, String password) {
    String encodedPassword = passwordEncoder.encode(password);
    // Save the user with the encoded password
}
```

Here, the `encode` method of `PasswordEncoder` is used to hash the plain-text password before persisting it in the database.

### Verifying Passwords

During user authentication, developers can employ the `PasswordEncoder` to verify that the provided password matches the hashed password stored in the database.

### Example:

```java
@Autowired
private PasswordEncoder passwordEncoder;

public boolean authenticate(String username, String password) {
    // Retrieve the user's hashed password from the database
    String hashedPassword = userService.getPasswordByUsername(username);
    // Verify the provided password against the hashed password
    return passwordEncoder.matches(password, hashedPassword);
}
```

In this example, the `matches` method of `PasswordEncoder` compares the provided plain-text password with the hashed password retrieved from the database, ensuring authentication integrity.

## Existing Hashing Types in Spring Security

Spring Security offers several `PasswordEncoder` implementations, including:

- **BCryptPasswordEncoder**: Utilizes the BCrypt hashing algorithm.
- **Pbkdf2PasswordEncoder**: Implements the PBKDF2 algorithm with HMAC SHA-1 as the hash function.
- **SCryptPasswordEncoder**: Utilizes the scrypt hashing algorithm.

## Custom Hashing Mechanism

Besides the built-in `PasswordEncoder` implementations provided by Spring Security, developers can create custom hashing mechanisms to fulfill specific requirements or utilize alternative hashing algorithms. Here's a step-by-step guide on implementing a custom hashing mechanism:

### Step 1: Define Custom PasswordEncoder

Create a class that implements the `PasswordEncoder` interface, incorporating the logic for hashing passwords based on the desired algorithm.

### Example:

```java
public class CustomPasswordEncoder implements PasswordEncoder {

    @Override
    public String encode(CharSequence rawPassword) {
        // Implement custom password hashing logic
    }

    @Override
    public boolean matches(CharSequence rawPassword, String encodedPassword) {
        // Implement custom password verification logic
    }
}
```

### Step 2: Configure Custom PasswordEncoder

Register the custom `PasswordEncoder` bean in the Spring application context configuration, allowing Spring Security to utilize the custom hashing mechanism for password encoding and verification.

### Example:

```java
@Bean
public PasswordEncoder passwordEncoder() {
    return new CustomPasswordEncoder();
}
```

### Step 3: Utilize Custom PasswordEncoder

Inject the custom `PasswordEncoder` bean into authentication mechanisms or services where password encoding or verification is required. Update the configuration to use the custom `PasswordEncoder` implementation.

### Step 4: Test and Validate

Thoroughly test the custom hashing mechanism to ensure it securely hashes passwords and accurately verifies them during authentication. Validate the implementation against established security standards and best practices.

### Example for Custom Encoder

```java
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Component;

import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.PBEKeySpec;
import java.security.NoSuchAlgorithmException;
import java.security.spec.InvalidKeySpecException;
import java.util.Base64;

@Component
public class CustomEncoder implements PasswordEncoder {

    private static final String SECRET = "mySecretKey";
    private static final int ITERATION = 10000;
    private static final int KEY_LENGTH = 512;

    @Override
    public String encode(CharSequence cs) {
        String algorithm = "PBKDF2WithHmacSHA512";

        try {
            byte[] result = SecretKeyFactory.getInstance(algorithm)
                    .generateSecret(new PBEKeySpec(
                            cs.toString().toCharArray(),
                            SECRET.getBytes(),
                            ITERATION,
                            KEY_LENGTH))
                    .getEncoded();
            return Base64.getEncoder().encodeToString(result);
        } catch (NoSuchAlgorithmException | InvalidKeySpecException ex) {
            throw new RuntimeException(ex);
        }
    }

    @Override
    public boolean matches(CharSequence cs, String string) {
        return encode(cs).equals(string);
    }
}
```

## Conclusion

`PasswordEncoder` serves as a fundamental interface in Spring Security, enabling secure password storage and verification. Whether utilizing built-in implementations or creating custom ones, developers can ensure that user passwords are hashed using robust cryptographic algorithms, thereby safeguarding them from unauthorized access and enhancing overall application security.
