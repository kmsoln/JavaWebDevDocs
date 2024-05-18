# Принципы работы транзакций

В основе транзакций лежит принцип, который называется ACID. Это аббревиатура, которая расшифровывается как atomicity,
consistency, isolation, durability или атомарность, согласованность, изолированность, долговечность.

- **Атомарность** означает, что транзакция либо выполняется полностью, либо не выполняется
  вовсе. ([подробнее](principles/atomicity.md))
- **Согласованность** означает, что транзакция должна переводить базу данных из одного согласованного состояния в другое
  согласованное состояние. ([подробнее](principles/consistency.md))
- **Изолированность** означает, что транзакция должна быть изолирована от других
  транзакций. ([подробнее](principles/isolation.md))
- **Долговечность** означает, что изменения, внесенные транзакцией, должны быть долговечны и не должны быть отменены
  после успешного завершения транзакции. ([подробнее](principles/durability.md))

Эти принципы обеспечивают целостность данных в базе и гарантируют, что транзакции выполняются корректно и безопасно.
Далее мы рассмотрим к чему приводит нарушение некоторых из них.

# [**Следующий урок**: *Транзакции в JPA*](transactions-jpa)