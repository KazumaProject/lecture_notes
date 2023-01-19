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