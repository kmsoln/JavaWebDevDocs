# [**Back to**: *Thymeleaf Syntax*](thymeleaf-syntax.md)

# Formatting Data in Thymeleaf

Thymeleaf provides the ability to format data that you output on the page. For example, you can format dates, times, numbers, and money. In this lesson, we'll look at how to use data formatting in Thymeleaf.

## Formatting Dates and Times

To format a date or time, you can use the `th:text` attribute along with the formatting method. For example, if you have a date that you want to format, you can use the `#dates.format` method:

```html
<p th:text="${#dates.format(date, 'dd.MM.yyyy')}"></p>
```

In this example, we use the `#dates.format` method to format the date from the `date` variable in the `dd.MM.yyyy` format. This method takes two arguments: the date and the formatting pattern. In this case, the formatting pattern `dd.MM.yyyy` means that the date will be formatted as `day.month.year`.

You can also use the `#dates.format` method to format time:

```html
<p th:text="${#dates.format(time, 'HH:mm:ss')}"></p>
```

In this example, we use the `#dates.format` method to format the time from the `time` variable in the `HH:mm:ss` format. This method takes two arguments: the time and the formatting pattern. In this case, the formatting pattern `HH:mm:ss` means that the time will be formatted as `hours:minutes:seconds`.

## Formatting Numbers and Money

To format a number or money, you can use the `th:text` attribute along with the formatting method. For example, if you have a number that you want to format, you can use the `#numbers.format` method:

```html
<p th:text="${#numbers.format(number, '0,0')}"></p>
```

In this example, we use the `#numbers.format` method to format the number from the `number` variable in the `0,0` format. This method takes two arguments: the number and the formatting pattern. In this case, the formatting pattern `0,0` means that the number will be formatted as `1,000`.

You can also use the `#numbers.format` method to format money:

```html
<p th:text="${#numbers.format(money, '0,0.00')}"></p>
```

In this example, we use the `#numbers.format` method to format the money from the `money` variable in the `0,0.00` format. This method takes two arguments: the money and the formatting pattern. In this case, the formatting pattern `0,0.00` means that the money will be formatted as `1,000.00`.

---

# [**Back to**: *Thymeleaf Syntax*](../features/syntax.md)