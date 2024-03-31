# Variables in Thymeleaf

In Thymeleaf, you can use variables to insert dynamic data into HTML templates. Variables are commonly used in attributes such as `th:text`, `th:value`, `th:href`, and others where value insertion is required.

For example, if you have a variable named `name`, you can use it inside the `th:text` attribute like this:

```html
<div th:text="${name}"></div>
```

In this example, if you have a variable `name` with the value "Denis", then "Denis" will be displayed on the page.

To make variables available in the template, you need to pass them from the controller. [Passing Variables from Controller to Thymeleaf](send-data-to-controller.md).

You can also declare variables directly within the template using the `th:with` attribute:

```html
<div th:with="name='Denis'" th:text="${name}"></div>
```

In this example, we created a variable named `name` with the value "Denis" and used it inside the `th:text` attribute.

Thymeleaf usually determines the data type of the variable automatically. For example, it will understand whether the variable contains a string, number, or another data type. For example, let's create a variable containing a number and display it on the page:

```html
<div th:with="number=5" th:text="${number}"></div>
```

In this example, we created a variable `number` with the value 5 and displayed it on the page.

Using variables makes templates more dynamic and allows you to easily insert various data into your HTML pages.

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)