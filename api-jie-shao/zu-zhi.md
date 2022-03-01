# 組織

## 一般搜尋

查詢符合特定條件的組織資料

* Method：POST
* URL：/rest/accounts/api/group/list/
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

```
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"org_name" : [],
	"org_no" : []
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。
* org\_no：選填，組織代號，陣列內可放置多個組織代號。(與組織名稱二擇一)
* org\_name：選填，組織名稱，陣列內可放置多個組織名稱。(與組織代號二擇一)

{% hint style="info" %}
**如果組織代號與組織名稱都留空時，則回傳全部的組織。**
{% endhint %}

API回傳範例如下：

```
{
    "status": 200,
    "message": "查詢成功。",
    "result": [
        {
            "id": <組織編號>,
            "group_no": <組織代號>,
            "display_name": <組織名稱>,
            "parent_group_id": <父組織編號>,
            "description": <組織說明>
        },...
    ]
}
```
