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

```
curl -i --user <user>:<pwd> http://<server_ip>:<port>/accounts/api/security/get/
```

```
import requests

url = 'http://<server_ip>:<port>/accounts/api/security/get/'
user = '<user>'
pwd = '<pwd>'
response = requests.post( url, auth=( user, pwd ))
```

After verification, the following two responses will appear:

```
{    
    "status": 200,
    "message": "Success.",
    "result": {
        "security": "<security>"
        }
}
```

```
{
    "status": "404",
    "message": "User does not exist or is not enabled."
}
```
