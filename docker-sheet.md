# understanding docker.

## Understanding how computer systems work.

Namespace - used to isolate resources per processes.
Control Group - used to control amount of resources used by the processes.

## Quick docker commands

|command | What it does |
|---- | ---- |
|`docker ps` | Lists all running processes |
|`docker ps -a` | List all containers that have run since beginning of time |
|`docker create <image_name>` | Just creates a container from the image |
|`docker start <container_id>` | Executes the primary command |
|`docker start -a` | Takes the output from the container and takes the output and displays it |
|`docker system prune` | deletes everything including cache |
|`docker logs <container_id>` | logs output the container |
|`docker stop <container_id>` | slow/safe stop the container |
|`docker kill <container_id>` | instant kill |

### Level 2

|command | What it does |
|---- | ---- |
|`docker exec -it <container_id> <command>` | Execute commands inside running docker container. **-it** allows to interact directly with the container. |
|`docker exec -it <container_id> sh` | Run shell into the docker container. and do things there |
|`docker build .`| `To build a docker file. Generates a image_id |
|`docker build -t <docker_id>/<project_name>:<version> .` | `To build and tag a new docker image with a name.|

### Level 3

|command | What it does |
|----- | ----- |
|`docker commit` | generating images from an container after running certain programs. |
|`docker -v <bookmark_nonreference_file_location> -v <localhost>:<reference_file_location>` | Attaching volumes from local machine to container, just like ports. You can also select the folders/files you want to skip, or not refer. |
|`docker attach` | Attach STDIN, STDOUT, ERR to container |

## Docker Compose
|command | What it does |
|----- | ----- |
|`docker-compose up `| Build & run docker-compose.yml |
|`docker-compose up -d ` | Run command in background |
|`docker-compose down `| Stop all containers from compose |
|`docker-compose up -d --build` | Building from new |
|`docker-compose ps`| Only works when run from appropriate directory |


### Example 'docker-compose.yml' file
```yml
version: '3.7'            # version number


services:               # essentially saying container.
  redis-server:         # container-name
    image: 'redis'      # take 'image' from
    restarts: always    # restart the container. "NO" by default.
  node-app:
    build: .            # build container from code
    ports: 
        - "4001<localhost-port>:8081<container-port>"  # map port <localhost-port:container-port>
    volumes:
      - 
```




## Docker Understanding

**Alpine** : Alpine base image has all the necessary requirements to run docker systems, just like Ubuntu, MacOS etc.\

**Cache** : Docker cache is powerful and uses snapshot from previously done work and uses it instead of doing everything again. **Order of steps is important.**

**Port mapping** : Map localhost network ports with the container ports. So requests are automatically redirected.

**Volumes**: Mapping of folder inside the localhost to the container.

## Docker-compose Understanding

**Docker compose** : Essentially composes multiple containers into one package and provides networking (communication) between the containers. (so OS with multiple containers.)

Notes:

* Remember to reference the containers, inside another container setting.. 


## Dockerfile settings

**COPY** : Copy files from localhost to container.
**CMD** : Run the commmand after the container has started.
**WORKDIR** : All commands will be executed relative to this path.
**RUN** : Runs inside the terminal of the container.