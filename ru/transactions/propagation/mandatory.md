# Transactional Propagation - MANDATORY в Java

## Введение

Один из аспектов управления транзакциями — это propagation, то есть поведение транзакции, когда метод с аннотацией `@Transactional` вызывает другой метод, также аннотированный `@Transactional`. В этой методической инструкции мы рассмотрим одно из видов propagation — MANDATORY.

## Что такое Propagation.MANDATORY?

**`Propagation.MANDATORY`** означает, что метод должен выполняться в рамках существующей транзакции. Если текущая транзакция отсутствует, будет выброшено исключение **`IllegalTransactionStateException`**.

### Пример:

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
В данном примере mandatoryTransactionMethod в AnotherService требует, чтобы была существующая транзакция. Метод performOperation в ExampleService создает эту транзакцию, поскольку у него установлен Propagation.REQUIRED.

## Объяснение поведения
Вызов с существующей транзакцией
Когда performOperation вызывается, создается новая транзакция, так как Propagation.REQUIRED создает новую транзакцию, если её нет. Затем вызывается mandatoryTransactionMethod, который требует существующей транзакции. Поскольку транзакция уже существует, метод выполняется успешно в рамках этой транзакции.

Вызов без существующей транзакции
Если метод mandatoryTransactionMethod вызывается без существующей транзакции (например, из метода без аннотации @Transactional или с другой propagation), будет выброшено исключение:

```java
public void someOtherMethod() {
anotherService.mandatoryTransactionMethod(); // Это вызовет IllegalTransactionStateException
}
```
Важность использования Propagation.MANDATORY
Использование Propagation.MANDATORY полезно, когда определенные методы должны всегда выполняться в рамках транзакции, обеспечивая целостность данных и согласованность операций. Например, если метод выполняет несколько операций, которые должны быть атомарными (либо все успешны, либо ни одна не успешна), его выполнение вне транзакции может привести к