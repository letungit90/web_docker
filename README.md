## About 
This an packages that using in develop (and production) environment

| Image/Package | Version | Description |
|---------------|---------|-------------|
| PHP | 7.2.4 | Programming language |
| xdebug | 2.6.0 | Debug library for PHP |
| composer | 1.6.4 | PHP package management system |
| nginx | 1.13.12 | Web server |
| Mysql | 5.7.12 | Database management system |
| Redis | 3.2.10 | Cache management system |

## How to setup

1. Install DockerCE
- If you use MAC, Download and install DockerCE for Mac from following link.

```
https://download.docker.com/mac/stable/Docker.dmg
```

- If you use Linux (Ubuntu), Download and follow instructions in following link to install Docker for Linux.

```
https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce
```

2. Install docker-sync
- Install docker-sync as guide in following link
```
https://github.com/EugenMayer/docker-sync/wiki/1.-Installation
```

3. Build Docker Containers
- Start Docker CE that installed before
- change current working directory to here
```
docker-compose build
```

4. Create your .env file

```
XDEBUG_PROFILER_ENABLE=0
XDEBUG_PROFILER_OUTPUT_DIR=/tmp
XDEBUG_REMOTE_PORT=9002
XDEBUG_IDEKEY=PHPSTORM
XDEBUG_REMOTE_HOST=host.docker.internal
MYSQL_TIME_ZONE=Asia/Tokyo
```

5. Start Docker
- Start docker CE engine

```
docker-sync-stack start
```

- If has no any errors, mean setup successful!

6. Change .env file of Laravel project

```
DB_CONNECTION=mysql
DB_HOST=docker-mysql
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=root
DB_PASSWORD=root

CACHE_DRIVER=redis
SESSION_DRIVER=redis

REDIS_HOST=docker-redis
```

7. Access Database
You can use sequel pro or Mysql workbench with following configurations to access database.

```
Host: 127.0.0.1
Username: root
Password: root
Database: db_name
Port: 3333
```

8. Change hosts file
In local machine, Add bellow config to「/etc/hosts」file.
```
127.0.0.1 localhost.com
```

9. Some Docker commands

```
## Start docker
docker-sync-stack start

## Stop docker
docker-sync-stack clean

## Confirm docker containers status
docker ps

## Access into docker container
docker exec -it {container_name} bash

Example: docker exec -it bt-php bash

## Stop and remove containers
docker-compose down

```

