# Thymeleaf Standard Expressions

Thymeleaf Standard Expressions are used to insert data into HTML templates. They allow you to interact with data passed from the controller to the page.

Standard expressions are typically written within brackets, using a special character before them:
- `${...}` - for inserting variables. For example, `${name}` is an expression containing the variable `name`.
- `*{...}` - for inserting objects. For example, `*{user.name}` is an expression containing the `user` object and accessing its `name` property.
- `#{...}` - for inserting messages from localization files. For example, `#{message}` is an expression containing the message `message`.
- `@{...}` - for inserting URLs. For example, `@{url}` is an expression containing the URL `url`.
- `~{...}` - for inserting template fragments. For example, `~{fragment}` is an expression containing the fragment `fragment`.

Examples of using standard expressions in practice:

```html
<div th:text="${name}"></div>
<div th:text="*{user.name}"></div>
<div th:text="#{message}"></div>
<a th:href="@{url}">Link</a>
<div th:insert="~{fragment}"></div>
```

In this example, we used all standard Thymeleaf expressions:
- `${name}` - inserts the variable `name`.
- `*{user.name}` - inserts the `name` property of the `user` object.
- `#{message}` - inserts a message from a localization file.
- `@{url}` - inserts a URL that can be clicked to navigate to it.
- `~{fragment}` - inserts a template fragment located in the `fragment.html` file.

Expressions can be combined to achieve the desired result. For example, you can use `${...}` together with `*{...}`:

```html
<div th:text="*{user.name} + ' ' + ${user.surname}"></div>
```

In this example, we used the expression `*{user.name}` to insert the `name` property of the `user` object, and the expression `${user.surname}` to insert the `surname` variable. Thus, the name and surname of the user will be displayed on the page.

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)