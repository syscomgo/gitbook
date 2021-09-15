---
description: this is translated by machine
---

# Security

* Method：GET
* URL：/accounts/api/security/get/
* Basic Authentication：True

{% hint style="info" %}
The security code becomes invalid after not used for 5 minutes, and the security code needs to be obtained again.
{% endhint %}

This API uses **basic authentication** methods to verify user identity. The following are examples of curl and python:

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

After verification, the following two responses will appear:

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

