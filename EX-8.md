# Ex.No 08 – Creating and Executing Your First Container Using Docker

## Aim
To create and execute your first container using Docker.

## Procedure

### 1. Install Docker
**On Ubuntu:**
```bash
sudo apt update
sudo apt install docker.io
sudo docker run hello-world   # verify installation
```
For macOS or Windows, follow Docker's official installation guides.

### 2. Create the Project
Create a folder containing:
```
project/
├── Dockerfile
└── main.py
```

### 3. Write the Python File (`main.py`)
```python
#!/usr/bin/env python3
print("Docker is magic!")
```

### 4. Write the Dockerfile
```dockerfile
# Import the base image
FROM python:latest

# Copy the python file into the image
COPY main.py /

# Command to run when the container starts
CMD [ "python", "./main.py" ]
```

### 5. Build the Docker Image
```bash
docker build -t python-test .
```

### 6. Run the Docker Image
```bash
docker run python-test
```
Expected output:
```
Docker is magic!
```

## Useful Docker Commands
```bash
docker image ls                       # list images
docker image rm [image name]          # delete a specific image
docker image rm $(docker images -a -q)  # delete all images
docker ps -a                          # list all containers
docker stop [container name]          # stop a specific container
docker stop $(docker ps -a -q)        # stop all containers
docker rm [container name]            # delete a stopped container
docker rm $(docker ps -a -q)          # delete all stopped containers
docker logs [container name]          # view container logs
```

## Result
A Docker container was successfully created and executed.
