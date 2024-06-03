# Propagation level - NEVER

Уровень распространения `NEVER` означает, что текущий метод должен выполняться без транзакции. Если текущая транзакция
существует, будет выброшено исключение. Этот уровень распространения обеспечивает выполнение метода без транзакции, даже если
он вызывается из метода существующей транзакции. Если метод вызывается из метода с транзакцией, будет выброшено исключение.

Например, у нас есть два сервиса: `ExampleService` и `AnotherService`. Метод `performOperation` в `ExampleService` вызывает
метод `neverTransactionMethod` в `AnotherService`, который аннотирован уровнем распространения `NEVER`.

```java
@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.neverTransactionMethod();
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.NEVER)
    public void neverTransactionMethod() {
        // Логика, которая не требует транзакции
    }
}
```

В этом примере `neverTransactionMethod` в `AnotherService` требует отсутствия транзакции. Метод `performOperation` в
`ExampleService` создает транзакцию, поскольку у него установлен уровень распространения `REQUIRED`. Если метод
`neverTransactionMethod` вызывается из метода с транзакцией, будет выброшено исключение.

Если же метод `neverTransactionMethod` вызывается из метода без транзакции, он будет выполнен без транзакции.

# [**Назад**: *Уровни распространения*](../propagation.md)

