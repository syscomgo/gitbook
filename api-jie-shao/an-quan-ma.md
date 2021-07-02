---
description: 所有API呼叫皆需要附帶參數「security」進行安全碼認證，因此需先呼叫此API取得安全碼。
---

# 安全碼

* Method：GET
* URL：/accounts/api/security/get/
* Basic Authentication：True

{% hint style="info" %}
安全碼在連續 5 分鐘未使用後失效，需重新取得安全碼。
{% endhint %}

此API採用**基礎認證**方式驗證使用者身分，以下為curl及python範例：

```text
curl -i --user <user>:<pwd> http://<server_ip>:<port>/accounts/api/security/get/
```

```text
import requests

url = 'http://<server_ip>:<port>/accounts/api/security/get/'
user = '<user>'
pwd = '<pwd>'
response = requests.get( url, auth=( user, pwd ))
print(response.text)
```

在驗證後會出現以下兩種回覆：

```text
{    
    "status": 200,
    "message": "取得成功。",
    "result": {
        "security": "<安全碼>"
        }
}
```

```text
{
    "status": "500",
    "message": "使用者不存在。"
}

{
    "status": "404",
    "message": "使用者未啟用。"
}

{
    "status": "404",
    "message": "登入失敗。"
}
```

