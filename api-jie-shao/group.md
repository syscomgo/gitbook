# Group

## General search

Query organization information that meets specific conditions

* Method：POST
* URL：/rest/accounts/api/group/list/
* postbody：

{% hint style="info" %}
All API must obtain a security code (security) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method.
{% endhint %}

```
{
    "security" : "<security_code>",
    "omflow_restapi" : 1,
    "org_name" : [],
    "org_no" : []
}
```

* secuity：Required
* omflow\_restapi：Required, Fill in 1
* org\_no：Fill in Organization No (Just choose one between org\_no, org\_name)
* org\_name：Fill in Organization Name (Just choose one between org\_no, org\_name)

{% hint style="info" %}
If both the Organization No and Organization Name are left blank, all organizations will be returned.
{% endhint %}

API Response example：

```
{
    "status": 200,
    "message": "查詢成功。",
    "result": [
        {
            "id": <org_id>,
            "group_no": <org_no>,
            "display_name": <org_name>,
            "parent_group_id": <parent_org_id>,
            "description": <description>
        },...
    ]
}
```
