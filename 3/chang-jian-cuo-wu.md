# 常見錯誤

## 1. 使用MySQL資料庫，出現500 Internal Server Error

類似錯誤訊息如下：

* populate\(\) isn't reentrant
* MySQLdb.\_exceptions.OperationalError: \(2059, NULL\)

### 解決辦法：

由於django目前還不支持mysql8.0的caching\_sha2\_password加密方式，因此需修改為mysql\_native\_password加密方法

打開mysql指令視窗，輸入指令

```text
ALTER USER '<帳號>'@'localhost' IDENTIFIED BY '<帳號>' PASSWORD EXPIRE NEVER;
```

更新密碼

```text
ALTER USER '<帳號>'@'localhost' IDENTIFIED WITH mysql_native_password BY '<密碼>';
```

修改後重啟服務即可

