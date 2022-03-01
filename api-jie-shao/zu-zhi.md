# 組織

## 一般的な検索

特定の条件を満たす組織情報を照会する

* Method：POST
* URL：/rest/accounts/api/group/list/
* 入力パラメータ(postbody)：形式の例は次のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security ）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"org_name" : [],
	"org_no" : []
}
```

* secuity：必須のセキュリティコード。
* omflow\_restapi：必須，1。
* org\_no：オプション、組織コード、複数の組織コードを配列に配置できます。 （組織名から1つ選択してください）
* org\_name：オプション、組織名、複数の組織コードを配列に配置できます。 （組織コードから1つ選択してください）

{% hint style="info" %}
**組織コードと組織名の両方を空白のままにすると、すべての組織が返されます。 \*\***
{% endhint %}

APIの戻り例は次のとおりです：

```
{
    "status": 200,
    "message": "クエリは成功しました。",
    "result": [
        {
            "id": <組織番号>,
            "group_no": <組織コード>,
            "display_name": <組織名>,
            "parent_group_id": <親組織番号>,
            "description": <組織の説明>
        },...
    ]
}
```
