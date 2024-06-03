# RollbackOnly в Spring транзакциях

RollbackOnly это параметр декоратора `@Transactional`, который указывает на то должна ли транзакция быть откатана. Если
транзакция помечена как `RollbackOnly`, она будет откатана, даже если она завершается успешно. Это позволяет откатить
транзакцию в случае возникновения ошибки, несмотря на то, что она завершилась успешно.

Звучит немного запутанно, давайте разберемся. При начале работы транзакции при неявном указании `RollbackOnly`, стандартное
значение этой переменной равно `false`, в большинстве случаев программист не будет указывать значение `RollbackOnly` явно,
потому что если в процессе выполнения метода произойдет ошибка, Spring сам поменяет значение `RollbackOnly` на `true` и
таким образом в любой момент выполнения транзакции можно будет понять были ли ошибки в процессе выполнения метода.

Например:

```java
@Service
public class ExampleService {

    @Autowired
    private ExampleRepository exampleRepository;

    @Transactional
    public void performOperation() {
        exampleRepository.save(new Example("Example")); // (1)
        
        // (2)
        
        if (isRollbackOnly())
            System.out.println("Rollback is true");
        else 
            System.out.println("Rollback is false");
    }
}
```

В примере выше в точке (1) происходит сохранение объекта `Example` в базу данных. Предположим, что при выполнении
этой операции произошла ошибка и транзакция должна быть откатана. Spring поменяет значение `RollbackOnly` на `true` и
в точке (2) значение `RollbackOnly` будет равно `true`. Это будет означать, что транзакция будет откатана независимо от
того, что случится дальше.

Таким образом в примере будет выведено сообщение `Rollback is true`.