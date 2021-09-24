---
description: リストされているすべてのカスタムフォームは、このAPIを使用して関連情報をクエリできます。
---

# フォーム検索

## 検索

{% hint style="info" %}
すべてのAPIは、使用前にセキュリティコード（セキュリティ）とともに取得する必要があります。取得方法については、[コード](https://app.gitbook.com/@omflow-syscom/s/omflow-doc/v/japan/api-jie-shao/an-quan-ma)の取得を参照してください。
{% endhint %}

* Method：POST
* URL：/rest/flowmanage/api/omdata/list/&lt;api路徑&gt;
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

{% hint style="info" %}
API Path の[フロー設計](https://app.gitbook.com/@omflow-syscom/s/omflow-doc/v/japan/5/6#xin-jian-bian-ji-liu-cheng-ye-mian-can-shu-she-ding)を参照してください。
{% endhint %}

```text
{
	"security" : "<セキュリティコード>",
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
パラメータの詳細については、[APIの紹介 &gt; 私のタスク ](https://app.gitbook.com/@omflow-syscom/s/omflow-doc/v/japan/api-jie-shao/wo-de-ren-wu)を参照してください。
{% endhint %}

成功した場合、返されるデータの例は以下のとおりです。

```text
{
    "status": 200,
    "message": "検索に成功。",
    "result": [
        {
            "id": 3,
            "flow_uuid": "1c192a11-842a-4439-8bd2-b4e0c1226c97",
            "dataid_header": "",
            "data_no": 2,
            "history": true,
            "status": "新しい",
            "title": "1",
            "level": "yellow",
            "group": "",
            "closed": false,
            "stop_uuid": "FITEM_15-FITEM_2",
            "stop_chart_type": null,
            "stop_chart_text": "標準の変更の分類とステータス",
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
        },...<等々>
    ]
}
```

失敗した場合、返されるデータの例は以下のとおりです。

```text
{
    "status": 404,
    "message": "クエリが失敗しました。エラーメッセージは次のとおりです：<エラーメッセージ>",
    "result": []
}
```

