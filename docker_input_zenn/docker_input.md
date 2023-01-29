## Note for [実践 Docker \- ソフトウェアエンジニアの「Docker よくわからない」を終わりにする本](https://zenn.dev/suzuki_hoge/books/2022-03-docker-practice-8ae36c33424b59)

<details>
<summary> コンテナの基本操作 </summary>

### コンテナを起動

```bash
docker container run [option] <image> [command]
docker container run --rm hello-world
```

### コンテナ一覧

```bash
docker container ls [option]
docker container ls -a
```

### コンテナを停止

```bash
docker container stop [option] <container>
```

### コンテナを削除

```bash
docker container rm [option] <container>
docker container rm -f <container_id>
```

### コンテナに名前をつける

```bash
docker container run \
  --name web-server  \
  --rm               \
  --detach           \
  --publish 8080:80  \
  nginx:1.21
```

## コンテナは　`メインプロセス(PID = 1)を実行するために起動する`

### コンテナ内でコマンドを実行する

```bash
docker container exec [option] <container> command
```

### イメージ一覧を確認する

```bash
docker image ls [option]
```

### イメージをpull

```bash
docker image pull [option] <image>
```

### イメージをビルドする

```bash
docker image build [option] <path>

docker image build     \
    --tag my-ubuntu:date \
    .
```

### イメージのレイヤーを確認

```bash
docker image history [option] <image>
```

### `--file`オプション

```bash
docker image build              \
    --tag my-ubuntu:date          \
    --file ~/Documents/ \
    docker_input/date
```
### コンテナに環境変数を設定する

`-e`, `--env`

```bash
docker container run                     \
    --name db                              \
    --rm                                   \
    --platform linux/amd64                 \
    --env MYSQL_ROOT_PASSWORD=rootpassword \
    --env MYSQL_USER=hoge                  \
    --env MYSQL_PASSWORD=password          \
    --env MYSQL_DATABASE=event             \
    docker-practice:db
```

### ブラウザからコンテナにアクセスできない時(port未設定)

```bash
curl localhost:8000
```

```bash
docker container run     \
    --name mail            \
    --rm                   \
    --platform linux/amd64 \
    mailhog/mailhog:v1.0.1
```

### ボリュームを作成

```bash
docker volume create [option]
```

ボリュームは**ホストマシン側のどこに保存されているかは関心がなくとにかくデータを永続化したい**という場合に有用

```bash
docker volume create \
    --name docker-practice-db-volume
```

```bash
docker volume ls
```

### `--volume`オプションによるマウント

```bash
docker container run                                \
    --name db                                         \
    --rm                                              \
    --detach                                          \
    --platform linux/amd64                            \
    --env MYSQL_ROOT_PASSWORD=rootpassword            \
    --env MYSQL_USER=hoge                             \
    --env MYSQL_PASSWORD=password                     \
    --env MYSQL_DATABASE=event                        \
    --volume docker-practice-db-volume:/var/lib/mysql \
    docker-practice:db
```

### `--mount`オプションによるマウント

```bash
docker container run                                                   \
    --name db                                                            \
    --rm                                                                 \
    --detach                                                             \
    --platform linux/amd64                                               \
    --env MYSQL_ROOT_PASSWORD=rootpassword                               \
    --env MYSQL_USER=hoge                                                \
    --env MYSQL_PASSWORD=password                                        \
    --env MYSQL_DATABASE=event                                           \
    --mount type=volume,src=docker-practice-db-volume,dst=/var/lib/mysql \
    docker-practice:db
```

`volume inspecr`

### バインドマウント

バインドマウントは**ホストマシンの任意のディレクトリをコンテナにマウントする**仕組み

```bash
docker container run          \
    --name app                  \
    --rm                        \
    --detach                    \
    --interactive               \
    --tty                       \
    --volume $(pwd)/src:/src    \
    docker-practice:app         \
    php -S 0.0.0.0:8000 -t /src
```

```bash
docker container run                        \
    --name app                                \
    --rm                                      \
    --detach                                  \
    --interactive                             \
    --tty                                     \
    --mount type=bind,src=$(pwd)/src,dst=/src \
    docker-practice:app                       \
    php -S 0.0.0.0:8000 -t /src
```

### `COPY`の用途

- 設定ファイルなど、**コンテナによって変えない**かつ**滅多に変更しない**ものを配置する場合

- 本番デプロイ時のソースコードなど,**即起動できる配布物を作る**場合

### バインとマウントの用途

- 開発時のソースコードなど**ホストマシンで変更したいがコンテナに随時反映したい**ものがある場合

- 初期化クエリなど**イメージを配布する時点では用意できない**ものがある場合

### ボリュームの削除

```bash
docker volume rm \
    docker-practice-db-volume
```

### ネットワークを作成する

```bash
docker network create [option] name

docker network create \
    docker-practice-network 
```

```bash
docker container run                        \
    --name app                                \
    --rm                                      \
    --detach                                  \
    --mount type=bind,src=$(pwd)/src,dst=/src \
    --publish 18000:8000                      \
    --network docker-practice-network         \
    docker-practice:app                       \
    php -S 0.0.0.0:8000 -t /src
```

`docker network ls`

```bash
docker container run                                                                       \
    --name db                                                                                \
    --rm                                                                                     \
    --detach                                                                                 \
    --platform linux/amd64                                                                   \
    --env MYSQL_ROOT_PASSWORD=rootpassword                                                   \
    --env MYSQL_USER=hoge                                                                    \
    --env MYSQL_PASSWORD=password                                                            \
    --env MYSQL_DATABASE=event                                                               \
    --mount type=volume,src=docker-practice-db-volume,dst=/var/lib/mysql                     \
    --mount type=bind,src=$(pwd)/docker/db/init.sql,dst=/docker-entrypoint-initdb.d/init.sql \
    --network docker-practice-network                                                        \
    --network-alias db                                                                       \
    docker-practice:db

```

```bash
docker container run                \
    --name mail                       \
    --rm                              \
    --detach                          \
    --platform linux/amd64            \
    --publish 18025:8025              \
    --network docker-practice-network \
    --network-alias mail              \
    mailhog/mailhog:v1.0.1
```
## `--network-alias`オプションで　hostを設定できる

- コンテナ同士で通信したいときは**自分でネットワークを作る**
- **エリアス**を設定すると**ホスト名**で通信できる

```yml
version: '3.9'

services:
  app:
    container_name: docker-practice-app
    build:
      dockerfile: docker/app/Dockerfile
      context: .
    ports:
      - '18000:8000'
    volumes:
      - type: bind
        source: ./src
        target: /src
    command: php -S 0.0.0.0:8000 -t /src

  db:
    container_name: docker-practice-db
    build:
      dockerfile: docker/db/Dockerfile
      context: .
    volumes:
      - type: volume
        source: docker-practice-db-volume
        target: /var/lib/mysql
      - type: bind
        source: ./docker/db/init.sql
        target: /docker-entrypoint-initdb.d/init.sql
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_USER: hoge
      MYSQL_PASSWORD: password
      MYSQL_DATABASE: event

  mail:
    container_name: docker-practice-mail
    image: mailhog/mailhog:v1.0.1
    platform: linux/x86_64
    ports:
      - "18025:8025"

volumes:
  docker-practice-db-volume:
```


</details>
