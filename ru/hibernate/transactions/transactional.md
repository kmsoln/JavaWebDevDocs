# Создание транзакций в Hibernate

Для создания транзакций для последующего их запуска в Spring, используется аннотация `@Transactional`. Эта аннотация позволяет нам указать, что метод должен выполняться в рамках транзакции.

```java
@Transactional
public void transferMoney(Account from, Account to, BigDecimal amount) {
    // Проверяем баланс счета отправителя
    if (from.getBalance().compareTo(amount) < 0) {
        throw new NotEnoughMoneyException("Not enough money on account");
    }

    // Снимаем деньги со счета отправителя
    from.setBalance(from.getBalance().subtract(amount));
    accountRepository.save(from);

    // Зачисляем деньги на счет получателя
    to.setBalance(to.getBalance().add(amount));
    accountRepository.save(to);

    // Сохраняем запись о транзакции
    Transaction transaction = new Transaction(from, to, amount);
    transactionRepository.save(transaction);
}
```

В этом примере у нас есть метод `transferMoney`, который переводит деньги с одного счета на другой. Метод помечен аннотацией `@Transactional`, что означает, что он должен выполняться в рамках транзакции.

Если во время выполнения метода возникнет исключение, транзакция будет откатана, и все изменения, сделанные в рамках транзакции, будут отменены.

Таким образом, мы можем создавать транзакции в Hibernate при помощи аннотации `@Transactional`.

