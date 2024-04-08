# Отношение многие ко многим

## Описание

Отношение многие ко многим (Many-to-Many) - это отношение, при котором одна сущность может быть связана с несколькими другими сущностями, и наоборот, каждая из этих сущностей может быть связана с несколькими сущностями первой.

Давайте рассмотрим пример отношения многие-ко-многим между сущностями `Student` и `Course`. Один студент может посещать несколько курсов, и каждый курс может посещать несколько студентов.

## Описание сущностей

Давайте создадим две сущности `Student` и `Course`. Сущности `Student` и `Course` будут иметь отношение многие-ко-многим друг с другом.

### Сущность Student

```java
@Entity
@Table(name = "students")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToMany
    @JoinTable(
        name = "students_courses",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private List<Course> courses;

    // геттеры и сеттеры
}
```

### Сущность Course

```java
@Entity
@Table(name = "courses")
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    @ManyToMany(mappedBy = "courses")
    private List<Student> students;

    // геттеры и сеттеры
}
```

В этом примере у нас есть две сущности: `Student` и `Course`. У сущности `Student` есть поле `courses`, которое связано с сущностью `Course` при помощи аннотации `@ManyToMany`. У сущности `Course` есть поле `students`, которое также связано с сущностью `Student` при помощи аннотации `@ManyToMany`.

В аннотации `@ManyToMany` есть параметр `@JoinTable`, который указывает на таблицу, которая связывает две сущности. В данном случае, это таблица `students_courses`. В аннотации `@JoinTable` есть параметры `joinColumns` и `inverseJoinColumns`, которые указывают на столбцы в таблице `students_courses`, которые связаны с таблицами `students` и `courses`.

Теперь у нас есть две таблицы: `students` и `courses`, которые связаны отношением многие-ко-многим. В таблице `students_courses` есть столбцы `student_id` и `course_id`, которые связаны с таблицами `students` и `courses` по столбцам `id`.

Таким образом, мы описали отношение многие-ко-многим между сущностями при помощи JPA.

# [**Назад**: *Отношения между таблицами*](what-is-relations.md)