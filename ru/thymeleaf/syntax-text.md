# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)

# Текст в Thymeleaf

Чтобы создать текст на веб странице с использованием Thymeleaf, вам нужно использовать атрибут `th:text`. Этот атрибут позволяет вам установить текстовое значение для элемента.

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
<div th:text="'Hello, World!'"></div>
</body>
</html>
```

В этом примере мы установили текст "Hello, World!" для элемента `<div>`. Как видите, мы использовали одинарные кавычки, чтобы обернуть наш текст. Это нужно для того, чтобы Thymeleaf понимал, что это именно текст, а не какое-то выражение.

Также, к тексту можно применить форматирование, сделав его, например, курсивным или жирным:

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
<div th:text="'Hello, World!'" style="font-style: italic;"></div>
<div th:text="'Hello, World!'" style="font-weight: bold;"></div>
</body>
</html>
```

В этом примере мы добавили атрибут `style` для элементов `<div>`, чтобы сделать текст курсивным и жирным соответственно.

# [**Назад**: *Синтаксис Thymeleaf*](thymeleaf-syntax.md)