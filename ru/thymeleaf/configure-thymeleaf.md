# Шаблонный движок Thymeleaf

Чтобы шаблонизатор работал корректно, а также, чтобы получить доступ к его тонким настройкам, нам необходимо создать его настройки
в проекте.
Для этого перейдем в ваш класс конфигуратор, где находятся все ваши [бины][beans], и добавим несколько новых бинов.

```java
    @Bean
    public ClassLoaderTemplateResolver templateResolver() {
        ClassLoaderTemplateResolver templateResolver = new ClassLoaderTemplateResolver();
        
        templateResolver.setPrefix("/templates/");
        templateResolver.setSuffix(".html");
        
        return templateResolver;
    }

    @Bean
    public SpringTemplateEngine templateEngine() {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver());
        
        return templateEngine;
    }

    @Bean
    public ViewResolver thymeleafViewResolver() {
        ThymeleafViewResolver resolver = new ThymeleafViewResolver();
        resolver.setTemplateEngine(templateEngine());
        
        return resolver;
    }
```

Разберем по порядку какие настройки мы определили в коде выше и зачем они нужны:
- `ClassLoaderTemplateResolver` - это класс, который позволяет нам указать, где искать наши шаблоны. В данном случае, мы указали
  что они будут находиться в папке `templates` в корне проекта. Также мы указали, что все наши шаблоны будут иметь расширение
  `.html`. Это можно изменить, если вам нужно работать с другими типами файлов.
- `SpringTemplateEngine` - это класс, который позволяет нам настроить наш шаблонизатор. Мы указали, что он будет использовать
  наш `templateResolver` для поиска шаблонов.
- `ThymeleafViewResolver` - это класс, который позволяет нам настроить наш шаблонизатор для работы с Spring. Мы указали, что он
  будет использовать наш `templateEngine` для обработки шаблонов.

# [**Следующий урок**: *Текст в Thymeleaf*](thymeleaf-syntax.md)

[beans]: beans.md
