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

- テーブルの作成、削除
```sql
create table users (id int unsigned, name varchar(32), age int);
drop table users;
```

## データ型
1. 数値型
	- int
	 整数 -2147483648 ~ 2147483647
	- tinyint 
	 -128 ~ 127
	- float
	- double

- int unsigned
正の値のみ

- tinyint(1)

2. 文字列
	- char
	固定長の文字列255文字まで
	 i.e. 商品コードで５桁固定
	- varchar, char(5)
	可変長も文字列255文字まで
	i.e. email, varchar(255)
	- text
	65535文字まで

3. 日付、時刻型
	- date
	- datetime
	- time

- データの挿入
```sql
insert into users(id, name, age) values (1, 'sato', '20')
```

- auto_increment
- not null
- PRIMARY KEY

```sql
create table users (id int unsigned auto_increment not null primary key, name varchar(32), age int not null);
```

```sql
create table users (id int unsigned auto_increment not null primary key,
    -> name varchar(32),
    -> age int not null default 1);
```

- 値の取得
```sql
select * from users;
select name from users;
select * from users where age >= 20
```

- 名前がsから始まる
```sql:
select * from users where name like 's%';
```

- aを含む
```sql:
 select * from users where name like '%a%';
```

- aでおわる
```sql:
 select * from users where name like '%a';
```

- 6文字
```sql:
select * from users where name like '______';
```

- 2文字目がa
```sql:
select * from users where name like '_a%';
```

- 並び替え
```sql
select * from users order by age asc;
select * from users order by age desc;
```

- 制限
```sql
select * from users limit 3;
select * from users order by age asc limit 3;
select * from users where age is not null  order by age asc limit 3;
select * from users where age is not null  order by age asc limit 3 offset 3;
```

- Update
```sql
update users set age = 40 where id = 1;
```

- Delete
```sql
delete from users where id =1 ;
```

## 参考にした記事
- [MacbookにRubyをインストール](https://qiita.com/yamato1491038/items/ae95114b9f25c4a10cf0)

- [Macでmysqlを扱う方法](https://qiita.com/fuwamaki/items/194c2a82bd6865f26045)
