# Создание контролируемых транзакций

Если в каких-то ситуациях вам нужно создать транзакцию и контролировать ее вручную в SpringBoot, для этого
предусмотрены специальные методы контролирования транзакций.

```java
import org.springframework.transaction.PlatformTransactionManager;
import org.springframework.transaction.TransactionDefinition;
import org.springframework.transaction.TransactionStatus;
import org.springframework.transaction.support.DefaultTransactionDefinition;

import javax.sql.DataSource;

public class TransactionExample {

    private final PlatformTransactionManager transactionManager;
    private final DataSource dataSource;

    public TransactionExample(PlatformTransactionManager transactionManager, DataSource dataSource) {
        this.transactionManager = transactionManager;
        this.dataSource = dataSource;
    }

    public void transferMoney(Long fromAccountId, Long toAccountId, BigDecimal amount) {
        TransactionDefinition def = new DefaultTransactionDefinition();
        TransactionStatus status = transactionManager.getTransaction(def);
        try {
            // your business logic here
            transactionManager.commit(status);
        } catch (Exception e) {
            transactionManager.rollback(status);
            throw e;
        }
    }
}
```

В случае, если внутри транзакции, возникает необходимость откатить все изменения, то можно вызвать метод `rollback` у
объекта `TransactionStatus`, для сохранения изменений в базе данных используйте метод `commit`.

Также у класса `PlatformTransactionManager` есть еще несколько методов, которые могут быть полезны вам. Например:
- `suspend(TransactionStatus status)` - приостанавливает транзакцию.
- `resume(TransactionStatus status)` - возобновляет транзакцию.

# [**Следующий урок**: *Использование уровней изоляции*](isolation-usage.md)