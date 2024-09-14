Обычная конструкция, которую любят разработчики, выглядит так: запуск сервиса сделать скриптом, который сначала накатывает миграции на БД, а потом запускает основной сервис.

Такая конструкция конфликтует с облачными окружениями типа кубернетеса или cloud run, которые любят часто перезапускать сервисы при разных обстоятельствах.Типичный сценарий фейла, который я часто видел такой:  

- есть alembic (система миграции для sqlalchemy)
- alembic при миграции смотрит на текущую версию миграций в БД, если она старая - накатывает дельту
- если алембик видит версию, которую не знает - он падает с ошибкой
- когда алембик видит неизвестную версию? когда произошел неудачный релиз, что-то идет не так и надо срочно откатываться на предыдущую версию

В такой ситуации сервис в огне: новая версия не работает по причине багов, а откат на старую не работает, потому что запуск старой версии падает при миграции перед запуском.Аналогично, можно представить сценарий фейла для любой другой системы наката миграций, главное, чтобы был кейс в котором она падает при каком-то стечении обстоятельств.

Поэтому я не люблю связывать миграции и запуск, и всем рекомендую контролируемо катить миграции руками сохраняя N+/-1 совместимость базы и кода.


----

  
A typical setup favored by developers often looks like this: a service is launched via a script that first rolls out database migrations and then initiates the main service.

However, this approach clashes with cloud environments such as Kubernetes or Cloud Run, which frequently restart services under various conditions. A common failure scenario I've frequently observed goes like this:

- There's Alembic, a migration system for SQLAlchemy.
- During the migration process, Alembic checks the database for the current migration version. If it's outdated, it applies the necessary updates.
- If Alembic encounters an unrecognized version, it fails and returns an error.
- When does Alembic encounter an unknown version? Typically, when there's been a botched release, things are going awry, and there's an immediate need to revert to a previous version.

In such instances, the service is in a critical state: the new version is dysfunctional due to bugs, and reverting to an older version fails because the migration process crashes before the old version can start. This issue could similarly arise in other migration systems, especially under specific adverse conditions.

Therefore, I'm not in favor of linking migrations with service startup. Instead, I advise a controlled, manual approach to migration, ensuring that the database and code maintain N+/-1 compatibility.