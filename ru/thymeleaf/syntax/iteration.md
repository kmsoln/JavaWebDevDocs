# [**Назад**: *Синтаксис Thymeleaf*](../features/thymeleaf-syntax.md)

# Цикл each в Thymeleaf

Также, вы можете использовать переменные внутри `th:each`. Например, если у вас есть список `fruits`, в котором находится несколько строк "Apple", "Pineapple", "Watermelon", "Kiwi", вы можете использовать `th:each` для того, чтобы вывести все элементы списка на странице:

```html
<div th:each="fruit: ${fruits}">
    <div th:text="fruit"></div>
</div>
```

В этом примере, если у вас есть список `fruits` с элементами "Apple", "Pineapple", "Watermelon", "Kiwi", то на странице будет выведено:

```
Apple
Pineapple
Watermelon
Kiwi
```

Таким образом, вы можете использовать переменные внутри Thymeleaf, чтобы управлять содержимым веб страницы.

# [**Назад**: *Синтаксис Thymeleaf*](../features/thymeleaf-syntax.md)