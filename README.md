# podman_docker_cheatsheet
also see: https://github.com/lineality/clean_up_podman_docker_guide



# docker stats:
This does not log, but shows resource use in real time.
```bash
docker stats
```
Shows:
```
CONTAINER ID   NAME             CPU %     MEM USAGE / LIMIT     MEM %     NET I/O           BLOCK I/O   PIDS
```

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

#### Custom Docker File Alternate File
```bash
sudo docker build -t PROJECT_NAME -f /path/to/your/Dockerfile .
```
```bash
podman build -t PROJECT_NAME -f /path/to/your/Dockerfile .
```
#### Run
run container
- If your server is exposed at a given port, say 5000, and you want to test it at the same number, have both numbers be that same number -> 5000:5000
```bash
docker run -p 5003:5000 PROJECT_NAME
```
```bash
podman run -p 5003:5000 PROJECT_NAME
```

#### Run with Environment Variables
```bash 
docker run -e DB_HOST=localhost -e DB_PORT=5432 -p 5003:5000 PROJECT_NAME
```
```bash
podman run -e DB_HOST=localhost -e DB_PORT=5432 -p 5003:5000 PROJECT_NAME
```

#### Test
test server, port forward
```
```

https://hub.docker.com/_/python/
