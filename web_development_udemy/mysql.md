## SQL Basic Commands
- SQLの起動と停止
```zsh
mysql.server start
mysql.server stop
```

- ログイン
```zsh
sudo mysql -u root
```

- 設定を見る
```sql
show variables like '%char%';
```

- データベースを表示
```sql
show databases;
```

- データベースの作成,削除
```sql
create database <database_name>;
drop database <database_name>;
```

- 選択されているデータベースの表示と選択
```sql
select database();
use <database_name>;
```

- ユーザーの作成,削除
```sql
create user <user_name@localhost> identified 'password';
create user dbuser01@localhost identified 'password_for_dbuser01';

drop user dbuser01@localhost;
```

- ユーザーに権限を与える
```sql
grant all on <database_name>.* to <user_name>@localhost;
grant all on db01.* to dbuser01@localhost;
```

- sqlファイルを実行する
```zsh
sudo mysql -u root < initilize.sql
```

```sql
drop database if exists mydb;
create database mydb;
grant all on mydb.* to mydbuser@localhost identified by '1111';
```

## 参考にした記事
- [MacbookにRubyをインストール](https://qiita.com/yamato1491038/items/ae95114b9f25c4a10cf0)

- [Macでmysqlを扱う方法](https://qiita.com/fuwamaki/items/194c2a82bd6865f26045)
