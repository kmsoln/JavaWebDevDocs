# Propagation level - NOT_SUPPORTED

Уровень распространения `NOT_SUPPORTED` означает, что текущий метод должен выполняться без транзакции. Если текущая транзакция существует, она будет
приостановлена и возобновлена после выполнения метода. Этот уровень распространения полезен, когда методу не требуется участие в транзакции,
например, при выполнении операций только для чтения. 

Например, у нас есть два сервиса: `ExampleService` и `AnotherService`. Метод `performOperation` в `ExampleService` вызывает
метод `notSupportedTransactionMethod` в `AnotherService`, который аннотирован уровнем распространения `NOT_SUPPORTED`.

```java

@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.notSupportedTransactionMethod();
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.NOT_SUPPORTED)
    public void notSupportedTransactionMethod() {
        // Логика, которая не требует транзакции
    }
}
```

В этом примере `notSupportedTransactionMethod` в `AnotherService` не требует участия в транзакции. Метод `performOperation` в
`ExampleService` создает транзакцию, поскольку у него установлен уровень распространения `REQUIRED`. Если метод
`notSupportedTransactionMethod` вызывается из метода с транзакцией, текущая транзакция будет приостановлена и возобновлена после выполнения метода.

Если же метод `notSupportedTransactionMethod` вызывается из метода без транзакции, он будет выполнен без транзакции.

# [**Назад**: *Уровни распространения*](../propagation.md)

