# Conditions in Thymeleaf

Conditions in Thymeleaf allow you to embed dynamic content into your HTML templates based on certain conditions.

There are several types of conditional operators in Thymeleaf that allow you to check various conditions and embed content based on their results:
- `th:if` - embeds content if the condition is true
- `th:unless` - embeds content if the condition is false
- `th:switch` - analogous to the `switch` operator in Java

Conditions use standard comparison operators with some enhancements:
- `==` - equals, cannot be used to compare string content, only for primitive types
- `!=` - not equal
- `<` - less than
- `>` - greater than
- `<=` - less than or equal to
- `>=` - greater than or equal to
- `and` or `&&` - logical "and", used between conditions to check both
- `or` or `||` - logical "or", used between conditions to check at least one of them
- `not` - logical "not", used before a condition to check its negation
- `empty` - checks if a variable or collection is empty
- `!empty` - checks if a variable or collection is not empty
- `isEven` - checks if a number is even
- `isOdd` - checks if a number is odd
- `isDivisibleBy` - checks if a number is divisible by another without remainder
- `isNotDivisibleBy` - checks if a number is not divisible by another without remainder
- `matches` - checks if a string matches a regular expression
- `startsWith` - checks if a string starts with a specified substring
- `endsWith` - checks if a string ends with a specified substring
- `contains` - checks if a string contains a specified substring
- `equals` - checks if two strings are equal
- `equalsIgnoreCase` - checks if two strings are equal regardless of case
- there are more, but these are the basics

Here's a simple example of using `if` and `unless` conditions in Thymeleaf, where we check that a variable is not equal to 5, and if this condition is true, we display the message "Variable is not equal to 5"; otherwise, we display the message "Variable is equal to 5":

```html
<div th:if="${variable != 5}">
    <p>Variable is not equal to 5</p>
</div>
<div th:unless="${variable != 5}">
    <p>Variable is equal to 5</p>
</div>
```

In this example, we used `th:if` and `th:unless` to check conditions and embed content based on their results. Also, instead of `th:unless`, you can use `th:else` to embed content if the condition is false:

```html
<div th:if="${variable != 5}">
    <p>Variable is not equal to 5</p>
</div>
<div th:else>
    <p>Variable is equal to 5</p>
</div>
```

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)