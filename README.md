# Environnement Docker for Symfony 5

_Inspired from Yoandev Youtube Channel, link [here](https://youtu.be/tRI6KFNKfFo)_

Creation of containers PHP-Apache / MySql / PHPMyAdmin / MailDev for Symfony 5 projects.

Below, see commands to init the project and test it as you want:

```shell
# Build images & run the docker-compose
docker-compose build
docker-compose up -d
```

## Interact with the project in the docker container

```shell
# Enter the container (the exit)
docker exec -it docker_symfony_php bash
exit

# Init a Symfony project
# docker exec docker_symfony_php symfony new project --full
docker exec -it docker_symfony_php bash

symfony new project --full
cd project
echo "DATABASE_URL=mysql://root:@docker_symfony_db:3306/test?serverVersion=5.7" > .env.local

symfony console doctrine:database:create
# docker exec -it docker_symfony_php symfony console doctrine:database:create
symfony console make:entity
# docker exec -it docker_symfony_php symfony console make:entity
symfony console make:migration
# docker exec -it docker_symfony_php symfony console make:migration
symfony console doctrine:migrations:migrate
# docker exec -it docker_symfony_php symfony console 

exit
```

## Interact with the project outside the docker container

```shell
symfony new project --full
cd project

echo "DATABASE_URL=mysql://root:@docker_symfony_db:3306/test?serverVersion=5.7" > .env.local

symfony console doctrine:database:create
symfony console make:entity
symfony console make:migration
symfony console doctrine:migrations:migrate
```

Commands to interact with containers and global project

```shell
# To force build the PHP custom container
cd php
docker build . --no-cache

# To delete the project 
sudo rm -rf project
```
