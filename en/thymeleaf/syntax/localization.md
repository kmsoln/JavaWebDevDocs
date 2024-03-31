# Localization in Thymeleaf

Localization is the process of adapting software to different languages and regional standards. Web applications also need to be localized to be accessible to users from different countries. Thymeleaf provides the ability to localize your HTML templates using localization files.

Localization is configured in the `application.properties` file:

```properties
spring.messages.basename=messages
```

In this example, we specified that the localization files will be located in the project root and named `messages.properties`. Now, let's create a localization file `messages.properties` in the project root. Since the file is not language-specific, it will be used as a default if a file for the desired language is not found. In the `messages.properties` file, let's add a message:

```properties
hello=Hello, World!
```

As we can see, we added a message called `hello` with the value "Hello, World!". Now, we can use this message in an HTML template as follows:

```html
<div th:text="#{hello}"></div>
```

In this example, "Hello, World!" will be displayed on the page. Note that `#{...}` is used as a special character to refer to the message. The reason for this is explained [here](syntax-simple-expressions).

If you need to localize this message in another language, you need to create a localization file for that language. For example, for the Russian language, you need to create a file `messages_ru.properties` and add the message there:

```properties
hello=Привет, Мир!
```

Now, if a user requests the page in Russian, the `messages_ru.properties` file will be used, and "Привет, Мир!" will be displayed on the page.

# [**Back**: *Thymeleaf Syntax*](thymeleaf-syntax.md)