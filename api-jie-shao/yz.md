# ユーザー

## 一般的な検索

特定の条件を満たすユーザーデータをクエリする

* Method：POST
* URL：/rest/accounts/api/user/list/
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
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

* search\_columns：オプションで、照会するフィールドの名前。 フォーマット例は以下のとおりです。

  ```text
  "search_columns" : ["id", "username", "nick_name"]
  ```

{% hint style="info" %}
search\_columnsが入力されていない場合、クエリフォームのすべてのフィールド名とフィールド値が返されます。
{% endhint %}

* search\_conditions：オプションで、条件を満たすデータを除外します。 配列内の各条件はJSONオブジェクト構造であり、各条件はAND関係です。デフォルトでは、すべてのデータをクエリします。
  * column：フィールド名、[**一般的な検索の戻り形式**](yz.md#nanori)を参照してください
  * condition：条件文字は以下の5種類に分けられます。
    * =：値とまったく同じようにデータを除外します。
    * &gt;：値より大きいデータを除外します。
    * &lt;：値よりも小さいデータを除外します。
    * in：値の配列と同じデータを除外します。
    * contains：値を含むデータを除外します。
  * value：フィールド値には、[**ユーザー**](../5/8.md#yz)に従って対応する値を入力します。

```text
"search_conditions" :
[
    {
        "column" : "username",
        "condition" : "in",
        "value" : ["admin", "user001"]
    },
    {
        "column" : "id",
        "condition" : ">",
        "value" : 3
    },
    <其他條件>,...
]
```

* exclude\_conditions：オプション。条件を満たすデータを除外します。形式はsearch\_conditionsと同じです。デフォルトでは、条件を除外しません。
* order\_columns：オプションで、指定されたフィールドに従ってソートします。 逆に並べ替える必要がある場合は、フィールド名の前に「-」記号を追加してください。デフォルトでは、\["id"\]で並べ替えます。 形式の例は次のとおりです。

  ```text
  #ASC
  "order_columns" : ["id"]

  #DESC
  "order_columns" : ["-id"]
  ```

* limit：オプションで、データの数を取得するために数値を入力します。デフォルトは100です。
* start：オプションで、取得するデータの数から数を入力します。デフォルトは0番目です。

{% hint style="info" %}
例1：start=0，limit=100，100個のデータを返します。

例2：start=1，limit=100，99個のデータを返します。

例3：start=100，limit=100，0個のデータを返します。
{% endhint %}

## 一般的な検索の戻り形式

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "検索に成功。",
    "result": [
        {
            "id": <ユーザーID>,
            "password": <暗号化されたパスワード>,
            "last_login": <最終ログイン時間>,
            "is_superuser": <それはマネージャーですか>,
            "username": <口座番号>,
            "first_name": <ファーストネーム>,
            "last_name": <苗字>,
            "is_active": <有効にするかどうか>,
            "email": <Eメール>,
            "nick_name": <表示名>,
            "birthday": <お誕生日>,
            "gender": <性別>,
            "phone1": <電話>,
            "phone2": <携帯電話>,
            "extension_no": <拡張>,
            "company": <会社名>,
            "ad_flag": <統合するかどうかad>,
            "ad_sid": <adナンバリング>,
            "frequency": <フロントエンドのリフレッシュレート>,
            "updatetime": <更新時間>,
            "delete": <削除するかどうか>,
            "default_group": <デフォルトの組織>,
            "ad_no": <従業員ID>
        },...
    ]
}
```

## 組織検索

組織コードを使用して、これらの組織の下のユーザーを検索します。

* Method：POST
* URL：/rest/accounts/api/user/list-by-group/
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"group_no" : []
}
```

* secuity：必須のセキュリティコード。
* omflow\_restapi：必須，1。
* group\_no：必須の組織コード、複数の組織コードを配列に配置できます。

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "正常に読み取る。",
    "result": {
        "<組織コード>": [
            {
                "user": <ユーザーID>, #これは、omflowデータベースで使用される番号です。
                "user__nick_name": <ユーザー表示名>,
                "user__username": <ユーザーアカウント>,
                "user__ad_no": <ユーザー従業員番号>
            },...
        ],
        "<組織コード>": [
            {
                "user": <ユーザーID>, #これは、omflowデータベースで使用される番号です。
                "user__nick_name": <ユーザー表示名>,
                "user__username": <ユーザーアカウント>,
                "user__ad_no": <ユーザー従業員番号>>
            },...
        ],
    }
}
```

