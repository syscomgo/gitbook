---
description: ログオフしたユーザーの休暇記録を追加および削除します
---

# 休暇記録

## 追加

ユーザーの休暇記録を追加します。

* Method：POST
* URL：/rest/api/leave-records/add/
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"start" : <開始時間、必須>,
	"end" : <終了時間、必須>,
	"principal" : "<必要に応じて、ユーザーアカウント、ニックネーム、メンバーコードを入力できます。>",
	"substitute" : "<エージェントは、必須で、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>",
	"identifier" : "<オプションの識別コード。他のシステムの休暇フォームとのインターフェースに使用されます。>"
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "正常に追加されました。",
    "result": <レコードIDを残す>
}
```

## リスト

リストユーザーの記録を残します。

* Method：POST
* URL：/rest/api/leave-records/list/
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"cancel" : <キャンセルデータかどうか>, #0または1を入力してください。入力しない場合は、すべてが取得されます。
	"history" : <履歴データかどうか>, #0または1を入力してください。入力しない場合は、すべてが取得されます。
	"principal" : "<必要に応じて、ユーザーアカウント、ニックネーム、メンバーコードを入力できます。>",
	"substitute" : "<エージェントは、必須で、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>"
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "検索に成功しました。",
    "result": {
        "now_time" : <システムの現在時刻>
        "leave_list" : [{
            "principal_id" : <個人IDを残す>
            "principal_id__nick_name" : <偽のニックネームを尋ねる>
            "substitute_id" : <エージェントID>
            "substitute_id__nick_name" : <エージェントのニックネーム>
            "starttime" : <開始時間>
            "endtime" : <終了時間>
            "cancel" : <キャンセルデータかどうか>
            "identifier" : <識別子>
        },...]
    }
}
```

## 更新

ユーザーの休暇エージェントを更新します。

* Method：POST
* URL：/rest/api/leave-records/update/
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"leave_id" : <レコードIDを残し、2つのうちの1つを選択して、識別コードを入力します>,
	"identifier" : <識別コード、2つのうちの1つを選択して、休暇記録IDを入力します>,
	"substitute" : "<エージェントは、必須で、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>"
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "更新が完了しました。",
    "result": None
}
```

## ログアウト

ユーザーの休暇記録をキャンセルします。

* Method：POST
* URL：/rest/api/leave-records/cancel/
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"leave_id" : <レコードIDを残し、2つのうちの1つを選択して、識別コードを入力します>,
	"identifier" : <識別コード、2つのうちの1つを選択して、休暇記録IDを入力します>
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "ログアウトに成功。",
    "result": None
}
```

## 削除

ユーザーの休暇記録を削除します。

* Method：POST
* URL：/rest/api/leave-records/delete/
* 入力パラメータ\(postbody\)：形式の例は次のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"leave_id" : <レコードIDを残し、2つのうちの1つを選択して、識別コードを入力します>,
	"identifier" : <識別コード、2つのうちの1つを選択して、休暇記録IDを入力します>
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "正常に削除されました。",
    "result": None
}
```

