# Propagation level - SUPPORTS

Уровень распространения `SUPPORTS` означает, что текущий метод должен выполняться в рамках существующей транзакции. Если
текущая транзакция отсутствует, метод будет выполнен без транзакции. Это означает, что метод будет выполняться в рамках
транзакции, если она существует, и без транзакции, если нет. Если метод вызывается из метода без транзакции, он будет
выполнен без транзакции.

Например, у нас есть два сервиса: `ExampleService` и `AnotherService`. Метод `performOperation` в `ExampleService` вызывает
метод `supportsTransactionMethod` в `AnotherService`, который аннотирован уровнем распространения `SUPPORTS`.

```java 

@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.supportsTransactionMethod();
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.SUPPORTS)
    public void supportsTransactionMethod() {
        // Логика, которая может выполняться в рамках транзакции
    }
}
```

В этом примере `supportsTransactionMethod` в `AnotherService` требует существующей транзакции. Метод `performOperation` в
`ExampleService` создает эту транзакцию, поскольку у него установлен уровень распространения `REQUIRED`. Если метод
`supportsTransactionMethod` вызывается без существующей транзакции (например, из метода без аннотации `@Transactional`), он
будет выполнен без транзакции. Если метод вызывается с существующей транзакцией, он будет выполняться в рамках этой транзакции.

# [**Назад**: *Уровни распространения*](../propagation.md)
