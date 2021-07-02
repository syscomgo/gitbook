---
description: APIを使用してタスクリストをクエリします。
---

# 私の任務

## クエリ

* Method：POST
* URL：/rest/my-mission/api/my-mission/list/
* 引数入力\(postbody\)：以下形式の例。

{% hint style="info" %}
セセキュリティコード（security）を使用する前に、全apiを取得する必要があります。取得方法については、[セキュリティコード](https://doc.omflow.com.tw/v/japan/api-jie-shao/an-quan-ma)の取得を参照してください。
{% endhint %}

```text
{
	"security" : "<セセキュリティコード>",
	"omflow_restapi" : 1,
	"search_columns" : [],
	"search_conditions" : [],
	"exclude_conditions" : [],
	"order_columns" : [],
	"limit" : 100,
	"start" : 0
}
```

* secuity：必要，セキュリティコード。
* omflow\_restapi：必要，1。
* search\_columns：オプション，照会するフィールドの名前。以下形式の例。

  ```text
  "search_columns" : ["id", "status", "level"]
  ```

{% hint style="info" %}
search\_columnsが入力されていない場合、クエリフォームの全フィールド名とフィールド値が返されます。
{% endhint %}

* search\_conditions：search\_conditions：オプションで、条件を満たすデータを除外します。 配列内の各条件はJSONオブジェクト構造であり、各条件はAND関係です。デフォルトでは、全データをクエリします。
  * column：列名。[返されたデータ](https://doc.omflow.com.tw/v/japan/api-jie-shao/wo-de-ren-wu#hui-chuan-zi-liao)の例を参照できます。カスタムフォームの場合は、[クリエートAPI](https://doc.omflow.com.tw/v/japan/api-jie-shao/kuai-su-kai-chan-tui-chan#kai-chan)のid値を参照してください。
  * 条件：条件文字。以下5つのタイプに分類されます。
    * =：値とまったく同じようにデータを除外します。
    * &gt;：値より大きいデータを除外します。
    * &lt;：値より小さいデータを除外します。
    * in：値の配列と同じデータをフィルターで除外します。
    * contains：値を含むデータを除外します。
  * value：フィールド値。[アプリケーション管理&gt;アプリケーションデザイン&gt;フォームデザイン](https://doc.omflow.com.tw/v/japan/5/6#xin-jian-bian-ji-liu-cheng-ye-mian-biao-chan-she-ji)に従って対応する値を入力します。

```text
"search_conditions" :
[
    {
        "column" : "status",
        "condition" : "in",
        "value" : ["アサイン", "審查中"]
    },
    {
        "column" : "id",
        "condition" : ">",
        "value" : 3
    },
    <其の他条件>,...
]
```

* exclude\_conditions：オプションで、条件を満たすデータを除外します。形式はsearch\_conditionsと同じです。デフォルトでは、条件を除外しません。
* order\_columns：オプションで、指定したフィールドに従ってソートします。 逆順に並べ替える必要がある場合は、フィールド名の前に「-」記号を追加してください。デフォルトでは\["id"\]で並べ替えられます。 以下は形式の例。

  ```text
  #ソート
  "order_columns" : ["id"]

  #逆ソート
  "order_columns" : ["-id"]
  ```

* limit：オプション、数値を入力してデータ数を取得します。デフォルトは100です。
* start：オプションで、取得する最初のデータから数を入力します。デフォルトは0番目です。

{% hint style="info" %}
例1：start=0，limit=100，100データを返す。

例2：start=1，limit=100，990データを返す。

例3：start=100，limit=100，0データを返す。
{% endhint %}

## データ返す

成功した場合、以下は返されるデータの例。

```text
{
    "status": 200,
    "message": "クエリ成功。",
    "result": [
        {
            "id": 6,
            "flow_uuid": "67d4cf9a-49cd-4341-90da-b899eb0219b1",
            "flow_name": "問題管理",
            "status": "アサイン",
            "level": "",
            "title": "123",
            "data_no": 1,
            "data_id": 4,
            "history": false,
            "stop_uuid": "FITEM_7",
            "stop_chart_text": "アサイン",
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

失敗した場合、以下は返されるデータの例。

```text
{
    "status": 404,
    "message": "クエリ失敗，エラー：<エラーメッセージ>",
    "result": []

```

