# よくある間違う

## 1. MySQLデータベースを使用すると、500 Internal Server Error

同様のエラーメッセージは次のとおりです。

* populate\(\) isn't reentrant
* MySQLdb.\_exceptions.OperationalError: \(2059, NULL\)

### 解決：

Djangoは現在mysql8.0のcache\_sha2\_password暗号化方式をサポートしていないため、mysql\_native\_password暗号化方式に変更する必要があります

mysqlコマンドウィンドウを開き、コマンドを入力します

```text
ALTER USER '<アカウント>'@'localhost' IDENTIFIED BY '<アカウント>' PASSWORD EXPIRE NEVER;
```

パスワードを更新する

```text
ALTER USER '<アカウント>'@'localhost' IDENTIFIED WITH mysql_native_password BY '<パスワード>';
```

変更後にサービスを再起動します

