# Настройка Thymeleaf в Spring MVC

Для настройки Thymeleaf в Spring MVC нам необходимо создать конфигурацию шаблонизатора, который будет обрабатывать
представления Thymeleaf. В этом уроке мы рассмотрим, как настроить Thymeleaf в Spring MVC, чтобы использовать его в
веб-приложениях.

```java

@EnableWebMvc
@ComponentScan(basePackages = "com.example")
public class WebConfig implements WebMvcConfigurer {

    @Bean
    public SpringResourceTemplateResolver templateResolver() {
        SpringResourceTemplateResolver templateResolver = new SpringResourceTemplateResolver();
        templateResolver.setPrefix("/WEB-INF/templates/");
        templateResolver.setSuffix(".html");
        templateResolver.setTemplateMode("HTML5");
        templateResolver.setCharacterEncoding("UTF-8");
        return templateResolver;
    }

    @Bean
    public SpringTemplateEngine templateEngine() {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver());
        templateEngine.setEnableSpringELCompiler(true);
        return templateEngine;
    }

    @Bean
    public ThymeleafViewResolver viewResolver() {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
        viewResolver.setTemplateEngine(templateEngine());
        viewResolver.setCharacterEncoding("UTF-8");
        return viewResolver;
    }
}
```

### SpringResourceTemplateResolver:

Это компонент, который отвечает за нахождение и чтение шаблонов (HTML файлов) для Thymeleaf.
setPrefix("/WEB-INF/templates/"): Указывает, что все шаблоны будут находиться в папке /WEB-INF/templates/.
setSuffix(".html"): Указывает, что все шаблоны будут иметь расширение .html.
setTemplateMode("HTML5"): Задает режим шаблонов как HTML5.
setCharacterEncoding("UTF-8"): Устанавливает кодировку символов как UTF-8.

### SpringTemplateEngine:

Это основной класс для обработки шаблонов Thymeleaf.
setTemplateResolver(templateResolver()): Устанавливает ранее созданный templateResolver как резольвер шаблонов.
setEnableSpringELCompiler(true): Включает поддержку Spring Expression Language (SpEL), позволяя использовать выражения
SpEL внутри шаблонов.

### ThymeleafViewResolver

Этот компонент отвечает за отображение представлений (views) с использованием Thymeleaf.
setTemplateEngine(templateEngine()): Устанавливает ранее созданный templateEngine как движок шаблонов.
setCharacterEncoding("UTF-8"): Устанавливает кодировку символов для представлений как UTF-8.