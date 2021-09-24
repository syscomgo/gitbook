---
description: ログアウトしたユーザーのレコードを追加および削除します
---

# 記録を残す

## 追加

ユーザーの記録を追加します。

* Method：POST
* URL：/rest/api/leave-records/add/
* 入力パラメータ\(postbody\)：フォーマット例は以下のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security ）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"start" : <開始時間、必須>,
	"end" : <終了時間、必須>,
	"principal" : "<休暇を申請する、必須、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>",
	"substitute" : "<エージェント、必須、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>",
	"identifier" : "<識別子、オプション、他のシステムの休暇フォームとのインターフェースに使用されます。>"
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "正常に追加されました。",
    "result": <リクエストレコードIDを残す>
}
```

## リスト

リストユーザーの記録を残します。

* Method：POST
* URL：/rest/api/leave-records/list/
* 入力パラメータ\(postbody\)：フォーマット例は以下のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"cancel" : <キャンセルデータかどうか>、＃0または1を入力してください。入力しないと、すべて取得されます。
	"history" : <履歴データかどうか>、＃すべて入力しない場合は0または1を入力してください
	"principal" : "<休暇を申請する、必須、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>",
	"substitute" : "<エージェント、必須、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>"
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "クエリは成功しました。",
    "result": {
        "now_time" : <システムの現在時刻>
        "leave_list" : [{
            "principal_id" : <休暇をリクエストする人のID>
            "principal_id__nick_name" : <偽物を要求している人のニックネーム>
            "substitute_id" : <エージェントID>
            "substitute_id__nick_name" : <エージェントのニックネーム>
            "starttime" : <開始時間>
            "endtime" : <終了時間>
            "cancel" : <キャンセルデータかどうか>
            "identifier" : <識別子コード>
        },...]
    }
}
```

## 更新

ユーザーの休暇エージェントを更新します。

* Method：POST
* URL：/rest/api/leave-records/update/
* 入力パラメータ\(postbody\)：フォーマット例は以下のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"leave_id" : <リクエストレコードIDを残し、2つのうち1つを選択して識別コードを入力>,
	"identifier" : <識別子、2つのうちの1つを選択して、休暇レコードIDを入力します>,
	"substitute" : "<エージェント、必須、ユーザーアカウント、ニックネーム、メンバーコードを入力できます>"
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "正常に更新されました。",
    "result": None
}
```

## ログアウト

ユーザーの休暇記録をキャンセルします。

* Method：POST
* URL：/rest/api/leave-records/cancel/
* 入力パラメータ\(postbody\)：フォーマット例は以下のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"leave_id" : <リクエストレコードIDを残し、2つのうち1つを選択して識別コードを入力>,
	"identifier" : <識別コード、入力するものを選択するためにリクエストレコードIDを残します>
}
```

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "ログアウトに成功しました。",
    "result": None
}
```

## 削除

ユーザーの休暇記録を削除します。

* Method：POST
* URL：/rest/api/leave-records/delete/
* 入力パラメータ\(postbody\)：フォーマット例は以下のとおりです。

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"leave_id" : <リクエストレコードIDを残し、2つのうち1つを選択して識別コードを入力>,
	"identifier" : <識別コード、入力するものを選択するためにリクエストレコードIDを残します>
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



