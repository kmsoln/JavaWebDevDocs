# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)

# Цикл each в Thymeleaf

Также, вы можете использовать переменные внутри `th:each`. Например, если у вас есть список `fruits`, вы можете использовать его внутри `th:each`:

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
<div th:each="fruit: ${fruits}">
    <div th:text="fruit"></div>
</div>
</body>
</html>
```

В этом примере, если у вас есть список `fruits` с элементами "Apple", "Pineapple", "Watermelon", "Kiwi", то на странице будет выведено:

```
Apple
Pineapple
Watermelon
Kiwi
```

Таким образом, вы можете использовать переменные внутри Thymeleaf, чтобы управлять содержимым веб страницы.

# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)