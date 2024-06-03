# Propagation level - NESTED

Уровень распространения `NESTED` означает, что текущий метод должен выполняться во вложенной транзакции. Если текущая
транзакция отсутствует, будет создана новая транзакция. Вложенная транзакция является частью родительской транзакции и
может быть сохранена или откатана независимо от родительской транзакции.

Например, у нас есть два сервиса: `ExampleService` и `AnotherService`. Метод `performOperation` в `ExampleService` вызывает
метод `nestedTransactionMethod` в `AnotherService`, который аннотирован уровнем распространения `NESTED`.

```java
@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.nestedTransactionMethod();
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.NESTED)
    public void nestedTransactionMethod() {
        // Логика, которая требует вложенной транзакции
    }
}
```

В этом примере `nestedTransactionMethod` в `AnotherService` требует вложенной транзакции. Метод `performOperation` в
`ExampleService` создает эту транзакцию, поскольку у него установлен уровень распространения `REQUIRED`. Если метод
`nestedTransactionMethod` вызывается без существующей транзакции (например, из метода без аннотации `@Transactional`), будет
создана новая вложенная транзакция.

В случае же вызова метода `nestedTransactionMethod` с существующей транзакцией, он будет выполняться в рамках этой вложенной
транзакции. Если вложенная транзакция завершается успешно, изменения будут сохранены в базе данных. Если же вложенная транзакция
завершается с ошибкой, она будет откатана, но родительская транзакция останется активной.

# [**Назад**: *Уровни распространения*](../propagation.md)


