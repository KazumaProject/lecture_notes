# Notes of Docker Udemy

## Section4

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

## dockerのimageを削除する
```bash
docker rmi <DOCKER_HUB_USER_NAME>/my-first-repo
```

## pullしたimageからcontainerを起動する
```bash
docker run -it <DOCKER_HUB_USER_NAME>/my-first-repo bash
```

## Section 5

## `docker run`は`docker create` + `docker start`

## `docker start`ではdefaultの実行結果を見ることができない
実行結果をみるには
```bash
docker start <CONTAINER_ID> -a
```
defaultのcommandは`docker ps -a`の`COMMAND`

## docker run -it
> -i : インプット可能
>
> -t : 表示が綺麗になる

## containerを削除する
```bash
docker rm <CONTAINER_ID>
docker rm <NAME>
```

## containerをstopする
```bash
docker stop <CONTAINER_ID>
docker stop <NAME>
```

## 止まっているcontainerを全削除
```bash
docker system prune
```

## コンテナ名を指名してrunする
```bash
docker run --name <NAME> <IMAGE>
```

## container 起動後にdetachする(backgroundで動かす)
```bash
docker run -d <IMAGE>
```

## containerをexin後に削除する(一回きりのcontainer)
