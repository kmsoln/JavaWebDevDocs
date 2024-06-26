# Проблемы транзакций

Как вы уже поняли - транзакции - это мощный инструмент, который позволяет обеспечить целостность данных в базе. Однако,
транзакции могут привести к некоторым проблемам, которые вам нужно уметь решать. Как вы скорее всего уже поняли, в
большинстве приложений использование транзакций не ограничивается одной атомарной операцией, в большинстве случаев
транзакций бывает много и все они выполняются одновременно. И так часто случается, что разные транзакции могут работать 
с одними и теми же данными. Вот именно в этом случае могут возникнуть проблемы.

Рассматривая все эти проблемы транзакций, важно понимать что сами по себе транзакции не являются источником проблем. 
Проблемы начинаются, когда несколько независимых транзакций одновременно работают с одними и теми же данными. Такие транзакции называются
**конфликтующими** (concurrent transactions).

Зачастую, невозможно предугадать в какой момент времени запустится та или иная транзакция, какая из них запустится или
завершится первой, поэтому важно уметь предусматривать такие ситуации, потому что они могут привести к непредсказуемым
результатам, отладить причину которых очень сложно.

Существует несколько видов проблем в таких случаях:
- [**Dirty reads**](problems/dirty-reads.md)
- [**Non-repeatable reads**](problems/non-repeatable-reads.md)
- [**Phantom reads**](problems/phantom-reads.md)
- [**Lost updates**](problems/lost-updates.md)

Для недопущения этих проблем, разработчики придумали принципы, использование которых гарантирует корректное выполнение
транзакций. О них мы поговорим дальше.

# [**Следующий урок**: *Принципы работы транзакций*](principles.md)