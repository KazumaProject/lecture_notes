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

## 参考にした記事
- [MacbookにRubyをインストール](https://qiita.com/yamato1491038/items/ae95114b9f25c4a10cf0)

- [Macでmysqlを扱う方法](https://qiita.com/fuwamaki/items/194c2a82bd6865f26045)