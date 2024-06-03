# Propagation level - REQUIRED

Уровень распространения `REQUIRED` означает, что текущий метод должен выполняться в рамках существующей транзакции. Если
текущая транзакция отсутствует, будет создана новая. Этот уровень распространения обеспечивает атомарность операций,
предотвращая нежелательные изменения в базе данных в случае возникновения ошибок.

Например, у нас есть два сервиса: `ExampleService` и `AnotherService`. Метод `performOperation` в `ExampleService` вызывает
метод `requiredTransactionMethod` в `AnotherService`, который аннотирован уровнем распространения `REQUIRED`.

```java
@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.requiredTransactionMethod();
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.REQUIRED)
    public void requiredTransactionMethod() {
        // Логика, которая требует существования транзакции
    }
}
```

В этом примере `requiredTransactionMethod` в `AnotherService` требует существующей транзакции. Метод `performOperation` в
`ExampleService` создает эту транзакцию, поскольку у него установлен уровень распространения `REQUIRED`. Если метод
`requiredTransactionMethod` вызывается без существующей транзакции (например, из метода без аннотации `@Transactional`), будет
создана новая транзакция.

В случае же вызова метода `requiredTransactionMethod` с существующей транзакцией, он будет выполняться в рамках этой транзакции и
новая транзакция создана не будет.

# [**Назад**: *Уровни распространения*](../propagation.md)
