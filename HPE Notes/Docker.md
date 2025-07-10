**Build Docker Image from Dockerfile**
`docker build -t <image_name> <dockerfile_dir>`

**Load image from tarball**
`docker load -i <file.tar>`

**Pull image from artifactory**
`docker image pull <repository>:<tag>`

**List Images**
`docker image ls -a`

**List Containers
`docker ps -a`
`docker container ls -a`

**Inspect Image
`docker inspect <image-id>`

**Run Container**
Detached:
`docker run -d <repo>:<tag>`
Exec:
`docker run -it --entrypoint /bin/bash <image>`
Service:
`docker run -it -p <host_port>:<service_port> --name <container_name> <image>`

**Remove Containers**
Specific:
`docker container rm <container_id>`
All:
`docker container rm -f $(docker ps -qa)`

**Remove Images**
Specific:
`docker image rm <image_id>`
All:
`docker image rm -f $(docker image ls -qa)`

**Full Clean up**
`docker system prune -a
`docker builder prune -a
`docker image prune -a`
