# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)

# Формы в Thymeleaf

Формы в Thymeleaf создаются при помощи стандартного HTML-тега `<form>`. Однако, Thymeleaf позволяет вам использовать
дополнительные атрибуты для управления формой и отправки данных в виде POST-запроса:

Например, создадим форму паспортных данных пользователя, которая будет содержать данные о ФИО, дате рождения, серии и
номере паспорта:

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

В этом примере мы создали форму, которая отправляет POST запрос на `/passport`. Также, мы использовали
атрибут `th:object`, чтобы связать форму с объектом `passport`, который будет содержать данные формы и должен быть
создан и передан на страницу из контроллера. Для каждого поля формы мы использовали атрибут `th:field`, чтобы связать
поле с соответствующим полем объекта `passport`. После передачи формы, объект `passport` будет содержать данные,
введенные пользователем.

Рассмотрим подробнее синтаксис Thymeleaf выражений в коде выше:

- `th:action="@{/passport}"` - атрибут `th:action` указывает на адрес, на который будет отправлен POST запрос. В данном
  случае, это `/passport`.
- `th:object="${passport}"` - атрибут `th:object` связывает форму с объектом `passport`. Этот объект должен быть создан
  и передан на страницу из контроллера.
- `th:field="*{name}"` - атрибут `th:field` связывает поле формы с полем объекта `passport`. В данном случае,
  поле `name` объекта `passport` будет содержать значение поля формы с id `name`.
- `th:field="*{dob}"` - атрибут `th:field` связывает поле формы с полем объекта `passport`. В данном случае, поле `dob`
  объекта `passport` будет содержать значение поля формы с id `dob`.
- `th:field="*{passport}"` - атрибут `th:field` связывает поле формы с полем объекта `passport`. В данном случае,
  поле `passport` объекта `passport` будет содержать значение поля формы с id `passport`.

Также можно использовать аттрибут `th:value` для установки значения поля из данных переданных из контроллера:

```html
<form th:action="@{/passport}" th:object="${passport}" method="post">
    <div>
        <label for="name">ФИО:</label>
        <input type="text" id="name" th:field="*{name}" th:value="${passport.name}"/>
    </div>
    <div>
        <label for="dob">Дата рождения:</label>
        <input type="date" id="dob" th:field="*{dob}" th:value="${passport.dob}"/>
    </div>
    <div>
        <label for="passport">Паспорт:</label>
        <input type="text" id="passport" th:field="*{passport}" th:value="${passport.passport}"/>
    </div>
    <button type="submit">Отправить</button>
</form>
```

# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)
