# DockerNetworks

# Открытие портов на server:docker-container

## `docker run -d -p 80:80 nginx` первым параметром указан тот порт который мы хотим открыть на сервере в котором используем docker. Вторым параметром указывается порт открывающийся на docker container.

# Отобразить список сетей в docker.

##  `docker network ls`

# Типы сетей в docker: 

## Bridge, Host, None, Macvlan, ipvlan. 

### Brigde - тип сети использующаяся в Docker по умолчаниюю при создании контейнера. Нет возможности использовать DNS - Domain Name System. В ней можно обращаться к контейнерам в этой же сети (Bridge) по ipV4-address.

### Host - тип сети, который использует ipv4 адресацию хоста. 

### None - Тип сети не использующий ip.

# Примеры создания сети

## `docker network create myint_a`

### В таком случае будет создана сеть с параметром --drive bridge.  

## `docker network create -d bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 MyNet192`  

### В таком случае будет создана сеть с определенным --subnet и --gateway.

# Так же мы имеем возможность подключить определенный docker container в режиме up

## `docker network connect bridge test`

### На место bridge указываем существующую сеть на место test указываем имя/id контейнера.

# Если мы хотим отключить docker от определенной сети можем воспользоваться данной инструкцией: 

## `docker network disconnect <network id> <container_name>`

### Получить network_id можно с помощью комманды `docker inspect <network>` 