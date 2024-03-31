# Blocks in Thymeleaf

Blocks in Thymeleaf are used to insert fragments of HTML templates into other HTML templates. They allow you to create templates that can be reused in different parts of your application. For example, if you have a `header.html` template containing the top part of the page, and a `footer.html` template containing the bottom part of the page, you can use these templates in other HTML templates:

```html
<div th:insert="~{header}"></div>
<div>
    <p>Content</p>
</div>
<div th:insert="~{footer}"></div>
```

In this example, we used `th:insert` to insert fragments of the `header.html` and `footer.html` templates into the current HTML template. Note that we used `~{...}` to specify that this is a template fragment. You can read more about Thymeleaf standard expressions in the [Thymeleaf Standard Expressions](syntax-simple-expressions.md) section.

In addition to the `th:insert` attribute, there are other attributes that allow you to insert template fragments:
- `th:replace` - replaces the content of the element with the content of the template fragment
- `th:substituteby` - replaces the current element with the content of the template fragment
- `th:fragment` - defines a template fragment
- `th:remove` - removes the current element
- `th:include` - inserts the content of the template fragment into the current element (deprecated in Thymeleaf 3, use `th:insert`)

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)