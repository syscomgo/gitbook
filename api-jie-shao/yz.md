# ユーザー

## 一般的な検索

特定の条件を満たすユーザーデータをクエリする

* Method：POST
* URL：/rest/accounts/api/user/list/
* 入力パラメータ(postbody)：フォーマット例は以下のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード\（security \）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```
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

*   search\_columns：オプション、**列名**を照会します。フォーマット例は以下のとおりです。

    ```
    "search_columns" : ["id", "username", "nick_name"]
    ```

{% hint style="info" %}
search  \_columnsが入力されていない場合、クエリフォームのすべての**フィールド名とフィールド値**が返されます。
{% endhint %}

* search  \_conditions：オプションで、条件を満たすデータを除外します。配列内の各条件はJSONオブジェクト構造であり、各条件はAND関係です。デフォルトでは、すべてのデータがクエリされます。
  * column：列名。\[_**データの例を返す**_を参照してください。
  * condition：条件文字。次の5つのタイプに分けられます。
    * \=：値とまったく同じデータを除外します。
    * \>：値より大きいデータを除外します。
    * <：値未満のデータを除外します。
    * in：値の配列と同じデータを除外します。
    * contains：値を含むデータを除外します。
  * value：フィールド値、 _ **個人管理＆gt;ユーザー管理＆gt;ユーザーデータ** _ によるそして対応する値を入力します。

```
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
    <その他の条件>,...
]
```

* exclude  \_conditions：オプションで、条件を満たすデータを除外します。形式はsearch  \_conditionsと同じであり、デフォルトでは条件を除外しません。
*   order  \_columns：オプション、指定された列に従って並べ替えます。逆に並べ替える必要がある場合は、フィールド名の前に「-」記号を追加してください。デフォルトでは、 \["id" ]で並べ替えます。形式の例は次のとおりです。

    ```
    #ASC
    "order_columns" : ["id"]

    #DESC
    "order_columns" : ["-id"]
    ```
* limit：オプションで、データの数を取得するために数を入力します。デフォルトは100です。
* start：オプションで、取得するデータの数から数を入力します。デフォルトは0番目です。

{% hint style="info" %}
例1：start=0，limit=100，100個のデータを返します。

例2：start=1，limit=100，99個のデータを返します。

例3：start=100，limit=100，0個のデータを返します。
{% endhint %}

## 一般的なクエリの戻り形式

APIの戻り例は次のとおりです。

```
{
    "status": 200,
    "message": "クエリは成功しました。",
    "result": [
        {
            "id": <ユーザーID>,
            "password": <暗号化されたパスワード>,
            "last_login": <最終ログイン時間>,
            "is_superuser": <マネージャーです>,
            "username": <アカウント>,
            "first_name": <名前>,
            "last_name": <姓>,
            "is_active": <有効にするかどうか>,
            "email": <メール>,
            "nick_name": <表示名>,
            "birthday": <誕生日>,
            "gender": <性別>,
            "phone1": <電話>,
            "phone2": <phone>,
            "extension_no": <extension>,
            "company": <会社名>,
            "ad_flag": <広告を統合するかどうか>,
            "ad_sid": <広告番号>,
            "frequency": <フロントエンドの更新頻度>,
            "updatetime": <更新時間>,
            "delete": <削除するかどうか>,
            "default_group": <デフォルトの組織>,
            "ad_no": <従業員番号>
        },...
    ]
}
```

## 組織検索

「**組織コード**」を使用して、これらの組織のユーザーを検索します。

* Method：POST
* URL：/rest/accounts/api/user/list-by-group/
* 入力パラメータ(postbody)：フォーマット例は以下のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security ）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"org_no"：[]、
  "org_name"：[]
}
```

* secuity：必須、セキュリティコード。
* omflow\_restapi：必須，1。
* org  \_no：オプション、組織コード、複数の組織コードを配列に配置できます。 \（組織名から1つ選択してください\）
* org  \_name：オプション、組織名、複数の組織コードを配列に配置できます。 \（組織コードから1つ選択してください\）

APIの戻り例は次のとおりです。

```
{
    "status": 200,
    "message": "正常に読み取りました。",
    "result": {
        "<組織コード>": [
            {
                "user": <ユーザーID>, #これはomflowデータベースで使用される番号です。
                "user__nick_name": <ユーザー表示名>,
                "user__username": <ユーザーアカウント>,
                "user__ad_no": <ユーザー従業員番号>
            },...
        ],
        "<組織コード>": [
            {
                "user": <ユーザーID>, #これはomflowデータベースで使用される番号です。
                "user__nick_name": <ユーザー表示名>,
                "user__username": <ユーザーアカウント>,
                "user__ad_no": <ユーザー従業員番号>>
            },...
        ],
    }
}
```
