---
description: 作成したフォームをリリース後、APIで直接起票したり、人的処理で滞留しているものを処理したり、関連するAPIでシステムで直接表示したりすることができます。
---

# クイック操作

## 簡易起票、簡易処理

### APIの取得

**メインメニュー>アプリケーション管理>リリース済みアプリケーション**にて、調べたいアプリケーションのプロセス一覧を表示します。

![](../.gitbook/assets/pic028.jpg)

調べたいプロセスの右側の設定ボタンをクリックします。

![](../.gitbook/assets/pic029.jpg)

クリックすると次の画面が表示されます。以下にタブの説明を1つずつ記載します。

![](<../.gitbook/assets/pic032 (1).jpg>)

* カラム設定：プロセスのフォームリストの表示列をカスタマイズします。
* 起票API：起票時に使用するAPI形式。
* クエリAPI：検索時に使用するAPI形式。
* 処理API：処理を進めるときに使用するAPI形式。

### 起票

クリックした後、\[起票API]タブを選択すると、次の図に示すように、該当APIの例が表示されます。

![](../.gitbook/assets/jie-tu-20200817-shang-wu-9.56.27.png)

{% hint style="info" %}
**セキュリティコードを\<security>に設定する必要があり、formdataの"<>"内容を変更する必要があります。**

formdataは少なくとも必須入力欄の内容を設定する必要があります。必須入力欄かどうかは、 **アプリケーション管理 >アプリケーション設計 > フォームフィールド設計**を参照して確認してください。
{% endhint %}

起票成功時、2種類の戻り情報があります。

一、プロセスの開始要素で 検証機能を使用していない場合， data\_noを起票番号として返します。

```
{
  "status": "200",
  "message": "起票成功",
  "result": "<data_no>"
}
```

二、検証機能を使用している場合、data\_noは返しません。

```
{
  "status": "200",
  "message": "起票成功",
  "result": ""
}
```

起票に失敗すると、次のように返します。

```
{
  "status": "404",
  "message": "起票失敗"
}
```

### ファイル添付

フォームのファイル添付機能が有効になっている場合は、起票時に下図のように同時にファイルをアップロードすることもできます。：

<figure><img src="https://3346898383-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M6SrengyyhO1h0_BsJ_%2F-MUptA-ihW68AxzlLLQ4%2F-MUq2eJqXIOtSxKMUGbb%2Fimage.png?alt=media&#x26;token=451b4efe-23aa-44fd-9fef-5ad3c434b7e3" alt=""><figcaption></figcaption></figure>

Pythonでの例は以下の通り：

```
import requests,json

url = '<起票APIのURL >'
formdata = [{"id": "FORMITM_2","value": "<入力値>"}]
values={
  "security": "<sevurity>",
  "omflow_restapi": 1,
  "action": "create",
  "formdata": json.dumps(inputjson)
}
files={'files': open('<ファイルパス>','rb')}
requests.post( url, data=values, files=files )
```

## クエリ

「クエリAPI」タブを選択します。このAPIを使用して、フォームデータの最新のIDを検索できます。全ての起票済みのフォームデータは\<data\_id>を取得しないと処理できず、かつ\_**フォームデータの\<data\_id>は、処理プロセスにおいて絶えず変更されていたり、1データに留まらない可能性があります**\_。そのため、処理前にクエリを実行する必要があります。

![起票成功時に戻されるdata\_noを用いて、現在の最新のidを調べることができます。](../.gitbook/assets/jie-tu-20200817-shang-wu-9.56.47.png)

クエリが成功すると、次のようなデータが戻されます。

<pre><code>{
  "status": "200",
  "message": "クエリ成功",
  "result": [
<strong>    {
</strong>      "data_id": "&#x3C;データのユニークなID番号、処理時に使用する>",
      "stop_chart_text": "&#x3C;滞留している処理名称 （手動入力要素の名称）>"
    },...
  ]
}</code></pre>

{% hint style="info" %}
返される結果は1個ではない可能性があります。プロセス設計に並行が含まれる場合、1つの起票データが複数のidで同時進行している場合があります。その為、要素名称で判断した上で、処理を行う必要があります。

注：クエリ結果が１つか複数かに関わらず、配列形式で返されます。
{% endhint %}

クエリが失敗した場合の応答は次のとおりです。

```
{
  "status": "404",
  "message": "クエリ失敗"
}
```

### 処理

「処理API」タブを選択すると、フォーム処理の例が表示されます。

![data\_idはクエリAPIで取得します。](../.gitbook/assets/jie-tu-20200817-shang-wu-9.57.01.png)

処理に成功すると、次のような応答を返します。

```
{
  "status": "200",
  "message": "処理成功",
  "result": ""
}
```

処理に失敗した場合、次のような応答を返します。

```
{
  "status": "404",
  "message": "処理失敗"
}
```
