# Ключевые слова именованных запросов

Мы уже выяснили что такое именованные запросы в названиях методов и как они работают. Теперь давайте поговорим о ключевых словах, которые можно использовать в именованных запросах.

- Distinct* - удаляет дубликаты из результата запроса (например `findDistinctByNameAndLastname(String name, String lastname)`). В SQL это будет `SELECT DISTINCT ...`
- And - соединяет условия запроса логическим "И" (например `findByNameAndLastname(String name, String lastname)`). В SQL это будет `SELECT name, lastname WHERE name = $name AND lastname = $lastname`
- Or - соединяет условия запроса логическим "ИЛИ" (например `findByNameOrLastname(String name, String lastname)`). В SQL это будет `SELECT name, lastname WHERE name = $name OR lastname = $lastname`
- Between - выбирает значения в диапазоне (например `findByAgeBetween(int min, int max)`). В SQL это будет `SELECT ... WHERE age BETWEEN $min AND $max`
- Is, Equals - выбирает значения равные указанному (например `findByAgeIs(int age)` или `findByAgeEquals(int age)`). В SQL это будет `SELECT ... WHERE age = $age`
- LessThan - выбирает значения меньше указанного (например `findByAgeLessThan(int age)`). В SQL это будет `SELECT ... WHERE age < $age`
- LessThanEqual - выбирает значения меньше или равные указанному (например `findByAgeLessThanEqual(int age)`). В SQL это будет `SELECT ... WHERE age <= $age`
- GreaterThan - выбирает значения больше указанного (например `findByAgeGreaterThan(int age)`). В SQL это будет `SELECT ... WHERE age > $age`
- GreaterThanEqual - выбирает значения больше или равные указанному (например `findByAgeGreaterThanEqual(int age)`). В SQL это будет `SELECT ... WHERE age >= $age`
- After - выбирает значения после указанной даты (например `findByStartDateAfter(Date date)`). В SQL это будет `SELECT ... WHERE start_date > $date`
- Before - выбирает значения до указанной даты (например `findByEndDateBefore(Date date)`). В SQL это будет `SELECT ... WHERE end_date < $date`
- Like - выбирает значения по шаблону (например `findByNameLike(String name)`). В SQL это будет `SELECT ... WHERE name LIKE %$name%`
- NotLike - выбирает значения не соответствующие шаблону (например `findByNameNotLike(String name)`). В SQL это будет `SELECT ... WHERE name NOT LIKE %$name%`
- StartingWith - выбирает значения начинающиеся с указанного (например `findByNameStartingWith(String name)`). В SQL это будет `SELECT ... WHERE name LIKE $name%`
- EndingWith - выбирает значения заканчивающиеся на указанное (например `findByNameEndingWith(String name)`). В SQL это будет `SELECT ... WHERE name LIKE %$name`
- Containing - выбирает значения содержащие указанное (например `findByNameContaining(String name)`). В SQL это будет `SELECT ... WHERE name LIKE %$name%`
- OrderBy - сортирует результат запроса по указанному полю (например `findByAgeOrderByLastnameDesc(int age)`). В SQL это будет `SELECT ... WHERE age = $age ORDER BY lastname DESC`
- Not - отрицает условие запроса (например `findByNameNot(String name)`). В SQL это будет `SELECT ... WHERE name <> $name`
- In - выбирает значения из списка (например `findByAgeIn(Collection<Integer> ages)`). В SQL это будет `SELECT ... WHERE age IN $ages`
- NotIn - выбирает значения не из списка (например `findByAgeNotIn(Collection<Integer> ages)`). В SQL это будет `SELECT ... WHERE age NOT IN $ages`
- True - выбирает значения равные `true` (например `findByActiveTrue()`). В SQL это будет `SELECT ... WHERE active = true`
- False - выбирает значения равные `false` (например `findByActiveFalse()`). В SQL это будет `SELECT ... WHERE active = false`
- IgnoreCase - игнорирует регистр (например `findByNameIgnoreCase(String name)`). В SQL это будет `SELECT ... WHERE UPPER(name) = UPPER($name)`
- IsNull, Null - выбирает значения равные `null` (например `findByAgeNull()`). В SQL это будет `SELECT ... WHERE age IS NULL`
- NotNull - выбирает значения не равные `null` (например `findByAgeNotNull()`). В SQL это будет `SELECT ... WHERE age IS NOT NULL`

* - Distinct может иногда давать неожиданные результаты. Например, `SELECT DISTINCT * FROM Users` и `SELECT second_name FROM Users`
может вернуть разные результаты, так как в первом случае дубликаты будут искаться по всем полям, а во втором - только по `second_name`
    (а так как фамилии имеют свойство быть одинаковыми чаще, чем все данные вместе, то результаты будут разные)
Также, например запрос `countDistinctByName`, подсчитает всех пользователей, так как Spring выведет запрос `SELECT COUNT(DISTINCT id) FROM Users WHERE name = $name`
и получается, что в таком запросе вообще нет смысла.

# [**Следующий урок (Аннотация именованных запросов)**](named-query-annotation.md)