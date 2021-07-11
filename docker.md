- [Docker](#docker)
- [Flow](#flow)
  - [Basic](#basic)
  - [With volumes and network](#with-volumes-and-network)
- [Docker Compose](#docker-compose)
  - [Example docker-compose.yaml](#example-docker-composeyaml)
- [CI/CD](#cicd)
- [Language specific](#language-specific)
- [Run app in production](#run-app-in-production)
# Docker

- containerizing of programs(running them in seperate processes) using linux `namespaces` and `cgroups`
- write `Dockerfile` in app root to build image using docker `docker build`
- may need different containers for *app* and *DB*.
- could mount db file as ***docker named volume*** into *app*
- docker can create network to talk to different containers on same network
  - app container talks to db container
- mangement of multiple containers by **Container Orchestration Frameworks** like Kubernetes 

# Flow
## Basic
- write `Dockerfile`
```Docker
 # syntax=docker/dockerfile:1
 FROM node:12-alpine
 RUN apk add --no-cache python g++ make
 WORKDIR /app
 COPY . .
 RUN yarn install --production
 CMD ["node", "src/index.js"]
```
- build using `docker build -t app_docker .`
    - `-t` => `--tag`
    - `.` => create build from current directory
- run your build using `docker run -dp 3000:3000 app_docker`
    - `-d` -> background mode
    - `-p` -> map container port to host port

## With volumes and network
- volumes are data stores in filesystem and images can be built along with them. 
  - (ex: db is stored in a different file, and want to use it as persistend db across builds)
- 

# Docker Compose 
- create containers with services and volumes defined in a `docker-compose.yaml` file
- `docker compose up` automatically creates a network
- `-d` to run in background
- define `services` and `volumes` in the yaml
  - services may contain different app labels and define
    - `image` - image to to be used
    - `command` - optional commands
    - `port` - mapping of port of container to host
    - `working_dir`
    - `volumes` - named volumes(defined in top level volumes prop) or bound(as paths)
    - `environment` - various properties related to env vars.
- images can be fetched from docker hub `node12:alpine`, `mysql:5.7`
## Example docker-compose.yaml
```yaml
version:    "0.1"

servies:
    app:
        image:  django-app
        port:
            - 3000:3000
        working_dir:    /django-app
        volumes:
            -   ./:/app
        environment:
            MYSQL_HOST: mysql
            MYSQL_USER: root
            MYSQL_PASSWORD: password
            MYSQL_DB:   jarvis
    mysql:
        image:  mysql-app
        volumes:
            -   jarvis-app:/var/local/mysql
        environment:
            MYSQL_ROOT_PASSWORD:    password
            MYSQL_DATABASE: jarvis

volumes:
    jarvis-app:

```

# CI/CD

# Language specific

# Run app in production