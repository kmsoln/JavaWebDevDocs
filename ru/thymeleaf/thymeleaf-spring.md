# Thymeleaf и Spring

Мы разобрали основные синтаксические элементы Thymeleaf, но как это все связано с Spring? В этом уроке мы рассмотрим, как использовать Thymeleaf вместе с Spring.

Логика работы Thymeleaf в Spring основана на взаимодействии контроллеров Spring с Thymeleaf-шаблонами. Контроллеры обрабатывают запросы и возвращают Thymeleaf-шаблоны, которые затем отображаются на веб-странице. Как вы уже знаете, контроллеры могут передавать данные на веб страницу с помощью модели. С помощью синтаксических конструкций Thymeleaf, которые мы разбирали ранее, мы можем работать с этими данными на странице.

Простой пример. Предположим, что у нас есть контроллер, который передает паспортные данные пользователя из базы данных на веб-страницу. Мы можем использовать Thymeleaf для отображения этих данных на странице. Вот пример контроллера:

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

В этом примере мы создали контроллер `PassportController`, который обрабатывает GET запрос на `/passport`. В методе `showPassport` мы получаем паспортные данные пользователя из сервиса `PassportService` и передаем их на страницу с помощью модели.

Теперь давайте создадим Thymeleaf-шаблон, который будет отображать паспортные данные на странице. Вот пример шаблона `passport.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Паспортные данные</title>
</head>
<body>
    <h1>Паспортные данные</h1>
    <p>ФИО: <span th:text="${passport.name}"></span></p>
    <p>Дата рождения: <span th:text="${passport.dob}"></span></p>
    <p>Паспорт: <span th:text="${passport.passport}"></span></p>
</body>
</html>
```

В этом примере мы создали Thymeleaf-шаблон, который отображает паспортные данные пользователя. Мы используем синтаксические конструкции Thymeleaf для отображения данных, переданных из контроллера.

Теперь, когда пользователь отправит GET запрос на `/passport`, контроллер вернет Thymeleaf-шаблон `passport.html`, который отобразит паспортные данные на странице.

# [**Следующий урок**: *Валидация*](validation.md)
