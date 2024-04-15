# Отношение один-к-одному

Одно из наиболее распространенных отношений в базах данных - отношение один-к-одному. В этом случае одна запись в таблице связана с одной записью в другой таблице. Например, у нас есть таблица `Person` и таблица `Passport`. У каждого человека может быть только один паспорт, а у каждого паспорта только один человек.

Для описания таких отношений в JPA используется аннотация `@OneToOne`. Давайте посмотрим на пример:

```java
@Entity
@Table(name = "persons")
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToOne(mappedBy = "person")
    private Passport passport;

    // геттеры и сеттеры
}
```

```java
@Entity
@Table(name = "passports")
public class Passport {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String number;

    @OneToOne
    @JoinColumn(name = "person_id")
    private Person person;

    // геттеры и сеттеры
}
```

В этом примере у нас есть два Entity класса: `Person` и `Passport`. У класса `Person` есть поле `passport`, которое связано с классом `Passport` при помощи аннотации `@OneToOne`. У класса `Passport` есть поле `person`, которое также связано с классом `Person` при помощи аннотации `@OneToOne`.

В аннотации `@OneToOne` есть параметр `mappedBy`, который указывает на поле в классе `Passport`, которое связано с классом `Person`. Таким образом, мы указываем, что связь один-к-одному устанавливается через поле `passport` в классе `Person`.

В аннотации `@OneToOne` также есть параметр `@JoinColumn`, который указывает на столбец в таблице `passports`, который связан с таблицей `persons`. В данном случае, это столбец `person_id`.

Теперь у нас есть две таблицы: `persons` и `passports`, которые связаны отношением один-к-одному. В таблице `persons` есть столбец `passport_id`, который связан с таблицей `passports` по столбцу `id`.

Таким образом, мы описали отношение один-к-одному между таблицами при помощи JPA.

# [**Назад**: *Отношения между таблицами*](what-is-relations.md)