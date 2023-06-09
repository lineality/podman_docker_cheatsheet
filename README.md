# podman_docker_cheatsheet


#### Start 
start docker daemon
```
$ systemctl start docker
or
$ sudo systemctl start docker
```

#### Build
build image
```
$ sudo docker build -t PROJECT_NAME .
$ podman build -t PROJECT_NAME .
```

#### Run
run container
```
$ docker run -p 5003:5000 PROJECT_NAME
$ podman run -p 5003:5000 PROJECT_NAME
```

#### Test
test server, port forward
```
```

https://hub.docker.com/_/python/
