# Уровень распространения MANDATORY

Уровень распространения `MANDATORY` гарантирует, что текущий метод должен выполняться в рамках существующей транзакции.
Если текущая транзакция отсутствует, будет выброшено исключение. То есть по сути, если метод вызывается вне транзакции,
то будет выброшено исключение.

```java
@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.mandatoryTransactionMethod();
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.MANDATORY)
    public void mandatoryTransactionMethod() {
        // Логика, которая требует существования транзакции
    }
}
```

В этом примере `mandatoryTransactionMethod` в `AnotherService` требует существующей транзакции. Метод `performOperation` в
`ExampleService` создает эту транзакцию, поскольку у него установлен уровень распространения `REQUIRED`. Если метод
`mandatoryTransactionMethod` вызывается без существующей транзакции (например, из метода без аннотации `@Transactional`), будет
выброшено исключение.

В случае же вызова метода `mandatoryTransactionMethod` с существующей транзакцией, он будет выполняться в рамках этой транзакции.

# [**Назад**: *Уровни распространения*](../propagation.md)
