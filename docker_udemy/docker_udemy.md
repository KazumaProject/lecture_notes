# Notes of Docker Udemy

<details>

<summary>Section4</summary>

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

</details>

<details>
<summary> Section 5 </summary>

## docker runはdocker create + docker start

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
docker run -it -d ubuntu bash
```

## containerをexit後に削除する(一回きりのcontainer)
```bash
docker run --rm <IMAGE>
docker run --rm hello-world
```

</details>

<details>

<summary> Section 6 DockerFileについて知ろう</summary>

## Dockerfileとは
- Docker imageの設計図でDockerfileからDocker imageを作る
- Dockerfileというファイル名のテキストファイル
- INSTRUCTION argumentsの形で記載していく

```Dockerfile
FROM ubuntu:latest
# testファイルを作成
RUN touch test
```

## DockerfileからDocker imageを作成する
```bash
docker build <DIRECTORY>
docker build .

docker build -t <NAME> <DIRECTORY>
docker build -t new-ubuntu:latest .
```

- danglingを表示する
```bash
docker images -f dangling=true
```

</details>

<details>

<summary> Section 7 - Docekrfileの書き方 </summary>

## FROM
Dockerfileは`FROM`から書き始める
`FROM`はほとんどの場合OSを指定

## RUN
- Linuxコマンドを実行
- RUNを使うことで好きにカスタマイズ
- RUN毎にLayerが作られる

## Layer数を最小限にするために
- Docker imageのLayer数は最小限にする
- Layerを作るのは`RUN`, `COPY`, `ADD`
- コマンドを&&でつなげる
- \ で改行する

```Dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install \
xxx \
xyz \
yyy \
zzz
```

## cacheの使用
- cacheはLayerごとに保存される
- cacheを使用してDockerfileを作成して最終的に&&でつなげる

```Dockerfile
FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y \
curl \
nginx
RUN apt-get install -y cvs
```

最終的
```Dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y \
curl \
cvs \
nginx
```

## CMD
- containerのdefaultのcommandを指定
```Dockerfile
CMD["executable", "parames1", "parames2"]
```
- 原則Dockerfileの最後に記述
- CMDは1つのみ

ubuntuの`/bin/bash`はDockerfileのCMDで定義されている
```Dockerfile
CMD ["bash"]
```

## RUNとCMDの違い
- RUNはLayerを作る,CMDは作らない
- 保存したい内容: `RUN`
- `docker run`で起動するときに実行したい場合: `CMD`
</details>

<details>
<summary> Section 8 - docker buildの詳細と、その他のInstruction</summary>

## Docker deamonとは
- docker deamonがある場所を`DOCKER_HOST`と呼びclientから命令を出す
- docker objectsを管理するもの
> docker objects
> - newwork
> - container
> - image
> - data volumes

</details>
