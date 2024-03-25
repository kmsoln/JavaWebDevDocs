# Регистрация

Регистрация в Spring Boot организована чуть сложнее, чем аутентификация. В этом уроке мы рассмотрим, как настроить регистрацию пользователей в Spring Boot.

Для начала нам нужен контроллер, который будет отвечать за манипуляции с аккаунтами пользователей (регистрацией, аутентификацией и т.д.). Создадим класс `RegistrationController`:

Но прежде, чем это делать, нам понадобится класс-сервис, который будет отвечать за манипуляции с пользователями. Создадим класс `UserService`:

```java
@Service
public class UserService {

    private final UserRepository userRepository;
    private final BCryptPasswordEncoder passwordEncoder;

    public UserService(UserRepository userRepository, BCryptPasswordEncoder passwordEncoder) {
        this.userRepository = userRepository;
        this.passwordEncoder = passwordEncoder;
    }

    public void registerUser(User user) {
        user.setPassword(passwordEncoder.encode(user.getPassword()));
        userRepository.save(user);
    }
}
```

В этом классе у нас два поля, которые определяются в конструкторе - `userRepository` и `passwordEncoder`. Я думаю не стоит объяснять что они значит, ведь мы только что видели их в конфиге Spring Security и именно оттуда они будут переданы в наш класс.

Метод `registerUser` принимает объект `User` и сохраняет его в наше хранилище данных, которое также определяется в конфиге Spring Security. Перед сохранением пароль пользователя хэшируется с помощью кодировщика паролей, который также был настроен в SecurityConfig.

Я делаю на этом акцент, потому что важно понимать, что логика нашего приложения выстроена на получении данных из одного и того же места, что значит, что если нам понадобится их изменить (например перейти на базу данных), нам не нужно будет менять их по всему проекту, достаточно будет внести необходимые изменения в одном месте - в конфиге Spring Security.

Теперь создадим класс `RegistrationController`:

```java
@Controller
public class RegistrationController {

    private final UserService userService;

    public RegistrationController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/register")
    public String registerForm(Model model) {
        model.addAttribute("user", new User());
        return "register";
    }

    @PostMapping("/register")
    public String registerSubmit(@ModelAttribute User user) {
        userService.registerUser(user);
        return "redirect:/login";
    }
}
```

В этом классе у нас есть два метода - `registerForm` и `registerSubmit`. Первый метод отвечает за отображение формы регистрации, а второй за обработку данных, полученных из этой формы.

Метод `registerForm` принимает объект `Model`, который используется для передачи данных в представление. Мы добавляем в модель объект `User`, чтобы наша форма могла его использовать. Если не совсем понятно как это работает, рекомендую вернуться и перечитать [урок про работу форм в Thymeleaf](../../common/method-chain.md).

Метод `registerSubmit` принимает объект `User`, который заполняется данными из формы. Мы передаем этот объект в сервис `userService`, который сохраняет его в хранилище данных.

Теперь создадим представление `register.html`:

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Registration</title>
</head>
<body>
<form action="#" th:action="@{/register}" th:object="${user}" method="post">
    <div>
        <label for="username">Username:</label>
        <input type="text" id="username" th:field="*{username}"/>
    </div>
    <div>
        <label for="password">Password:</label>
        <input type="password" id="password" th:field="*{password}"/>
    </div>
    <button type="submit">Register</button>
</form>
</body>
</html>
```

В этом представлении мы создали форму, которая отправляет POST запрос на `/register`. Мы использовали атрибут `th:object`, чтобы связать форму с объектом `user`, который будет содержать данные формы и должен быть создан и передан на страницу из контроллера. Для каждого поля формы мы использовали атрибут `th:field`, чтобы связать поле с соответствующим полем объекта `user`. После передачи формы, объект `user` будет содержать данные, введенные пользователем.

Как видите, это обыкновенная форма, которую мы уже обсуждали, и обыкновенный метод в контроллере, который обрабатывает данные из этой формы, отправляя их на регистрацию.

Теперь, если вы перейдете на страницу `/register`, вы увидите форму, которая позволит вам зарегистрировать нового пользователя.


![Регистрация](../resources/register-form.png)