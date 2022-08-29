---
description: >-
  OMFLOWを利用するにはApache Serverが必要です。Apache
  Serverの脆弱性対応の新バージョンがリリースされた場合、速やかに更新する必要があります。更新手順は以下の通りです：
---

# Apache Serverの2.4.XXへの更新

## Windows <a href="#windows" id="windows"></a>

1. OMFLOW Server サービスを停止する。
2. C:\Program Files\OMFLOW Server\Apache24\conf\httpd.conf をバックアップする。
3. C:\Program Files\OMFLOW Server\Apache24\conf\extra\httpd-ssl.conf をバックアップする（OMFLOWがSSL証明書を有効化している場合は必要）。
4. 関連するcertificateファイルをバックアップする（OMFLOWのSSL証明書がApache24フォルダに格納されている場合は必要）。
5. 個別の必要性により独自ファイルを格納している場合は、該当のファイルをバックアップする。
6. C:\Program Files\OMFLOW Server\Apache24 フォルダを削除する。
7. Apache の最新バージョンをダウンロードし、C:\Program Files\OMFLOW Server\ に解凍する。
8. 解凍後のフォルダ名を Apache24 に変更する。
9. 2～5でバックアップしたファイルを元のパスに戻す。
10. OMFLOW Server サービスを起動する。

Windows版のインストーラはApache Serverを含みます。下記の対照表を参照し、Apache Serverの更新要否を判断してください。**​**

| OMFLOW Version | Apache2 Version |
| -------------- | --------------- |
| 1.1.0.0        | 2.4.43          |
| 1.1.4.0        | 2.4.51          |

## **Linux** <a href="#linux" id="linux"></a>

1. 次のコマンドにより、OMFLOW Server サービスを停止します。

```
/opt/omflow/server/omflow_server stop
```

&#x20;  2\. 次のコマンドにより、新バージョンのApacheをインストールします。

```
apt install -y software-properties-common
add-apt-repository ppa:ondrej/apache2
apt install -y apache2
```

&#x20; 3\. 次のコマンドにより、OMFLOW Server サービスを起動します。

```
/opt/omflow/server/omflow_server start
```
