# Синтаксис Thymeleaf

Синтаксические конструкции Thymeleaf используются для встраивания динамического контента в HTML-шаблоны. Они зачастую пишутся в атрибутах HTML-тегов и позволяют вам взаимодействовать с данными, передаваемыми из контроллера на страницу.

Обычно выражения Thymeleaf начинаются с префикса `th:`. Например, `th:text`, `th:if`, `th:each` и т.д. 

Основные конструкции Thymeleaf:
- `th:text` - устанавливает текстовое содержимое тега [Текст в Thymeleaf][thymeleaf-text]
- Переменные - вставка переменных в текст [Переменные в Thymeleaf][thymeleaf-variables]
- `th:if` - условный оператор [Условный оператор в Thymeleaf][thymeleaf-if]
- `th:each` - цикл [Цикл в Thymeleaf][thymeleaf-each]
- `th:block` - создание блоков [Блоки в Thymeleaf][thymeleaf-code-blocks]

[thymeleaf-text]: syntax-text
[thymeleaf-variables]: syntax-variables
[thymeleaf-if]: syntax-conditional-themeleaf.md
[thymeleaf-each]: syntax-iteration
[thymeleaf-code-blocks]: thymeleaf-code-blocks
