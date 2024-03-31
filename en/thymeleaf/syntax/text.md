# Text in Thymeleaf

To create text on a web page using Thymeleaf, you can use the `th:text` attribute. This attribute allows you to set a text value for an element.

```html
<div th:text="'Hello, World!'"></div>
```

In this example, we set the text "Hello, World!" for the `<div>` element. Note that the text is enclosed in single quotes. This allows Thymeleaf to interpret the text as a string.

You can also use the `th:utext` attribute for text that contains HTML tags:

```html
<div th:utext="'Hello, <b>World</b>!'"></div>
```

In this example, we used `th:utext` to allow the use of HTML tags within the text. Thus, the page will display "Hello, **World**!".

These attributes allow you to easily manage the displayed text on a web page using Thymeleaf.

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)