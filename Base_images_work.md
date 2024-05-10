# Базовые команды работы с Docker.

# Получить список работающих контейнеров `docker ps`

# Получить список всех конейнеров (в том числе остоновленных) `docker ps -a`

# Полная очистка images из docker.

## example: `docker system prune -a --volumes` 

___
### В случае если используется несколько приложений в контейнере которые работают на одинаковом порте в контейнере моожно поступить так, использовать значение до двоеточия что бы описать порт который мы хотим задать второму приложению использующему тот же порт
___

example: `docker run -d -p 8080:80 nginx`
___
### В случае если мы испытываем проблемы с использованием контейнера (Не запускается, не работает должным образом) мы можем воспользоваться функцией логгирования в docker:
___
`docker logs mysql_3` где mysql_3 будет именем контейнера

`
2024-05-01 14:50:15+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.0-1.el8 started.
2024-05-01 14:50:15+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2024-05-01 14:50:15+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.0-1.el8 started.
2024-05-01 14:50:15+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified
    You need to specify one of the following as an environment variable:
    - MYSQL_ROOT_PASSWORD
    - MYSQL_ALLOW_EMPTY_PASSWORD
    - MYSQL_RANDOM_ROOT_PASSWORD
`
В данном примере возникает ошибка на этапе инициализации DB, из-за отсутствия одной из перечисленных переменных окружжения, требуется исправить это и явно задать пароль для подключения к DB mysql.

В данном случае правильной инициализацией будет:

`docker run --name DB_mysql -e MYSQL_ROOT_PASSWORD=password -d mysql`
