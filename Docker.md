
# Docker


### Что бы отчистить все образы можно использовать следующий пример
___
example: `docker system prune -a --volumes` 
___
### Что бы открыть порты для приложения в контейнере использующего их можно выполнить команду по следующему примеру
___
example: `docker run -d -p 80:80 nginx`
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
___
### Volumes 
___
Необходимо явно указывать директорию монтирования для директорий используемую приложением в случае с nginx это будет /usr/share/nginx/html в таком случае при удалении контейнера или его случайном отключении, или патче/обновлении до определенной версии мы явно сможем указать место где приложение может взять данные для работы с 

`docker run --name test_vol_1 -p 80:80 -d -v /opt/nginx/data:/usr/share/nginx/html nginx`


Распространненный и часто используемый способ это хранить именной volume, в таком случае при создании volume мы получаем не его хеш а его именной раздел монтируемый в приложении вот один из примеров. Так же можно отметить что в случае создания раздела таким способом можно явно понять какой это был контейнер при его пересоздании.

`docker run --name test_vol_1 -p 80:80 -d -v web_data:/usr/share/nginx/html nginx`

Что произойдет в таком случае?

Ответ: в разделе /var/lib/docker/volume создается директория с данными приложения это хороший способ использования пространства хранения контейнеров.

Посмотреть список созданных разделов можно с помощью команды 

`docker volume ls `
___
### DockerNetworks

Посмотреть сети docker: `docker network ls`

Типы сетей в docker: 

bridge, Host, None, macvlan, ipvlan.

Создание сети практические примеры: 

`docker network create myint_a`

`docker network create -d bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 MyNet192`  