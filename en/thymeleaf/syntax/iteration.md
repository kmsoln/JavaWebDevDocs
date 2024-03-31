# Thymeleaf Iteration

You can also use variables inside `th:each`. For example, if you have a list `fruits` containing several strings like "Apple", "Pineapple", "Watermelon", "Kiwi", you can use `th:each` to display all the elements of the list on the page:

```html
<div th:each="fruit: ${fruits}">
    <div th:text="${fruit}"></div>
</div>
```

In this example, if you have a list `fruits` with elements "Apple", "Pineapple", "Watermelon", "Kiwi", then the page will display:

```
Apple
Pineapple
Watermelon
Kiwi
```

Thus, you can use variables within Thymeleaf to control the content of web pages.

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)