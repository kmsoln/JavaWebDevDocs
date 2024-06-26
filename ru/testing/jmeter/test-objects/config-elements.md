# Элементы конфигурации (Config Elements)

Конфигурационные элементы (Configuration elements) позволяют задать настройки "по умолчанию" для некоторых видов
запросов, что позволяет оптимизировать ввод повторяющихся данных (например, если необходимо протестировать несколько
сервисов, размещенных на одном сайте). Например, в элементе HTTP Request Defaults задаются настройки "по умолчанию" для
HTTP-запросов, в т.ч. адрес веб-сервера (URL или IP- адрес), порт веб-сервера (по умолчанию 80), протокол (по умолчанию
HTTP), путь к запускаемому файлу на сервере, передаваемые параметры и их значения.

Конфигурационные элементы HTTP Cookie Manager и HTTP Authorization Manager позволяют управлять в потоке куки и
аутентификацией, что обеспечивает поддержку сеансов пользователя.

При настройке любых типов элементов сценария можно использовать переменные, например, так: `“${varname}”`. Создать
переменные и установить их значения можно в таблице User Defined Variables элемента Test Plan или в конфигурационном
элементе User Defined Variables.

# [**Назад**: *Объекты плана тестов*](../test-plan-objects.md)