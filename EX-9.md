# Ex.No 09 – Run a Container from Docker Hub

## Aim
To run a container from Docker Hub.

## Procedure

### 0. Explore Docker CLI
```bash
docker -h          # list available commands
docker version      # check client/server version
```

### Step 1: Run Your First Container
Run a container using the `ubuntu` image with the `top` command:
```bash
docker container run -it ubuntu top
```
This pulls the `ubuntu` image (if not present locally) and starts the container, showing live process stats.

**Inspect the running container** (from a new terminal):
```bash
docker container ls                     # get the container ID
docker container exec -it <ID> bash     # enter the container's namespace
ps -ef                                   # inspect running processes inside
exit                                     # leave the container shell
```

Clean up:
```bash
docker ps -a
docker rm <CONTAINER_ID>
```

### Step 2: Run Multiple Containers

**Run an Nginx server:**
```bash
docker container run --detach --publish 8080:80 --name nginx nginx
```
Access it at `http://localhost:8080` — returns the Nginx welcome page.

**Run a MongoDB server:**
```bash
docker container run --detach --publish 8081:27017 --name mongo mongo:4.4
```
Access it at `http://localhost:8081` — returns a message that you're accessing MongoDB over HTTP on its native driver port (expected behavior, confirms it's running).

**Check running containers:**
```bash
docker container ls
```

### Step 3: Clean Up
```bash
docker container ls                 # list running containers
docker container stop <ID1> <ID2> ...   # stop each container
docker system prune                 # remove stopped containers, unused volumes/networks, dangling images
```

## Result
A container was successfully run from Docker Hub (Ubuntu, Nginx, and MongoDB images), verified, and cleaned up.
