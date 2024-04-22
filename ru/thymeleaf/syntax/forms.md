# [**Назад**: *Синтаксис Thymeleaf*](../features/thymeleaf-syntax.md)

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
## Работа с датами и временем в формах Thymeleaf
Форматы даты и времени часто становятся источником ошибок в веб-приложениях, поэтому важно понимать, как правильно их использовать в Thymeleaf.

Примеры использования поля даты
```
Поле даты (<input type="date">) используется для ввода дат. В Thymeleaf для корректной работы с датами можно использовать дополнительные библиотеки, такие как java.time.LocalDate, которые легко интегрируются с Thymeleaf:
```

```html
<div>
    <label for="dob">Дата рождения:</label>
    <input type="date" id="dob" th:field="*{dob}" pattern="\d{4}-\d{2}-\d{2}" placeholder="yyyy-mm-dd"/>
</div>
```
### Локализация и форматирование
Для поддержки различных форматов дат в зависимости от локализации пользователя, Thymeleaf позволяет легко интегрировать функциональность форматирования дат, используя #dates utility object для форматирования и парсинга дат в шаблонах:

```html
<div>
    <label for="dob">Дата рождения:</label>
    <input type="text" id="dob" th:value="${#dates.format(passport.dob, 'dd.MM.yyyy')}" th:field="*{dob}"/>
</div>
```
Этот код устанавливает значение поля ввода даты в соответствии с форматом dd.MM.yyyy, что особенно полезно, если данные о дате рождения поступают из различных источников в разных форматах.

### Валидация даты
Валидация даты также важна для обеспечения корректности данных. Thymeleaf позволяет легко интегрировать валидацию на стороне сервера:

```html
<div>
    <label for="dob">Дата рождения:</label>
    <input type="date" id="dob" th:field="*{dob}" required />
</div>
```
Атрибут required гарантирует, что пользователь не сможет отправить форму без заполнения поля даты рождения.
# [**Назад**: *Синтаксис Thymeleaf*](../features/thymeleaf-syntax.md)
