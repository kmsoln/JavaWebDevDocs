# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)

# Стандартные выражения Thymeleaf

Стандартные выражения Thymeleaf используются для вставки данных в HTML-шаблоны. Они позволяют вам взаимодействовать с данными, передаваемыми из контроллера на страницу.

Стандартные выражения обычно пишутся в скобках, с использованием спецсимвола перед ними:
- `${...}` - для вставки переменных. Например `${name}` - выражение, которое содержит переменную `name`
- `*{...}` - для вставки объектов. Например `*{user.name}` - выражение, которое содержит объект `user` и из него вызывается свойство `name`
- `#{...}` - для вставки сообщений из файла локализации. Например `#{message}` - выражение, которое содержит сообщение `message`
- `@{...}` - для вставки URL. Например `@{url}` - выражение, которое содержит URL `url`
- `~{...}` - для вставки фрагментов шаблона. Например `~{fragment}` - выражение, которое содержит фрагмент `fragment`

Примеры использования стандартных выражений на практике:

```html
<div th:text="${name}"></div>
<div th:text="*{user.name}"></div>
<div th:text="#{message}"></div>
<a th:href="@{url}">Link</a>
<div th:insert="~{fragment}"></div>
```

В этом примере мы использовали все стандартные выражения Thymeleaf:
- `${name}` - вставляет переменную `name`
- `*{user.name}` - вставляет свойство `name` объекта `user`
- `#{message}` - вставляет сообщение из файла локализации
- `@{url}` - вставляет URL, на который можно перейти кликнув на этот элемент
- `~{fragment}` - вставляет фрагмент шаблона, который находится в файле `fragment.html`

Выражения можно комбинировать между собой, чтобы получить нужный результат. Например, вы можете использовать выражение `${...}` вместе с выражением `*{...}`:

```html
<div th:text="*{user.name} + ' ' + ${user.surname}"></div>
```

В этом примере мы использовали выражение `*{user.name}` для вставки свойства `name` объекта `user`, и выражение `${user.surname}` для вставки переменной `surname`. Таким образом, на странице будет выведено имя и фамилия пользователя.

# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)