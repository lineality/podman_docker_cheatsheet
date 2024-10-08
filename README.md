# podman_docker_cheatsheet
also see: https://github.com/lineality/clean_up_podman_docker_guide



### docker stats:
This does not log, but shows resource use in real time.
```bash
docker stats
```
Shows:
```
CONTAINER ID   NAME             CPU %     MEM USAGE / LIMIT     MEM %     NET I/O           BLOCK I/O   PIDS
```

###	To turn off requiring-sudo for docker: 
This may be required for some applications such as azure cli.
```bash
sudo usermod -a -G docker $USER
```

### Start 
start docker daemon
```bash
sudo systemctl start docker
```

### Build
build image
```bash
sudo docker build -t PROJECT_NAME .
```
```bash
podman build -t PROJECT_NAME .
```

### Custom Docker File Alternate File
```bash
sudo docker build -t PROJECT_NAME -f /path/to/your/Dockerfile .
```
```bash
podman build -t PROJECT_NAME -f /path/to/your/Dockerfile .
```
### Run
run container
- If your server is exposed at a given port, say 5000, and you want to test it at the same number, have both numbers be that same number -> 5000:5000
```bash
docker run -p 5003:5000 PROJECT_NAME
```
```bash
podman run -p 5003:5000 PROJECT_NAME
```
Run in interactive mode:
```bash
podman run -it PROJECT_NAME
```

### Run with Environment Variables
```bash 
docker run -e DB_HOST=localhost -e DB_PORT=5432 -p 5003:5000 PROJECT_NAME
```
```bash
podman run -e DB_HOST=localhost -e DB_PORT=5432 -p 5003:5000 PROJECT_NAME
```

### Look at Resources, Memory
Step 1 of 2: Get all containers ID
```bash
podman ps
docker ps
```
Output looks like:
```
CONTAINER ID  IMAGE                COMMAND            CREATED         STATUS         PORTS       NAMES
987654321012  localhost/p2:latest  gunicorn main:app  2 minutes ago  Up 10 minutes  5001/tcp    stringofcharacters
```

Step 2 of 2: look at memory use
```bash
podman stats 987654321012
docker stats 987654321012
```
Output looks like:
```
ID            NAME                    CPU %       MEM USAGE / LIMIT  MEM %       NET IO             BLOCK IO      PIDS        CPU TIME    AVG CPU %
987654321012  stringofcharacters      0.08%       500.6MB / 10.00GB  5.00%       22.35MB / 112.2kB  0B / 8.917MB  18          4.179897s   0.58%
```

https://hub.docker.com/_/python/

# Put .env into Docker Build
```python
import os
import re

def read_env_file(env_file):
    env_vars = {}
    with open(env_file, 'r') as f:
        for line in f:
            line = line.strip()
            if line and not line.startswith('#'):
                match = re.match(r'(\w+)\s*=\s*(.*)', line)
                if match:
                    key, value = match.groups()
                    env_vars[key] = value
    return env_vars

def generate_docker_run_command(env_vars, project_name, port):
    env_args = ' '.join([f'-e {key}={value}' for key, value in env_vars.items()])
    port_mapping = f'-p {port}:{port}'
    command = f'docker run {env_args} {port_mapping} {project_name}'
    return command

if __name__ == '__main__':
    env_file = '.env'
    project_name = 'PROJECT_NAME'
    port = 5002

    env_vars = read_env_file(env_file)
    docker_run_command = generate_docker_run_command(env_vars, project_name, port)
    print(docker_run_command)
```
