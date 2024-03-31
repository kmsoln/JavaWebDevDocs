# Spring Forms

As we already know, forms in Thymeleaf are created using the HTML `<form>` tag. However, we haven't discussed how to handle forms on the server.

Let's start by creating a simple form with user passport data that they need to enter:

```html
<form th:action="@{/passport}" th:object="${passport}" method="post">
    <div>
        <label for="name">Full Name:</label>
        <input type="text" id="name" th:field="*{name}"/>
    </div>
    <div>
        <label for="dob">Date of Birth:</label>
        <input type="date" id="dob" th:field="*{dob}"/>
    </div>
    <div>
        <label for="passport">Passport:</label>
        <input type="text" id="passport" th:field="*{passport}"/>
    </div>
    <button type="submit">Submit</button>
</form>
```

As we can see, in our form there is a `th:object` tag that binds the form to the `passport` object. This object must be created and passed to the page from the controller. For each form field, we used the `th:field` attribute to bind the field to the corresponding field of the `passport` object. After submitting the form, the `passport` object will contain the data entered by the user.

Now, how will this look on the server? To do this, we need to create a controller and methods responsible for displaying and processing the form on the server:

```java
@Controller
public class PassportController {

    @Autowired
    private PassportService passportService;

    @GetMapping("/passport")
    public String showPassport(Model model) {
        model.addAttribute("passport", new Passport());
        return "passport";
    }

    @PostMapping("/passport")
    public String savePassport(@ModelAttribute("passport") Passport passport) {
        // Data processing
        // For example, let's save them to the database

        passportService.savePassport(passport);

        return "redirect:/passport";
    }
}
```

In this example, we created a `PassportController` controller, which handles the GET request to `/passport` and is responsible for displaying the page. In the `showPassport` method, we create a `passport` object and pass it to the page. This object will be bound to our form, and its fields will contain the data entered by the user.

