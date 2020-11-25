## Verified to work in Release
This project was derived from the sparkjava project in [awesome-compose](https://github.com/docker/awesome-compose)

No modifications to this project were necessary to make it work in Release.

To make this project run in [Release](https://releaseapp.io), simply create a new application with this repository.

## Compose sample application
### Spark Java

Project structure:
```
.
├── docker-compose.yaml
├── README.md
└── sparkjava
    ├── Dockerfile
    └── ...
```

[_docker-compose.yaml_](docker-compose.yaml)
```
version: "3.7"
services:
  sparkjava:
    build: sparkjava
    ports:
    - 8080:8080
```
The compose file defines an application with one service `sparkjava`.
When deploying the application, docker-compose maps port 8080 of the sparkjava service container to port 8080 of the host as specified in the file.
Make sure port 8080 on the host is not already being in use.

## Deploy with docker-compose

```
$ docker-compose up -d
Creating network "sparkjava_default" with the default driver
Building sparkjava
Step 1/11 : FROM maven:3.6.3-jdk-11 AS build
3.6.3-jdk-11: Pulling from library/maven
...
Successfully tagged sparkjava_sparkjava:latest
WARNING: Image for service sparkjava was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating sparkjava_sparkjava_1 ... done
```

## Expected result

Listing containers must show one container running and the port mapping as below:
```
$ docker ps
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                  NAMES
5af94cb25394        sparkjava_sparkjava   "/bin/sh -c 'java -j…"   20 seconds ago      Up 19 seconds       0.0.0.0:8080->8080/tcp   sparkjava_sparkjava_1
```

After the application starts, navigate to `http://localhost:8080` in your web browser or run:
```
$ curl localhost:8080
Hello from Docker!
```

Stop and remove the containers
```
$ docker-compose down
Stopping sparkjava_sparkjava_1 ... done
Removing sparkjava_sparkjava_1 ... done
Removing network sparkjava_default
```
