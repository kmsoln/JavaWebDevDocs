# Валидация данных в Thymeleaf

В Thymeleaf вы можете использовать встроенные атрибуты для валидации данных. Это позволяет вам проверить данные, введенные пользователем, и если данные не прошли проверку, указать на это пользователю. 

Для валидации данных в HTML обычно используется атрибут `required`, `min`, `max`, `pattern` и другие. В Thymeleaf вы можете использовать эти атрибуты, а также дополнительные атрибуты, которые позволяют вам проверить данные на сервере.

Например, создадим форму ввода паспортных данных, пользователь будет вводить ФИО, возраст, серию и номер паспорта. Реализуем валидацию, которая проверит, что серия содержит ровно 4 цифры, номер ровно 6, а возраст больше 18 лет:

```html
<form th:action="@{/passport}" th:object="${passport}" method="post">
    <div>
        <label for="name">ФИО:</label>
        <input type="text" id="name" th:field="*{name}" required/>
    </div>
    <div>
        <label for="age">Возраст:</label>
        <input type="number" id="age" th:field="*{age}" required min="18"/>
    </div>
    <div>
        <label for="passport">Паспорт:</label>
        <input type="text" id="passport" th:field="*{passport}" required pattern="[0-9]{4} [0-9]{6}"/>
    </div>
    <button type="submit">Отправить</button>
</form>
```

В этом примере мы использовали атрибуты `required`, `min` и `pattern` для валидации данных. Однако, эти атрибуты проверяют данные только на клиентской стороне, их можно обойти, отключив JavaScript. Хорошие приложения используют не только клиентскую валидацию, но и серверную. Для этого в Thymeleaf есть дополнительные атрибуты, которые позволяют вам проверить данные на сервере:

Например аттрибуты `th:field` и `th:errors`:

```html
<form th:action="@{/passport}" th:object="${passport}" method="post">
    <div>
        <label for="name">ФИО:</label>
        <input type="text" id="name" th:field="*{name}" required/>
        <span th:if="${#fields.hasErrors('name')}" th:errors="*{name}">Неверное значение</span>
    </div>
    <div>
        <label for="age">Возраст:</label>
        <input type="number" id="age" th:field="*{age}" required min="18"/>
        <span th:if="${#fields.hasErrors('age')}" th:errors="*{age}">Неверное значение</span>
    </div>
    <div>
        <label for="passport">Паспорт:</label>
        <input type="text" id="passport" th:field="*{passport}" required pattern="[0-9]{4} [0-9]{6}"/>
        <span th:if="${#fields.hasErrors('passport')}" th:errors="*{passport}">Неверное значение</span>
    </div>
    <button type="submit">Отправить</button>
</form>
```

В этом примере мы использовали атрибуты `th:if` и `th:errors`, которые позволяют вам проверить данные на сервере и вывести сообщение об ошибке, если данные не прошли проверку.