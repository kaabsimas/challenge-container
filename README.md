# Teste

Aplicação de teste para encapsulamento de aplicações em continainers docker

## Setup

Execute:

```
docker-compose up -d
```

Remontar caso haja alguma alteração no docker-compose ou Dockerfile:

```
docker-compose build --no-cache
```

Em seguida deve-se instalar as dependências do projeto com o composer e configurar as variáveis de ambiente. Para isso é necessário acessar o bash do container php-apache:

```
$ docker-compose run php-apache bash

Starting challenge-container_database_1 ... done
user@31b694672ba8:/var/www/nr-challenge$  
```

E então no bash:

```
composer install
cp .env.example
php artisan key:generate
php artisan migrate
```

## Banco de dados

O volume utilizado para o banco de dados é o nr_challenge_mysql. Ele pode ser listado com o comando `docker volume ls`, onde aparecerá com o nome do diretório do projeto prefixado.
Exemplo, se você salvar o projeto numa pasta chamada challenge-container:

```
$ docker volume ls 
DRIVER    VOLUME NAME
local     challenge-container_nr_challenge_mysql
```

E pode ser inspecionado com `docker volume inspect challenge-container_nr_challenge_mysql`

```
$ docker volume inspect nr_challenge_mysql
[
    {
        "CreatedAt": "2022-06-01T11:40:44-03:00",
        "Driver": "local",
        "Labels": {
            "com.docker.compose.project": "challenge-container",
            "com.docker.compose.version": "1.25.0",
            "com.docker.compose.volume": "nr_challenge_mysql"
        },
        "Mountpoint": "/home/user/.local/share/docker/volumes/challenge-container_nr_challenge_mysql/_data",
        "Name": "challenge-container_nr_challenge_mysql",
        "Options": null,
        "Scope": "local"
    }
]
```