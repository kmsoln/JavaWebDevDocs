# Thymeleaf and Spring

We've covered the basic syntax elements of Thymeleaf, but how does it all tie in with Spring? In this lesson, we'll explore how to use Thymeleaf together with Spring.

The operation logic of Thymeleaf in Spring is based on the interaction of Spring controllers with Thymeleaf templates. Controllers handle requests and return Thymeleaf templates, which are then displayed on web pages. As you already know, controllers can pass data to the web page using a model. Using Thymeleaf's syntax constructs, which we've covered earlier, we can work with this data on the page.

Let's consider a simple example. Suppose we have a controller that fetches a user's passport data from a database and passes it to a web page. We can use Thymeleaf to display this data on the page. Here's an example controller:

```java
@Controller
public class PassportController {

    @Autowired
    private PassportService passportService;

    @GetMapping("/passport")
    public String showPassport(Model model) {
        Passport passport = passportService.getPassport();
        model.addAttribute("passport", passport);
        return "passport";
    }
}
```

In this example, we created a `PassportController` controller that handles GET requests to `/passport`. In the `showPassport` method, we retrieve the user's passport data from the `PassportService` and pass it to the page using the model.

Now let's create a Thymeleaf template that will display the passport data on the page. Here's an example template `passport.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Passport Data</title>
</head>
<body>
    <h1>Passport Data</h1>
    <p>Name: <span th:text="${passport.name}"></span></p>
    <p>Date of Birth: <span th:text="${passport.dob}"></span></p>
    <p>Passport: <span th:text="${passport.passport}"></span></p>
</body>
</html>
```

In this example, we created a Thymeleaf template that displays the user's passport data. We use Thymeleaf's syntax constructs to display the data passed from the controller.

Now, when a user sends a GET request to `/passport`, the controller will return the Thymeleaf template `passport.html`, which will display the passport data on the page.
