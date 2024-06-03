# Создание транзакций

В Spring приложениях, транзакции обычно располагаются в классах сервисов. Для их обозначения используется аннотация
`@Transactional`. Эта аннотация позволяет указать, что метод должен быть выполнен в рамках транзакции.

Например, определим транзакцию в сервисе `MoneyTransferService`, которая будет выполнять перевод денег с одного счета
на другой и в случае ошибки откатывать все изменения. Достигается это обычно с использованием конструкций обработки
исключений `try-catch` и вызова метода `rollback` у объекта `Transaction`.

```java
@Service
public class MoneyTransferService {

    @Autowired
    private AccountRepository accountRepository;

    @Transactional
    public void transferMoney(Long fromAccountId, Long toAccountId, BigDecimal amount) {
        Account fromAccount = accountRepository.findById(fromAccountId).orElseThrow();
        Account toAccount = accountRepository.findById(toAccountId).orElseThrow();

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
в рамках одной транзакции. Если хотя бы одна операция завершится неудачно (если будет выброшено исключение), то Spring
автоматически откатит все изменения и транзакция не будет сохранена в базе данных. 

Если все операции внутри метода `transferMoney` завершатся успешно, то изменения будут сохранены в базе данных методом 
`save` репозитория `accountRepository`.

Обратите внимание, что все используемые в этом коде методы типа `findById`, `setBalance` и `save` - это методы 
репозитория `AccountRepository` и сущности `Account`. Все они должны быть определены в соответствующих классах.

# [**Следующий урок**: *Проблемы транзакций*](transaction-control.md)

