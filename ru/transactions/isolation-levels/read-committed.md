# Уровень изоляции транзакций READ COMMITTED

Транзакции видят только те изменения, которые были зафиксированы другими транзакциями. Этот уровень гарантирует 
исполнение принципа `согласованности` и является наиболее распространенным уровнем изоляции из-за
хорошего баланса между производительностью и надежностью. Суть его заключается в том, что транзакции видят только
те изменения, которые были зафиксированы другими транзакциями, но не видят изменения, которые еще не были зафиксированы.

Представим, что у нас есть база данных товаров магазина. Среди других, в ней есть таблица `products`, которая содержит
информацию о товарах. Предположим, что у нас есть две транзакции. Одна из них начинается и изменяет цену товара,
в любой момент ее исполнения начинается транзакция, которая читает это значение. При использовании уровня изоляции 
READ COMMITTED, транзакция, которая считывает значение цены товара, получит старое значение, так как изменения еще не
были зафиксированы. Но если вторая транзакция завершится успешно, то первая транзакция сможет прочитать уже измененное
значение.

![read committed](../../../src/transactions/read-committed.png)

Как видим в примере, первая транзакция читает значение, вместе с ней вторая транзакция читает это значение и получает
старое. Но если эта транзакция запускается после полного успешного завершения транзакции, которая изменила значение,
то она получит уже измененное значение.

Таким образом, уровень изоляции READ COMMITTED гарантирует исполнение принципа `согласованности` и является наиболее
распространенным уровнем изоляции.

Однако, ошибки вроде
[неповторяемого чтения](../problems/non-repeatable-reads.md)
или [фантомного чтения](../problems/phantom-reads.md)
все еще могут возникнуть, так данные с которыми работает транзакция открыты для изменений другими транзакциями.

# [**Назад**: *Уровни изоляции транзакций*](../principles/isolation.md)