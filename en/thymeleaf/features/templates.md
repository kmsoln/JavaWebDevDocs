# Thymeleaf Templates

Thymeleaf is a templating engine that allows you to create web pages using HTML, CSS, and JavaScript. It enables you to interact with data passed from the controller to the page.

A template is the primary unit in Thymeleaf. It is an HTML file that contains both static content and dynamic data. Templates are used to create web pages that can be utilized in various parts of your application.

For example, suppose you have a page that displays user information:

```html
<!DOCTYPE html>
<html>
<head>
    <title>User Profile</title>
</head>
<body>
    <h1>User Profile</h1>
    <p>Name: Denis</p>
    <p>Surname: Doe</p>
    <p>Age: 25</p>
</body>
</html>
```

Currently, this is just a page that has no connection to Thymeleaf. Let's turn it into a Thymeleaf template to make the data dynamic:

```html
<!DOCTYPE html>
<html>
<head>
    <title>User Profile</title>
</head>
<body>
    <h1>User Profile</h1>
    <p>Name: <span th:text="${name}"></span></p>
    <p>Surname: <span th:text="${surname}"></span></p>
    <p>Age: <span th:text="${age}"></span></p>
</body>
</html>
```

As we can see, we are using Thymeleaf expressions starting with `th:`. These are Thymeleaf expressions that allow you to interact with data passed from the controller to the page. We'll discuss them later, but the main point is that a template is a regular HTML file containing static content and dynamic data created using Thymeleaf expressions.

# [**Back to: Thymeleaf Syntax**](syntax.md)