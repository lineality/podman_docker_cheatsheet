# podman_docker_cheatsheet


####	To turn off requiring-sudo for docker: 
```bash
sudo usermod -a -G docker $USER
```

#### Start 
start docker daemon
```bash
sudo systemctl start docker
```

#### Build
build image
```bash
sudo docker build -t PROJECT_NAME .
```
```bash
podman build -t PROJECT_NAME .
```

#### Run
run container
- If your server is exposed at a given port, say 5000, and you want to test it at the same number, have both numbers be that same number -> 5000:5000
```
$ docker run -p 5003:5000 PROJECT_NAME
$ podman run -p 5003:5000 PROJECT_NAME
```

#### Test
test server, port forward
```
```

https://hub.docker.com/_/python/
