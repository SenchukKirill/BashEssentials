### DockerNetworks

Посмотреть сети docker: `docker network ls`

Типы сетей в docker: 

bridge, Host, None, macvlan, ipvlan.

Создание сети практические примеры: 

`docker network create myint_a`

`docker network create -d bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 MyNet192`  