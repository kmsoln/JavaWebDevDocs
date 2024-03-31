# Spring Forms

Как мы уже выяснили, формы в Thymeleaf создаются при помощи HTML тега `<form>`. Однако, мы не говорили о том как обрабатывать формы на сервере.

Для начала создадим простую форму с паспортными данными пользователя, которые он должен будет ввести

```html
<form th:action="@{/passport}" th:object="${passport}" method="post">
    <div>
        <label for="name">ФИО:</label>
        <input type="text" id="name" th:field="*{name}"/>
    </div>
    <div>
        <label for="dob">Дата рождения:</label>
        <input type="date" id="dob" th:field="*{dob}"/>
    </div>
    <div>
        <label for="passport">Паспорт:</label>
        <input type="text" id="passport" th:field="*{passport}"/>
    </div>
    <button type="submit">Отправить</button>
</form>
```

Как видим в нашей форме есть тег `th:object`, который связывает форму с объектом `passport`. Этот объект должен быть создан и передан на страницу из контроллера. Для каждого поля формы мы использовали атрибут `th:field`, чтобы связать поле с соответствующим полем объекта `passport`. После передачи формы, объект `passport` будет содержать данные, введенные пользователем.

Это мы уже знаем, но как это будет выглядеть на сервере? Для этого нам нужно создать контроллер и методы, которые будут отвечать за отображение и обработку формы на сервере:

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
        // работа с данными
        // например сохраним их в базу данных
        
        passportService.savePassport(passport);
        
        return "redirect:/passport";
    }
}
```

В этом примере мы создали контроллер `PassportController`, который обрабатывает GET запрос на `/passport` и отвечает за отображение страницы. В методе `showPassport` мы создаем объект `passport` и передаем его на страницу. Именно с ним будет связана наша форма и его поля будут содержать введенные пользователем данные.


