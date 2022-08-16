---
description: 所有已上架的自訂表單皆可使用此API查詢相關資料。
---

# 查詢表單

## 查詢

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

* Method：POST
* URL：/rest/flowmanage/api/omdata/list/\<api路徑>
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
api路徑請參閱[流程設計](../5/6.md#xin-jian-bian-ji-liu-cheng-ye-mian-can-shu-she-ding)。
{% endhint %}

```python
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"search_conditions" : [],
	"search_columns" : [],
	"exclude_conditions" : [],
	"order_columns" : [],
	"limit" : 100,
	"start" : 0
}
```

{% hint style="info" %}
參數詳細介紹請參閱[**API介紹>我的任務**](wo-de-ren-wu.md#cha-xun)。
{% endhint %}

成功時，回傳資料範例如下所示：

```python
{
    "status": 200,
    "message": "查詢成功。",
    "result": [
        {
            "id": 3,                    #又稱data_id，推單時必要參數
            "flow_uuid": "1c192a11-842a-4439-8bd2-b4e0c1226c97",
            "dataid_header": "",
            "data_no": 2,               #單號
            "history": true,            #是否為歷史資料
            "status": "新建",
            "title": "1",
            "level": "yellow",py
            "group": "",
            "closed": false,            #是否關單
            "stop_uuid": "FITEM_15-FITEM_2",
            "stop_chart_type": null,
            "stop_chart_text": "標準變更分類與狀態",
            "running": false,           #是否處於執行狀態
            "error": false,             #是否處於異常狀態
            "createtime": "2020-07-15T15:44:06.670",
            "updatetime": "2020-07-15T15:44:06.672",
            "stoptime": "2020-07-15T15:44:06.977",
            "create_user_id": "kai",
            "update_user_id": "kai",
            "data_param": "",
            "error_message": null,
            "init_data_id": 3,
            "is_child": false,          #是否為子單
            "formitm_1": null,
            "formitm_2": null,
            "formitm_3": ""
        },...<以此類推>
    ]
}
```

失敗時，回傳資料範例如下：

```python
{
    "status": 404,
    "message": "查詢失敗，錯誤訊息如下：<錯誤訊息>",
    "result": []
}
```
