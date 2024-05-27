# Transactional Propagation - NEVER в Java

## Введение

В этой методической инструкции мы рассмотрим одно из видов propagation — NEVER.

## Что такое Propagation.NEVER?

`Propagation.NEVER` означает, что метод не будет выполняться в рамках существующей транзакции. Если текущая транзакция существует, будет выброшено исключение `IllegalTransactionStateException`.

### Пример:

```java
@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.neverTransactionMethod(); // Это вызовет IllegalTransactionStateException
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.NEVER)
    public void neverTransactionMethod() {
        // Логика, которая не должна выполняться в рамках транзакции
    }
}
```

## Объяснение поведения
### Вызов с существующей транзакцией
Когда метод performOperation вызывается, создается новая транзакция, так как установлен Propagation.REQUIRED. Затем вызывается метод neverTransactionMethod, который аннотирован как Propagation.NEVER. Поскольку этот метод не должен выполняться в рамках существующей транзакции, выбрасывается исключение IllegalTransactionStateException.

### Вызов без существующей транзакции
Если метод neverTransactionMethod вызывается без существующей транзакции (например, из метода без аннотации @Transactional), то он выполняется нормально, не в рамках транзакции.