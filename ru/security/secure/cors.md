# Кросс-доменное взаимодействие ресурсов (CORS):

В мире веб-разработки возникает потребность в обмене данными между веб-страницами и серверами на разных доменах. Однако безопасность браузера по умолчанию блокирует такие запросы из соображений безопасности. Здесь на помощь приходит механизм кросс-доменного взаимодействия ресурсов (CORS), который позволяет веб-страницам получать доступ к ресурсам с других источников, соблюдая правила безопасности. Давайте более подробно рассмотрим, что такое CORS, как он работает, и как его можно реализовать в веб-приложениях на Java.

## Что такое CORS?

CORS - это механизм веб-безопасности, который позволяет веб-страницам запрашивать ресурсы с других доменов в браузере пользователя. Браузер по умолчанию блокирует такие запросы из-за политики безопасности, но с помощью CORS сервер может сообщить браузеру, что запросы с определенных источников разрешены.

## Как это работает?

Когда веб-страница пытается сделать запрос на ресурс с другого домена, браузер добавляет дополнительные HTTP-заголовки в запрос, чтобы сервер мог понять, откуда пришел запрос. Затем сервер анализирует эти заголовки и, в случае разрешения, возвращает дополнительные заголовки в ответе, разрешающие браузеру продолжить запрос.

## Примеры Реализации CORS на Java

Рассмотрим несколько примеров реализации CORS в веб-приложениях на Java с использованием Spring Framework.

### Пример 1: Конфигурация CORS в Spring Boot

```java
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

    @CrossOrigin(origins = "http://example.com")
    @GetMapping("/hello")
    public String helloWorld() {
        return "Hello, World!";
    }
}
```
В этом примере мы использовали аннотацию @CrossOrigin, чтобы разрешить запросы с источника "http://example.com" к нашему эндпоинту "/hello".
### Пример 2: Глобальная Конфигурация CORS в Spring Boot
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://example.com")
                .allowedMethods("GET", "POST")
                .allowedHeaders("*");
    }
}
```
Этот пример демонстрирует глобальную конфигурацию CORS для всех эндпоинтов, разрешая запросы только с источника "http://example.com" и разрешая методы GET и POST.

### Пример 3: Конфигурация CORS через фильтр в Spring Boot
```java
import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class CorsFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        HttpServletResponse httpResponse = (HttpServletResponse) response;
        HttpServletRequest httpRequest = (HttpServletRequest) request;

        httpResponse.setHeader("Access-Control-Allow-Origin", "http://example.com");
        httpResponse.setHeader("Access-Control-Allow-Methods", "GET, POST");
        httpResponse.setHeader("Access-Control-Allow-Headers", "*");

        chain.doFilter(request, response);
    }

    // Другие методы интерфейса Filter
}

```
Этот пример показывает создание фильтра для конфигурации CORS, который добавляет необходимые заголовки в ответ для разрешения запросов с источника "http://example.com" и определения разрешенных методов и заголовков.

# [ДАЛЕЕ: Безопасность](protection.md)