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
user@31b694672ba8:/var/www/src$  
```

## Banco de dados

O volume utilizado para o banco de dados é o mysql_volume. Ele pode ser listado com o comando `docker volume ls`, onde aparecerá com o nome do diretório do projeto prefixado.
Exemplo, se você salvar o projeto numa pasta chamada challenge-container:

```
$ docker volume ls 
DRIVER    VOLUME NAME
local     challenge-container_mysql_volume
```

E pode ser inspecionado com `docker volume inspect challenge-container_mysql_volume`

```
$ docker volume inspect mysql_volume
[
    {
        "CreatedAt": "2022-06-01T11:40:44-03:00",
        "Driver": "local",
        "Labels": {
            "com.docker.compose.project": "challenge-container",
            "com.docker.compose.version": "1.25.0",
            "com.docker.compose.volume": "mysql_volume"
        },
        "Mountpoint": "/home/user/.local/share/docker/volumes/challenge-container_mysql_volume/_data",
        "Name": "challenge-container_mysql_volume",
        "Options": null,
        "Scope": "local"
    }
]
```