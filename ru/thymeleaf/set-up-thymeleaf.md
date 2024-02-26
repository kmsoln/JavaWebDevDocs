# Настройка Thymeleaf в проекте

Чтобы начать использовать библиотеку в вашем проекте, вам нужно добавить зависимость в файл `pom.xml` вашего проекта. Чтобы подключить Thymeleaf, добавьте следующую зависимость в раздел `dependencies` файла `pom.xml`:

```xml 

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
    <version>${springVersion}</version>
</dependency>

<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-spring6</artifactId>
    <version>${thymeleafVersion}</version>
</dependency>
```

Если вы используете Gradle Groovy, добавьте следующую строку в раздел `dependencies` файла `build.gradle`:

```groovy
dependencies {
    def thymeleafVersion = "3.1.2.RELEASE"
    def springVersion = '3.2.2'

    implementation "org.springframework.boot:spring-boot-starter-thymeleaf:$springVersion"
    implementation "org.thymeleaf:thymeleaf-spring6:$thymeleafVersion"
}
```

Можно заметить, что мы используем springVersion и thymeleafVersion. Вместо этих значений, необходимо подставить актуальные версии библиотек, которые вы используете в вашем проекте. Например, на данный момент, наиболее современная версия spring - 3.2.2. Следовательно, вместо springVersion нужно подставить 3.2.2. То же самое с Thymeleaf. Наиболее актуальная версия Thymeleaf - 3.1.2-RELEASE. Следовательно, вместо thymeleafVersion нужно подставить 3.1.2-RELEASE.

После добавления зависимости, Thymeleaf будет доступен в вашем проекте. Теперь вы можете использовать его для создания динамических веб-страниц.

Обратите внимание, что в groovy версии зависимостей мы используем $ для обращения к переменным, созданным ранее, в случае maven версии конструкция ${} написана только для того, чтобы выделить текст, который нужно заменить и синтаксического значения не имеет. 

# [**Следующий урок**: *Движок шаблонов*](template-engine.md)