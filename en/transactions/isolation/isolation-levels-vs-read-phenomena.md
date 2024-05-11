# **Isolation Levels vs read phenomena**
Isolation levels vs read phenomena

| [Isolation level](isolation.md)         | [Dirty reads](dirty-reads.md)                | [Lost updates](lost-updates.md)              | [Non-repeatable reads](non-repeatable-read.md) | [Phantoms](phantom-reads.md)                 |
|-----------------------------------------|----------------------------------------------|----------------------------------------------|------------------------------------------------|----------------------------------------------|
| [Read Uncommitted](read-uncommitted.md) | <span style="color:red">may occur</span>     | <span style="color:red">may occur</span>     | <span style="color:red">may occur</span>       | <span style="color:red">may occur</span>     |
| [Read Committed](read-committed.md)     | <span style="color:green">don't occur</span> | <span style="color:red">may occur</span>     | <span style="color:red">may occur</span>       | <span style="color:red">may occur</span>     |
| [Repeatable Read](repeatable-read.md)   | <span style="color:green">don't occur</span> | <span style="color:green">don't occur</span> | <span style="color:green">don't occur</span>   | <span style="color:red">may occur</span>     |
| [Serializable](serializable.md)         | <span style="color:green">don't occur</span> | <span style="color:green">don't occur</span> | <span style="color:green">don't occur</span>   | <span style="color:green">don't occur</span> |
