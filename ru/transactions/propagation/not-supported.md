# Transactional Propagation - NOT_SUPPORTED в Java

## Введение

В этой методической инструкции мы рассмотрим одно из видов propagation — NOT_SUPPORTED.

## Что такое Propagation.NOT_SUPPORTED?

`Propagation.NOT_SUPPORTED` означает, что метод не будет выполняться в рамках существующей транзакции. Если текущая транзакция существует, она будет приостановлена до завершения выполнения метода.

### Пример:

```java
@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.notSupportedTransactionMethod(); // Текущая транзакция будет приостановлена
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.NOT_SUPPORTED)
    public void notSupportedTransactionMethod() {
        // Логика, которая не должна выполняться в рамках транзакции
    }
}
```
## Объяснение поведения
### Вызов с существующей транзакцией
Когда метод performOperation вызывается, создается новая транзакция, так как установлен Propagation.REQUIRED. Затем вызывается метод notSupportedTransactionMethod, который аннотирован как Propagation.NOT_SUPPORTED. Текущая транзакция приостанавливается до завершения выполнения метода.

### Вызов без существующей транзакции
Если метод notSupportedTransactionMethod вызывается без существующей транзакции (например, из метода без аннотации @Transactional), то он выполняется нормально, не в рамках транзакции.