---
description: 使用API查詢我的任務清單。
---

# 我的任務

## 查詢

* Method：POST
* URL：/rest/my-mission/api/my-mission/list/
* 輸入參數\(postbody\)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼\(security\)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

```text
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"search_columns" : [],
	"search_conditions" : [],
	"exclude_conditions" : [],
	"order_columns" : [],
	"limit" : 100,
	"start" : 0
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。
* search\_columns：選填，要查詢的**欄位名稱**。格式範例如下。

  ```text
  "search_columns" : ["id", "status", "level"]
  ```

{% hint style="info" %}
若未填 search\_columns ，會回傳查詢表單所有**欄位名稱、欄位值**。
{% endhint %}

* search\_conditions：選填，篩選出符合條件的資料。陣列中每個條件為JSON物件結構，每個條件之間為AND關係，預設為查詢所有資料。
  * column：欄位名稱，可參考[_**回傳資料範例**_](wo-de-ren-wu.md#hui-chuan-zi-liao)，若為**自訂表單**可參考[_開單API_](kuai-su-kai-chan-tui-chan.md#kai-chan)中的id值。
  * condition：條件字元，分為下列五種。
    * =：篩選出與value完全相同的資料。
    * &gt;：篩選出大於value的資料。
    * &lt;：篩選出小於value的資料。
    * in：篩選出與value陣列中相同的資料。
    * contains：篩選出包含value的資料。
  * value：欄位值，依照 [_**應用管理 &gt; 應用設計 &gt; 表單設計**_](../5/6.md#xin-jian-bian-ji-liu-cheng-ye-mian-biao-chan-she-ji) 而填入對應值。

```text
"search_conditions" :
[
    {
        "column" : "status",
        "condition" : "in",
        "value" : ["指派", "審核中"]
    },
    {
        "column" : "id",
        "condition" : ">",
        "value" : 3
    },
    <其他條件>,...
]
```

* exclude\_conditions：選填，排除掉符合條件的資料，格式與search\_conditions相同，預設為不排除任何條件。
* order\_columns：選填，依照指定欄位進行排序。需要逆向排序請在欄位名稱前方加上"-"號，預設為以 \["id"\] 進行排序。範例格式如下。

  ```text
  #正排序
  "order_columns" : ["id"]

  #逆排序
  "order_columns" : ["-id"]
  ```

* limit：選填，填入數字取得至第幾筆資料，預設為100筆。
* start：選填，填入數字從第幾筆資料開始取得，預設為第 0 筆。

{% hint style="info" %}
例1：start=0，limit=100，回傳100筆資料。

例2：start=1，limit=100，回傳99筆資料。

例3：start=100，limit=100，回傳0筆資料。
{% endhint %}

## 回傳資料

成功時，回傳資料範例如下所示：

```text
{
    "status": 200,
    "message": "查詢成功。",
    "result": [
        {
            "id": 6,
            "flow_uuid": "67d4cf9a-49cd-4341-90da-b899eb0219b1",
            "flow_name": "問題管理",
            "status": "指派",
            "level": "",
            "title": "123",
            "data_no": 1,
            "data_id": 4,
            "history": false,
            "stop_uuid": "FITEM_7",
            "stop_chart_text": "指派人工",
            "create_user_id": "system",
            "update_user_id": null,
            "ticket_createtime": "2020-07-07T13:50:21.494",
            "createtime": "2020-07-07T13:50:21.589",
            "updatetime": "2020-07-07T13:50:21.589",
            "assignee_id": null,
            "assign_group_id": 1,
            "action": ",",
            "attachment": false,
            "closed": false
        },.....
    ]
}
```

失敗時，回傳資料範例如下：

```text
{
    "status": 404,
    "message": "查詢失敗，錯誤訊息如下：<錯誤訊息>",
    "result": []

```

