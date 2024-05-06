# Использование транзакций

После того как мы создали транзакцию внутри сервиса, мы можем использовать ее в нашем приложении. Для этого нам нужно
обратиться к методу транзакции сервиса в котором мы создали транзакцию. Например, если мы создали транзакцию в сервисе
`MoneyTransferService`, то мы можем использовать ее в контроллере следующим образом:

```java
@RestController
public class HomeController {

    @Autowired
    private MoneyTransferService moneyTransferService;

    @PostMapping("/transfer")
    public void transferMoney(@RequestParam Long fromAccountId, @RequestParam Long toAccountId, @RequestParam BigDecimal amount) {
        moneyTransferService.transferMoney(fromAccountId, toAccountId, amount);
    }
}
```

В этом примере мы создаем контроллер `HomeController`, который обрабатывает POST запрос на `/transfer`. В методе
`transferMoney` контроллера мы обращаемся к методу `transferMoney` сервиса `MoneyTransferService`, который выполняет
перевод денег с одного счета на другой в рамках транзакции.

Таким образом, все операции внутри метода `transferMoney` контроллера будут выполнены в рамках одной транзакции, созданной
в сервисе `MoneyTransferService`.