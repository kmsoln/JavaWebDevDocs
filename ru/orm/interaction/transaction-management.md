# Управление транзакциями в ORM
Управление транзакциями в ORM играет ключевую роль в обеспечении целостности данных и консистентности операций с базой данных.

## Что такое транзакция?

Транзакция представляет собой логическую операцию, которая состоит из одного или нескольких SQL запросов, образующих единое целое. Транзакции обеспечивают атомарность, согласованность, изолированность и устойчивость (ACID) операций с базой данных.

## Реализация управления транзакциями в ORM:

1. **Поддержка атомарных транзакций:**
    - ORM предоставляет механизмы для группировки нескольких операций с базой данных в одну транзакцию.
    - Это обеспечивает выполнение всех операций либо полностью, либо откатывание всех операций в случае возникновения ошибки.

2. **Методы коммита и отката транзакций:**
    - ORM предоставляет методы для явного подтверждения (commit) или отмены (rollback) транзакции.
    - При успешном выполнении всех операций транзакция коммитится, что приводит к сохранению изменений в базе данных. В случае ошибки или отката транзакция отменяется, и все изменения откатываются.

3. **Обработка исключений:**
    - ORM обрабатывает исключения, возникающие во время выполнения транзакций.
    - При возникновении ошибки ORM автоматически откатывает транзакцию, чтобы избежать нарушения целостности данных.

## Примеры использования в Java:

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityTransaction;
import javax.persistence.Persistence;

public class TransactionExample {

    public static void main(String[] args) {
        EntityManager entityManager = Persistence.createEntityManagerFactory("persistence_unit_name").createEntityManager();
        EntityTransaction transaction = entityManager.getTransaction();

        try {
            transaction.begin();

            // Выполнение операций с базой данных

            transaction.commit();
        } catch (Exception e) {
            if (transaction != null && transaction.isActive()) {
                transaction.rollback();
            }
            e.printStackTrace();
        } finally {
            if (entityManager != null) {
                entityManager.close();
            }
        }
    }
}
```

В данном примере:

- `EntityManager` представляет собой интерфейс для работы с сущностями в контексте персистентности.
- `EntityTransaction` используется для управления транзакциями.
- `transaction.begin()` запускает новую транзакцию.
- `transaction.commit()` фиксирует транзакцию (если все операции выполнены успешно).
- `transaction.rollback()` отменяет транзакцию в случае ошибки.

## [К оглавлению](../references.md)