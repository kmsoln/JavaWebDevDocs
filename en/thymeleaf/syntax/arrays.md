# Arrays in Thymeleaf

In Thymeleaf, you can use arrays to work with data. For example, let's create an array of strings as a variable, add some values to it, and display them on the page:

```html
<div th:with="names=${{'Denis', 'Karim', 'Danil'}}">
    <div th:each="name : ${names}">
        <p th:text="${name}"></p>
    </div>
</div>
```

In this example, we created an array `names` containing the strings "Denis", "Karim", and "Danil", and displayed them on the page using `th:each`. As a result, the following will be displayed on the page:

```
Denis
Karim
Danil
```

Thus, you can use arrays in Thymeleaf to work with data and manage the content of web pages.

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)