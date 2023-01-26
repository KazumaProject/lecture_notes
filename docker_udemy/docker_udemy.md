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
> - network
> - container
> - image
> - data volumes

## COPY
hostからcontainerにcopyする
```Dockerfile
COPY <src> <dest>

FROM ubuntu:latest
RUN mkdir /new_dir
COPY something /new_dir/
```

## COPY vs ADD
- 単純にfileやfolderをcopyする場合は`COPY`
- tarの圧縮ファイルをコピーして解凍したいときは`ADD`

```bash
tar -cvf compressed.tar sample_folder
```

## Dockerfileがbuild contextにない場合
```bash
docker build -f <docker_file_name> <build_context>
```
`Dockerfile.dev`

`Dockerfile.test`

```bash
docker build -f ../Dockerfile.dev .
```

## CMD vs ENTRYPOINT
- ENTRYPOINTでもdefaultのcommandを指定することができる
> - ENTRYPOINTは,run時に上書きできない
> - ENTRYPOINTがある場合はCMDは["param1", "param2"]の形を取る
>
>	 つまりCMDはENTRYPOINTの引数となる
> - run時に上書きできるのはCMDの部分のみ
> - containerをcommandのようにして使いたい時に使う

```Dockerfile
FROM ubuntu:latest
RUN touch test
CMD ["ls","--help"]
```

```Dockerfile
FROM ubuntu:latest
RUN touch test
ENTRYPOINT ["ls"]
CMD ["--help"]
```

## ENV :環境変数を設定する

```Dockerfile
ENV <key> <value>
ENV <key>=<value> ...
```

```Dockerfile
FROM ubuntu:latest
ENV key1 this_is_value1
ENV key2=this_is_value2
ENV key3="H e l l o , W o r l d !" key4=j\ o\ h\ n
ENV key5 v a l u e
```

全ての環境変数を表示する
```bash
env
```

## WORKDIR
Docker instructionの実行directoryを変更する

- Docker instructionはrootで実行される

```Dockerfile
FROM ubuntu:latest
RUN mkdir sample_folder
RUN cd sample_folder
RUN touch sample_file
```
sample_fileはroot下に作られる

```Dockerfile
FROM ubuntu:latest
# RUN mkdir sample_folder
WORKDIR /sample_folder
RUN touch sample_file
```
sample_fileはsample_folder下に作られる
runした際にsample_folderに移動されている

</details>

<details>

<summary> Section 9 ホストとコンテナの関係を理解する </summary>

## -vオプションでファイルシステムを共有する

> -v < host >:< container >

```bash
docker run -it -v ~/Documents/docker_projects/mounted_folder:/new_dir <image> bash

docker_projects % docker run -it -v ~/Documents/docker_projects/mounted_folder:/new_dir 0fd6b702080e1f5fdd222e bash
```

mountされたhostのファイルはhost内にある。container内には無い。
-vで指定するfolderがcontainer無いにない場合、自動的に作られる

## -uオプションでホストとコンテナのアクセス権限を共有する

> -u <user_id>:<group_id>

```bash
docker run -it -u $(id -u):$(id -g) -v ~/Documents/docker_projects/mounted_folder:/created_in_run <image> bash
```

- User IDを表示
```bash
id -u
```

- Group IDを表示
```bash
id -g
```

## -pオプションでホストとコンテナのポートを繋げる

> -p <host_port>:<container_port>

```bash
docker run -it -p 8888:8888 --rm jupyter/datascience-notebook bash
```
browserからlocalhost:8888

```bash
docker run -it -p 1234:8888 --rm jupyter/datascience-notebook bash
```
browserからlocalhost:1234

## containerで使えるコンピュータリソースの上限を設定する
> --cpus <# of CPUs> : コンテナがアクセスできる上限のCPUを設定
>
> --memory < byte > : コンテナがアクセスできる上限のメモリを設定

macでCPU,メモリの確認
```bash
sysctl -n hw.physicalcpu_max #物理コア数 
sysctl -n hw.logicalcpu_max #論理コア数
sysctl hw.memsize #メモリ(byte)
```

```bash
docker inspect <container_id>
docker inspect <container_id> | grep -i cpu
docker inspect <container_id> | grep -i memory
```

</details>

<details>
<summary> Section 10 応用編1-1 </summary>

## Dockerでデータサイエンスの解析環境を構築する
1. build contextは`dsenv_build` folder
2. containerはubuntuでAnacondaとJupyter labをインストールする
3. Hostのbuild context内のcodeをcontainerにmountしてファイルシステムを共有する
4. Hostのportとcontainerのportを`8888`でつなげる

```bash
FROM ubuntu:latest
RUN apt-get update && apt-get install -y \
    sudo \
    wget \
    vim
WORKDIR /opt
RUN wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
CMD ["jupyter lab"]
```


</details>
