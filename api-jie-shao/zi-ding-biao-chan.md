---
description: this is translated by machine
---

# Query Form

## Query

{% hint style="info" %}
All apis must obtain a security code \(security\) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method
{% endhint %}

* Method：POST
* URL：/rest/flowmanage/api/omdata/list/**&lt;api path&gt;**
* Input parameters \(postbody\): The example format is as follows.

{% hint style="info" %}
Please refer to the [flow design](../5/6.md#xin-jian-bian-ji-liu-cheng-ye-mian-can-shu-she-ding) for the api path
{% endhint %}

```text
{
	"security" : "<security>",
	"omflow_restapi" : 1,
	"search_conditions" : [],
	"search_columns" : [],
	"exclude_conditions" : [],
	"order_column" : [],
	"limit" : 100,
	"start" : 0
}
```

{% hint style="info" %}
Please refer to [**API&gt;My Mission**](../5/2.md) for details of other parameters
{% endhint %}

When successful, an example of the returned data is as follows:

```text
{
    "status": 200,
    "message": "查詢成功。",
    "result": [
        {
            "id": 3,
            "flow_uuid": "1c192a11-842a-4439-8bd2-b4e0c1226c97",
            "dataid_header": "",
            "data_no": 2,
            "history": true,
            "status": "新建",
            "title": "1",
            "level": "yellow",
            "group": "",
            "closed": false,
            "stop_uuid": "FITEM_15-FITEM_2",
            "stop_chart_type": null,
            "stop_chart_text": "標準變更分類與狀態",
            "running": false,
            "error": false,
            "createtime": "2020-07-15T15:44:06.670",
            "updatetime": "2020-07-15T15:44:06.672",
            "stoptime": "2020-07-15T15:44:06.977",
            "create_user_id": "kai",
            "update_user_id": "kai",
            "data_param": "",
            "error_message": null,
            "init_data_id": 3,
            "is_child": false,
            "formitm_1": null,
            "formitm_2": null,
            "formitm_3": ""
        },...<以此類推>
    ]
}
```

When it fails, the example of returned data is as follows:

```text
{
    "status": 404,
    "message": "查詢失敗，錯誤訊息如下：<錯誤訊息>",
    "result": []
}
```

