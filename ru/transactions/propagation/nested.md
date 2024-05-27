# Transactional Propagation - NESTED в Java

## Введение

В этой методической инструкции мы рассмотрим одно из видов propagation — NESTED.

## Что такое Propagation.NESTED?

**`Propagation.NESTED`** означает, что метод будет выполняться в рамках вложенной транзакции, если существует активная транзакция. Если нет активной транзакции, то поведение будет таким же, как у **`Propagation.REQUIRED`**.

### Пример:

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
        // Логика, выполняющаяся в рамках вложенной транзакции
    }
}
```
В данном примере nestedTransactionMethod в AnotherService выполняется в рамках вложенной транзакции, если существует активная транзакция. Метод performOperation в ExampleService создает эту транзакцию, поскольку у него установлен Propagation.REQUIRED.

## Объяснение поведения
Вызов с существующей транзакцией
Когда performOperation вызывается, создается новая транзакция, так как Propagation.REQUIRED создает новую транзакцию, если её нет. Затем вызывается nestedTransactionMethod, который выполняется в рамках вложенной транзакции.

## Вызов без существующей транзакции
Если метод nestedTransactionMethod вызывается без существующей транзакции (например, из метода без аннотации @Transactional или с другой propagation), поведение будет таким же, как у Propagation.REQUIRED, и создастся новая транзакция.