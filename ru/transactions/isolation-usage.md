# Использование изоляции транзакций в Spring

Для использования [уровней изоляции](principles/isolation.md) в транзакциях Spring, можно использовать параметры
декоратора `@Transactional`, а конкретно параметр `isolation`. Например, создадим транзакцию с уровнем изоляции
[READ_COMMITTED](isolation-levels/read-committed.md):

```java
@Service
public class MoneyTransferService {

    @Autowired
    private AccountRepository accountRepository;

    @Transactional(isolation = Isolation.READ_COMMITTED)
    public void transferMoney(Long fromAccountId, Long toAccountId, BigDecimal amount) {
        Account fromAccount = accountRepository.findById(fromAccountId).orElseThrow();
        Account toAccount = accountRepository.findById(toAccountId
        ).orElseThrow();

        if (fromAccount.getBalance().compareTo(amount) < 0) {
            throw new IllegalArgumentException("Not enough money on account");
        }

        fromAccount.setBalance(fromAccount.getBalance().subtract(amount));
        toAccount.setBalance(toAccount.getBalance().add(amount));

        accountRepository.save(fromAccount);
        accountRepository.save(toAccount);
    }
}
```

В этом примере мы создаем сервис `MoneyTransferService`, который выполняет перевод денег с одного счета на другой.
Метод `transferMoney` помечен аннотацией `@Transactional`, что означает, что все операции внутри метода будут выполнены
в рамках одной транзакции с уровнем изоляции [READ_COMMITTED](isolation-levels/read-committed.md).

Таким же образом можно использовать и другие уровни изоляции:
- [READ_UNCOMMITTED](isolation-levels/read-uncommitted.md)
- [REPEATABLE_READ](isolation-levels/repeatable-read.md)
- [SERIALIZABLE](isolation-levels/serializable.md)

Если не указывать уровень изоляции явно, то будет использован уровень по умолчанию, который зависит от используемой базы
данных. Например, в MySQL по умолчанию используется уровень изоляции [REPEATABLE_READ](isolation-levels/repeatable-read.md).

# [**Следующий урок**: *Propagation*](propagation.md)