# Transactional Propagation - REQUIRES_NEW в Java

Уровень распространения `REQUIRES_NEW` означает, что текущий метод должен выполняться в новой транзакции. Если текущая транзакция существует, она будет
приостановлена и возобновлена после выполнения метода. Если текущая транзакция отсутствует, будет создана новая транзакция. Этот уровень распространения
полезен, когда методу требуется выполниться в новой транзакции, независимо от того, существует ли уже транзакция или нет. Если метод вызывается из
метода с существующей транзакцией, текущая транзакция будет приостановлена, а метод будет выполнен в новой транзакции. Если метод вызывается из метода
без транзакции, будет создана новая транзакция. Если метод вызывается из метода с уровнем распространения `REQUIRES_NEW`, будет создана новая транзакция.

Например, у нас есть два сервиса: `ExampleService` и `AnotherService`. Метод `performOperation` в `ExampleService` вызывает метод `requiresNewTransactionMethod`
в `Another Service`, который аннотирован уровнем распространения `REQUIRES_NEW`.

```java
@Service
public class ExampleService {

    @Autowired
    private AnotherService anotherService;

    @Transactional(propagation = Propagation.REQUIRED)
    public void performOperation() {
        anotherService.requiresNewTransactionMethod();
        // Другие операции
    }
}

@Service
public class AnotherService {

    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void requiresNewTransactionMethod() {
        // Логика, которая требует новой транзакции
    }
}
```

В этом примере `requiresNewTransactionMethod` в `AnotherService` требует новой транзакции. Метод `performOperation` в `ExampleService` создает эту транзакцию,
поскольку у него установлен уровень распространения `REQUIRED`. Если метод `requiresNewTransactionMethod` вызывается без существующей транзакции (например,
из метода без аннотации `@Transactional`), будет создана новая транзакция. Если метод вызывается с существующей транзакцией, текущая транзакция будет
приостановлена, а метод будет выполнен в новой транзакции. Если новая транзакция завершается успешно, изменения будут сохранены в базе данных. Если же новая
транзакция завершается с ошибкой, она будет откатана, но родительская транзакция останется активной. 

# [**Назад**: *Уровни распространения*](../propagation.md)

