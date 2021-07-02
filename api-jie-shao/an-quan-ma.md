---
description: >-
  すべてのAPI呼び出しには、セキュリティコード認証のためのパラメーター「セキュリティ」が必要なので、最初にセキュリティコードを取得するには、このAPIを呼び出す必要があります。
---

# セキュリティコード

* Method：POST
* URL：/accounts/api/security/get/
* Basic Authentication：True

{% hint style="info" %}
5分間使用しないと暗証番号は無効になり、暗証番号を再取得する必要があります。
{% endhint %}

このAPIは、基本的な認証方法を使用してユーザーの身元を確認します。以下、curlとpythonの例を示します。

```text
curl -i --user <user>:<pwd> http://<server_ip>:<port>/accounts/api/security/get/
```

```text
import requests

url = 'http://<server_ip>:<port>/accounts/api/security/get/'
user = '<user>'
pwd = '<pwd>'
response = requests.post( url, auth=( user, pwd ))
```

確認後、以下の2つの応答が表示されます。

```text
{    
    "status": 200,
    "message": "取得成功",
    "result": {
        "security": "<安全碼>"
        }
}
```

```text
{
    "status": "404",
    "message": "使用者不存在或未啟用。"
}
```

