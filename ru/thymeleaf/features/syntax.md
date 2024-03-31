# Синтаксис Thymeleaf

Для понимания дальнейшей информации, рекомендуется уже понимать что такое шаблон Thymeleaf и как его использовать. Если вы не знакомы с этим, рекомендуется прочитать [шаблоны](thymeleaf-templates.md).

Синтаксические конструкции Thymeleaf используются для встраивания динамического контента в HTML-шаблоны. Они зачастую пишутся в атрибутах HTML-тегов и позволяют вам взаимодействовать с данными, передаваемыми из контроллера на страницу.

Обычно выражения Thymeleaf начинаются с префикса `th:`. Например, `th:text`, `th:if`, `th:each` и т.д. 

Основные конструкции Thymeleaf:
- `th:text` - устанавливает текстовое содержимое тега [Текст в Thymeleaf][thymeleaf-text]
-  Переменные - вставка переменных в текст [Переменные в Thymeleaf][thymeleaf-variables]
- `th:if` - условный оператор [Условный оператор в Thymeleaf][thymeleaf-if]
- `th:each` - цикл [Циклы в Thymeleaf][thymeleaf-each]
-  Массивы и списки [Массивы и списки в Thymeleaf][thymeleaf-arrays]
-  Template Layout [Блоки в Thymeleaf][thymeleaf-code-blocks]
-  Ссылки и URL [Ссылки и URL в Thymeleaf][thymeleaf-links]
-  Стандартные выражения Thymeleaf [Стандартные выражения Thymeleaf][thymeleaf-standard-expressions]
-  Сообщение из файла локализации [Сообщения из файла локализации в Thymeleaf][thymeleaf-messages]
-  Формы - обработка форм [Формы в Thymeleaf][thymeleaf-forms]
- Форматирование данных [Форматирование][thymeleaf-formatting]

[thymeleaf-text]: ../syntax/syntax-text.md
[thymeleaf-variables]: ../syntax/syntax-variables.md
[thymeleaf-if]: ../syntax/syntax-conditional-themeleaf.md
[thymeleaf-each]: ../syntax/syntax-iteration.md
[thymeleaf-arrays]: ../syntax/syntax-arrays.md
[thymeleaf-code-blocks]: ../thymeleaf-code-blocks.md
[thymeleaf-links]: ../syntax/syntax-links.md
[thymeleaf-standard-expressions]: ../syntax/syntax-simple-expressions.md
[thymeleaf-messages]: ../syntax/syntax-messages.md
[thymeleaf-forms]: ../syntax/syntax-forms.md
[thymeleaf-formatting]: ../syntax/syntax-formatting.md

# [**Следующий урок**: *Thymeleaf и Spring*](../thymeleaf-spring.md)
