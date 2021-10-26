# よくある間違い

## 1. MySQLデータベースを使用すると、500 Internal Server Errorというエラーメッセージが表示される

同様のエラーメッセージは次のとおりです。

* populate() isn't reentrant
* MySQLdb.\_exceptions.OperationalError: (2059, NULL)

### 解決方法：

Djangoは現在mysql8.0のcache\_sha2\_password暗号化方式をサポートしていないため、mysql\_native\_password暗号化方式に変更する必要があります

mysqlコマンドウィンドウを開き、コマンドを入力します

```
ALTER USER '<アカウント>'@'localhost' IDENTIFIED BY '<アカウント>' PASSWORD EXPIRE NEVER;
```

パスワードを更新します

```
ALTER USER '<アカウント>'@'localhost' IDENTIFIED WITH mysql_native_password BY '<パスワード>';
```

変更後にサービスを再起動します
