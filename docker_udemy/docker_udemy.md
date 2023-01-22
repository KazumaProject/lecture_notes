# Notes of Docker Udemy

## 環境変数
```bash
export AGE=20
echo $AGE
```

## hello world project
```bash
docker pull hello-world
```

## show docker images
```bash
docker images
```

## create docker container from image
```bash
docker run hello-world
```

## show docker containers
```bash
docker ps
docker ps -a
```

## restart docker container
```bash
docker restart <CONTAINER_ID>
```

## restart docker container then start bash
```bash
docker exec -it <CONTAINER_ID> bash
```

## out from container
```bash
exit
docker dettach
```

## come back to the container
- exit
```bash
 docker restart <CONTAINER_ID>
 docker exec -it <CONTAINER_ID> bash
```
- detach
```bash
docker attach <CONTAINER_ID>
```

## Create Docker image from container
```bash
docker commit <CONTAINER_ID> <NEW_IMAGE_NAME>
docker commit <CONTAINER_ID> ununtu:updated
```
