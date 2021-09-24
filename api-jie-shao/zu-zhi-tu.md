---
description: 組織図を使用して、ユーザーの上司または組織の下で特定の位置にいるユーザーを見つけます
---

# 組織図

## フェローシップ

組織図のデフォルトの組織の場所で「**ユーザーアカウント/従業員コード」**を使用し、スーパーバイザーなどの対応するジョブオブジェクトを**上方検索**します。

* Method：POST
* URL：/rest/organization/api/root-position/get/
* 入力パラメータ\(postbody\)：フォーマット例は以下のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"username" : <ユーザーアカウント>,
	"ad_no" : <従業員ID>,
	"position" : <職名>
}
```

* secuity：必須のセキュリティコード。
* omflow\_restapi：必須，1。
* username：ユーザーアカウント番号\（および従業員番号 **1つを選択**できます\）。
* ad\_no：従業員ID \（**ユーザーアカウント番号で**を選択してください\）。
* position：必須、役職または権限名、実際の名前は「投稿、権限名クエリ」を参照できます。 "。

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "クエリは成功しました。",
    "result": {
        "user_ad_no": <ユーザー従業員番号>,
        "username": <ユーザーアカウント>,
        "org_no": <ユーザー組織コード>
    }
}
```

## 組織の位置

組織図の位置で「**組織コード」**を使用し、**下に移動して対応するジョブオブジェクトを検索**します。

* Method：POST
* URL：/rest/organization/api/organization-position/get/
* 入力パラメータ（postbody）：フォーマット例は以下のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード\（security \）を取得する必要があります。取得方法については、\[セキュリティコードの取得\]（an-quan-ma.md）を参照してください。
{% endhint %}

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1,
	"org_no" : <組織コード>,
	"position" : <役職名/権限名>
}
```

* secuity：必須、セキュリティコード。
* omflow\_restapi：必須，1。
* org\_no：オプションの組織コード。 \（組織名と組織番号を入力してください **3つのうちの1つを選択してください**）
* org\_name：オプション、組織名。 \（組織コードと組織番号を入力してください **3つのうちの1つを選択してください**）
* org\_id：オプション、組織番号。 \（組織名と組織コードを入力してください **3つのうちの1つを選択してください**）
* position：必須、役職または権限名、実際の名前は「投稿、権限名クエリ」を参照できます。 "。

APIの戻り例は次のとおりです。

```text
{
    "status": 200,
    "message": "クエリは成功しました。",
    "result": {
        "user_ad_no": <ユーザー従業員番号>,
        "username": <ユーザーアカウント>,
        "org_no": <ユーザー組織コード>
    }
}
```

## 役職、権限、責任名のクエリ

参照組織図

![&#x5834;&#x6240;&#xFF1A;&#x30E1;&#x30A4;&#x30F3;&#x30E1;&#x30CB;&#x30E5;&#x30FC;&amp;gt;&#x4EBA;&#x4E8B;&#x7BA1;&#x7406;&amp;gt;&#x7D44;&#x7E54;&#x56F3;&amp;gt;&#x4F01;&#x696D;&#x7D44;&#x7E54;&amp;gt;&#x30B8;&#x30E7;&#x30D6;&#x30DD;&#x30A4;&#x30F3;&#x30C8;&#xFF08;&#x30B9;&#x30FC;&#x30C4;&#x30B1;&#x30FC;&#x30B9;&#x30A2;&#x30A4;&#x30B3;&#x30F3;&#xFF09;](../.gitbook/assets/image%20%2856%29.png)

![&#x30B8;&#x30E7;&#x30D6;&#x306E;&#x300C;&#x6B6F;&#x8ECA;&#x300D;&#x30A2;&#x30A4;&#x30B3;&#x30F3;&#x3092;&#x30AF;&#x30EA;&#x30C3;&#x30AF;&#x3059;&#x308B;&#x3068;&#x3001;&#x30B8;&#x30E7;&#x30D6;&#x306E;&#x30BF;&#x30A4;&#x30C8;&#x30EB;&#x3068;&#x6A29;&#x9650;&#x306E;&#x540D;&#x524D;&#x304C;&#x8868;&#x793A;&#x3055;&#x308C;&#x307E;&#x3059;](../.gitbook/assets/image%20%288%29.png)

ジョブ管理参照

![&#x5834;&#x6240;&#xFF1A;&#x30E1;&#x30A4;&#x30F3;&#x30E1;&#x30CB;&#x30E5;&#x30FC;&amp;gt;&#x4EBA;&#x4E8B;&#x7BA1;&#x7406;&amp;gt;&#x30B8;&#x30E7;&#x30D6;&#x7BA1;&#x7406;](../.gitbook/assets/image%20%2812%29.png)

![&#x4EFB;&#x610F;&#x306E;&#x4F4D;&#x7F6E;&#x306E;\[&#x7DE8;&#x96C6;\]&#x30DC;&#x30BF;&#x30F3;&#x3092;&#x30AF;&#x30EA;&#x30C3;&#x30AF;&#x3059;&#x308B;&#x3068;&#x3001;&#x542B;&#x307E;&#x308C;&#x3066;&#x3044;&#x308B;&#x6A29;&#x5229;&#x3068;&#x8CAC;&#x4EFB;&#x306E;&#x540D;&#x524D;&#x3092;&#x78BA;&#x8A8D;&#x3067;&#x304D;&#x307E;&#x3059;](../.gitbook/assets/image%20%2861%29.png)

## 組織図のエクスポート

組織図のコンポーネント構造をエクスポートします：

* Method：POST
* URL：/rest/organization/api/organization/load/
* 入力パラメータ\(postbody\)：フォーマット例は以下のとおりです。

{% hint style="info" %}
すべてのAPIを使用する前に、セキュリティコード（security ）を取得する必要があります。取得方法については、セキュリティコードの取得を参照してください。
{% endhint %}

```text
{
	"security" : "<セキュリティコード>",
	"omflow_restapi" : 1
}
```

* secuity：必須、セキュリティコード。
* omflow\_restapi：必填，1。

APIの戻りの例は次のとおりです：

```text
{
    "status": 200,
    "message": "正常に読み取りました。",
    "result": {
        "value": [<組織図オブジェクト>、<組織図オブジェクト>,...],
        "status": False,
        "org_approver": {
             "group" : <組織図レビュー組織>,
             "user" : <組織図レビューア>
         }
    }
}
```

