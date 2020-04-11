---
Title: "Docker"
Description: TODO
tags: ["docker", "computer-science"]
draft: true
---

# Get started with Docker

## Finding and retrieving a Docker Container
```
$ docker search hello-world
$ docker pull hello-world
$ docker run hello-world
or 
$ docker search hello-world
$ docker run hello-world
```
As you can see in the second example, the `pull` comand can be included in the `run` one as a subcommand.


## Running a Docker Container
```
$ docker run -it ubuntu
```

## Managing
```
$ docker images
```

```
$ docker ps -a or docker ps -l
```

```
$ docker ps -a
```

## Tutorials
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04

## Acknowledgements
https://hub.docker.com
