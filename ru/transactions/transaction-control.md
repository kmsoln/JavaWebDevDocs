# Контроль транзакций

Контроль транзакций в JPA может осуществляться автоматически, как в примере ниже:

```java
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
```

В этом примере Spring сам откатит изменения, если хотя бы одна операция завершится неудачно (если будет выброшено
исключение). Таким образом, все операции внутри метода `transferMoney` будут выполнены в рамках одной транзакции.

Но также, мы можем управлять транзакциями вручную, используя объект `Transaction`. Перепишем метод `transferMoney` так,
чтобы он использовал объект `Transaction`:

```java
public void transferMoney(Long fromAccountId, Long toAccountId, BigDecimal amount) {
    Account fromAccount = accountRepository.findById(fromAccountId).orElseThrow();
    Account toAccount = accountRepository.findById(toAccountId).orElseThrow();

    if (fromAccount.getBalance().compareTo(amount) < 0) {
        throw new IllegalArgumentException("Not enough money on account");
    }

    Transaction transaction = entityManager.getTransaction();
    try {
        transaction.begin();

        fromAccount.setBalance(fromAccount.getBalance().subtract(amount));
        toAccount.setBalance(toAccount.getBalance().add(amount));

        accountRepository.save(fromAccount);
        accountRepository.save(toAccount);

        transaction.commit();
    } catch (Exception e) {
        transaction.rollback();
        throw e;
    }
}
```

В этом примере мы создаем объект `Transaction` и вызываем метод `begin`, чтобы начать транзакцию. Если все операции
внутри блока `try` завершатся успешно, то вызываем метод `commit`, чтобы сохранить изменения в базе данных. Если хотя бы
одна операция завершится неудачно, то мы попадаем в блок `catch`, где вызываем метод `rollback`, чтобы откатить все
изменения.

Помимо метода `begin`, `commit` и `rollback`, объект `Transaction` также следует упомянуть метод `savepoint`, который
позволяет создавать точки сохранения внутри транзакции. Это может быть полезно, если мы хотим откатить только часть
изменений, а не всю транзакцию.

Например, мы хотим реализовать транзакцию, которая переводит деньги с одного счета на другой и после этого обновляет 
баланс счетов, участвующих в транзакции. Если обновление баланса счета получателя завершится неудачно, то мы не хотим
откатывать транзакцию полностью, а только откатить обновление. Для этого мы можем использовать метод `savepoint`:

```java
public void transferMoney(Long fromAccountId, Long toAccountId, BigDecimal amount) {
    Account fromAccount = accountRepository.findById(fromAccountId).orElseThrow();
    Account toAccount = accountRepository.findById(toAccountId).orElseThrow();

    if (fromAccount.getBalance().compareTo(amount) < 0) {
        throw new IllegalArgumentException("Not enough money on account");
    }

    Transaction transaction = entityManager.getTransaction();
    try {
        transaction.begin();

        fromAccount.setBalance(fromAccount.getBalance().subtract(amount));
        toAccount.setBalance(toAccount.getBalance().add(amount));

        accountRepository.save(fromAccount);
        accountRepository.save(toAccount);

        Savepoint savepoint = transaction.setSavepoint();

        if (toAccount.getBalance().compareTo(BigDecimal.ZERO) < 0) {
            transaction.rollback(savepoint);
        }

        transaction.commit();
    } catch (Exception e) {
        transaction.rollback();
        throw e;
    }
}
```

В этом примере мы создаем точку сохранения `savepoint` после обновления баланса счета получателя. Если баланс счета
получателя станет отрицательным, то мы вызываем метод `rollback` с параметром `savepoint`, чтобы откатить только
обновление баланса счета получателя. Если все операции внутри блока `try` завершатся успешно, то вызываем метод `commit`.

Таким образом, управление транзакциями вручную позволяет нам более гибко управлять изменениями в базе данных и откатывать
только часть изменений, если это необходимо.

# [**Следующий урок**: *Блокирование базы данных транзакцией*](database-lock.md)
