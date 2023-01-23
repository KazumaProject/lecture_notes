# Notes of Docker Udemy

## 環境変数
```bash
export AGE=20
echo $AGE
```

## hello world projectをpullする
```bash
docker pull hello-world
```

## docker imagesを表示
```bash
docker images
```

## containerをimageから作成する
```bash
docker run hello-world
```

## docker containersを表示
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

## Containerから出る
```bash
exit
docker dettach
```

## Containerを再度起動する
- exit
```bash
 docker restart <CONTAINER_ID>
 docker exec -it <CONTAINER_ID> bash
```
- detach
```bash
docker attach <CONTAINER_ID>
```

## 更新内容をDocker imageにする
```bash
docker commit <CONTAINER_ID> <NEW_IMAGE_NAME>
docker commit <CONTAINER_ID> ubuntu:updated
```

## Docker imageを別名で保存
```bash
docker tag <SOURCE> <TARGET>
docker tag ubuntu:updated <DOCKER_HUB_USER_NAME>/my-first-repo
```

## Docker Hubに imageをpushする
```bash
docker push <REPOSITORY_NAME>
```

