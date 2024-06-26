# [**Назад**: *Синтаксис Thymeleaf*](features/thymeleaf-syntax.md)

# Шаблоны Thymeleaf

Thymeleaf - это шаблонизатор, который позволяет вам создавать веб-страницы с использованием HTML, CSS и JavaScript. Он позволяет вам взаимодействовать с данными, передаваемыми из контроллера на страницу

Шаблон - основная единица в Thymeleaf. Он представляет собой HTML-файл, который содержит в себе статический контент и динамические данные. Шаблоны используются для создания веб-страниц, которые могут быть использованы в разных местах вашего приложения.

Например, у вас есть страница, которая содержит информацию о пользователе:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Профиль пользователя</title>
</head>
<body>
    <h1>Профиль пользователя</h1>
    <p>Имя: Денис</p>
    <p>Фамилия: Doe</p>
    <p>Возраст: 25</p>
</body>
</html>
```

Сейчас это просто страница, которая ничего общего с Thymeleaf не имеет. Давайте превратим ее в шаблон Thymeleaf, чтобы данные на ней стали динамическими:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Профиль пользователя</title>
</head>
<body>
    <h1>Профиль пользователя</h1>
    <p>Имя: <span th:text="${name}"></span></p>
    <p>Фамилия: <span th:text="${surname}"></span></p>
    <p>Возраст: <span th:text="${age}"></span></p>
</body>
</html>
```

Как видим, мы используем, пока что нам непонятные конструкции, которые начинаются с `th:`. Это и есть выражения Thymeleaf, которые позволяют вам взаимодействовать с данными, передаваемыми из контроллера на страницу. О них мы поговорим позже, главное понимание, того, что шаблон - это обычный HTML-файл, который содержит в себе статический контент и динамические данные, которые создаются при помощи выражений Thymeleaf.

# [**Назад**: *Синтаксис Thymeleaf*](features/thymeleaf-syntax.md)