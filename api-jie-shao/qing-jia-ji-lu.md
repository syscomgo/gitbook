# Leave Record

## Add

Add leave records.

* Method：POST
* URL：/rest/api/leave-records/add/
* postbody:

{% hint style="info" %}
All apis must obtain a security code \(security\) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method.
{% endhint %}

```text
{
	"security" : "",
	"omflow_restapi" : 1,
	"start" : <start time, require>,
	"end" : <end time, require>,
	"principal" : "<require, Can fill in user username, nick_name, ad_no>",
	"substitute" : "<require, Can fill in username, nick_name, ad_no>",
	"identifier" : "<Used to interface with the leave form of other systems>"
}
```

API Response:

```text
{
    "status": 200,
    "message": "新增成功。",
    "result": <leave id>
}
```

## List

List leave records.

* Method：POST
* URL：/rest/api/leave-records/list/
* postbody:

```text
{
	"security" : "",
	"omflow_restapi" : 1,
	"cancel" : <cancel>, #0 or 1, if not fill in return all
	"history" : <history>, #0 or 1, if not fill in return all
	"principal" : "<require, Can fill in user username, nick_name, ad_no>",
	"substitute" : "<require, Can fill in user username, nick_name, ad_no>"
}
```

API Response:

```text
{
    "status": 200,
    "message": "查詢成功。",
    "result": {
        "now_time" : <system now time>
        "leave_list" : [{
            "principal_id" : ""
            "principal_id__nick_name" : ""
            "substitute_id" : ""
            "substitute_id__nick_name" : ""
            "starttime" : ""
            "endtime" : ""
            "cancel" : ""
            "identifier" : ""
        },...]
    }
}
```

## Update

Update leave records.

* Method：POST
* URL：/rest/api/leave-records/update/
* postbody:

```text
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"leave_id" : <choose one to fill in with the identifier>,
	"identifier" : <choose one to fill in with the leave_id>,
	"substitute" : "<require, Can fill in user username, nick_name, ad_no>"
}
```

API Response:

```text
{
    "status": 200,
    "message": "更新成功。",
    "result": None
}
```

## Cancel

Cancel leave records.

* Method：POST
* URL：/rest/api/leave-records/cancel/
* postbody:

```text
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"leave_id" : <choose one to fill in with the identifier>,
	"identifier" : <choose one to fill in with the leave_id>
}
```

API Response:

```text
{
    "status": 200,
    "message": "註銷成功。",
    "result": None
}
```

## Delete

Delete leave records.

* Method：POST
* URL：/rest/api/leave-records/delete/
* postbody:

```text
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"leave_id" : <choose one to fill in with the identifier>,
	"identifier" : <choose one to fill in with the leave_id>
}
```

API Response:

```text
{
    "status": 200,
    "message": "刪除成功。",
    "result": None
}
```

