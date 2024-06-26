# Логические контроллеры (Logic Controllers)

Логические контроллеры (Logic controllers) служат для управления ходом выполнения сценария, и представляют собой аналоги
управляющих конструкций в обычных языках программирования. Для организации выполняемых шагов сценария в виде иерархии
`набор тестов->тест->шаг` используется простой контроллер (Simple Controller), который группирует запросы и другие
логические контроллеры. Контроллер If Controller позволяет проверить некоторое условие и выполнить
вложенные действия, только если условие выполняется. If Controller не содержит ветви else. Множественный выбор
реализуется контроллером Switch Controller. Для организации цикла служит контроллер Loop Controller. В качестве
единственной опции настроек Loop Controller выступает число повторений цикла. Предположим, что мы создали цикл на три
повторения, внутри которого разместили три действия (обозначим их как A, B, C). В этом случае действия будут выполняться
следующим образом: ABC, ABC, ABC.

Альтернативный способ организации цикла предоставляет контроллер ForEach Controller. Его особенность в том, что цикл
выполняется не фиксированное количество раз, а динамически, на основании списка переменных, имена которых строятся по
правилу “базовое имя_номер” (например, var_1, var_2, …). Многие элементы JMeter формируют результаты именно в виде
подобных переменных. Если необходимо, чтобы внутри цикла выполнялся только один из трех возможных шагов (т.е.
выполняемые действия чередовались: A, B, C), то следует использовать чередующий контроллер (Interleave Controller). Для
имитации случайного поведения пользователя, выбирающего на каждой итерации теста одно из возможных действий,
используется контроллер Random Controller. На каждой из итераций цикла он выбирает одно из вложенных действий не
последовательно, а случайно (в нашем примере это будет что-то вроде: A, B, A, C, A). Контроллер Throughput Controller
позволяет выполнять действия, помещенные внутрь контроллера, с некоторой долей вероятности (например, в 30% случаев).
Для тестирования кода, который может приводить к таймауту загрузки страницы, используется Runtime Controller. Его
единственный параметр – предельное время выполнения вложенных в этот контроллер действий. Также совместно с циклами
используется контроллер Once Only Controller. Его назначение – выполнить вложенные действия только один раз независимо
от того, сколько действий диктуется родительским контроллером. Например, если поместить Once Only Controller внутрь Loop
Controller, то действия внутри Once Only будут выполнены всего один раз

# [**Назад**: *Объекты плана тестов*](../test-plan-objects.md)

