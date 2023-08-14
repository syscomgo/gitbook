---
description: OMFLOWのバックアップと復元はWindowsとLinuxの2種類に分かれており、基本的に手順は似ていますが、異なる環境間では互換性がありません。
---

# バックアップと復元

## Windows

### OMFLOW Server

#### バックアップ手順

1. バックアップフォルダC:\Program Files\OMFLOW Server
2. データベースOMFLOW専用DBをダンプ(dump)する。

復元手順

1. ダンプのDBをリストアする。
2. OMFLOW Serverをインストールする。詳細はインストール・Windowsを参照してください。
   * インストールする時に、「Do not use database 」オプションを選択する。
   * バックアップと同じバージョンにアップデートする。
3. 以下のサービスを終了する。
   * OMFLOW Server&#x20;
   * OMFLOW Server Web
4. インストール後、以下のフォルダを削除する。
   * ...\OMFLOW Server\omflow\omcustom\migrations
   * ...\OMFLOW Server\omflow\omdashboard\migrations
   * ...\OMFLOW Server\omflow\omflow\migrations
   * ...\OMFLOW Server\omflow\omformflow\production
   * ...\OMFLOW Server\omflow\omformflow\migrations
   * ...\OMFLOW Server\omflow\omformmodel\migrations
   * ...\OMFLOW Server\omflow\omldap\migrations
   * ...\OMFLOW Server\omflow\ommessage\migrations
   * ...\OMFLOW Server\omflow\ommission\migrations
   * ...\OMFLOW Server\omflow\ommobile\migrations
   * ...\OMFLOW Server\omflow\ommonitor\migrations
   * ...\OMFLOW Server\omflow\omorganization\migrations
   * ...\OMFLOW Server\omflow\omformflow\migrations
   * ...\OMFLOW Server\omflow\ompolicymodel\migrations
   * ...\OMFLOW Server\omflow\omreport\migrations
   * ...\OMFLOW Server\omflow\omservice\migrations
   * ...\OMFLOW Server\omflow\omuser\migrations
5. バックアップしたすべてのファイルを上書きする
6. 新しい環境に合わせて修正する...\OMFLOW Server\omflow\omflow\setting.py
   * DATABASES：新しいDBのIP、Port、とその他の関連パラメータが正しいことを確認する。
   * LOCAL\_IP：OMFLOWの接続IP、0.0.0.0は任意のIP。
   * LOCAL\_PORT：OMFLOWの接続IP
   * LOCAL\_PROTOCOL：OMFLOWのSSL設定、http /httpsのいずれを選択する。
7. 以下のサービスを再起動する。
   * OMFLOW Server

### OMFLOW Collector

#### バックアップ手順

1. OMFLOW Collector とOMFLOW Collector Web サービスを停止する。
2. バックアップフォルダ C:\Program Files\OMFLOW Collector

#### 復元手順

1. OMFLOW Collectorをインストールする。詳細はインストール・Windowsを参照してください。
   * バックアップと同じバージョンにアップデートする。
2. 以下のサービスを終了する。
   * OMFLOW Collector
   * OMFLOW Collector Web
3. インストール後、以下のフォルダを削除する。
   * ...\OMFLOW Collector\omflow\omcustom\migrations
   * ...\OMFLOW Collector\omflow\omdashboard\migrations
   * ...\OMFLOW Collector\omflow\omflow\migrations
   * ...\OMFLOW Collector\omflow\omformflow\production
   * ...\OMFLOW Collector\omflow\omformflow\migrations
   * ...\OMFLOW Collector\omflow\omformmodel\migrations
   * ...\OMFLOW Collector\omflow\omldap\migrations
   * ...\OMFLOW Collector\omflow\ommessage\migrations
   * ...\OMFLOW Collector\omflow\ommission\migrations
   * ...\OMFLOW Collector\omflow\ommobile\migrations
   * ...\OMFLOW Collector\omflow\ommonitor\migrations
   * ...\OMFLOW Collector\omflow\omorganization\migrations
   * ...\OMFLOW Collector\omflow\omformflow\migrations
   * ...\OMFLOW Collector\omflow\ompolicymodel\migrations
   * ...\OMFLOW Collector\omflow\omreport\migrations
   * ...\OMFLOW Collector\omflow\omservice\migrations
   * ...\OMFLOW Collector\omflow\omuser\migrations
4. バックアップしたすべてのファイルを上書きする
5. 新しい環境に合わせて修正する ...\OMFLOW Collector\omflow\omflow\setting.py
   * LOCAL\_IP：OMFLOW Collectorの接続IP、0.0.0.0は任意のIP
   * LOCAL\_PORT：OMFLOW Collectorの接続Port
6. 以下のサービスを再起動する。
   * OMFLOW Collector

## Linux

### OMFLOW Server

#### バックアップ手順

1. バックアップフォルダ /opt/omflow
2. データベースOMFLOW専用DBをダンプ(dump)する。

#### 復元手順

1. ダンプのDBをリストアする。
2. OMFLOW Serverをインストールする。詳細はインストール・Linux​を参照してください。
   * バックアップと同じバージョンにアップデートする。
   * インストールの際、「SQLite」オプションを選択する。
3. 以下のサービスを終了する。
   * /opt/omflow/server/omflow\_server stop
4. インストール後、以下のフォルダを削除する。
   * /opt/omflow/server/omcustom/migrations
   * /opt/omflow/server/omdashboard/migrations
   * /opt/omflow/server/omflow/migrations
   * /opt/omflow/server/omformflow/productions
   * /opt/omflow/server/omformflow/migrations
   * /opt/omflow/server/omformmodel/migrations
   * /opt/omflow/server/omldap/migrations
   * /opt/omflow/server/ommessage/migrations
   * /opt/omflow/server/ommission/migrations
   * /opt/omflow/server/ommobile/migrations
   * /opt/omflow/server/ommonitor/migrations
   * /opt/omflow/server/omorganization/migrations
   * /opt/omflow/server/omformflow/migrations
   * /opt/omflow/server/ompolicymodel/migrations
   * /opt/omflow/server/omreport/migrations
   * /opt/omflow/server/omservice/migrations
   * /opt/omflow/server/omuser/migrations
5. バックアップしたすべてのファイルを上書きする
6. 新しい環境に合わせて修正する /opt/omflow/server/omflow/setting.py
   * DATABASES：新しいDBのIP、Port、とその他の関連パラメータが正しいことを確認する。
   * LOCAL\_IP：OMFLOWの接続IP、0.0.0.0は任意のIP。
   * LOCAL\_PORT：OMFLOWの接続IP
   * LOCAL\_PROTOCOL：OMFLOWのSSL設定、http /httpsのいずれを選択する
7. 以下のサービスを再起動する。
   * /opt/omflow/server/omflow\_server start

### OMFLOW Collector

#### バックアップ手順

1. バックアップフォルダ /opt/omflow

#### 復元手順

1. OMFLOW Collectorをインストールする。詳細はインストール・Linux​を参照してください。
   * バックアップと同じバージョンにアップデートする。
2. 以下のサービスを終了する。
   * /opt/omflow/server/omflow\_collector stop
3. インストール後、以下のフォルダを削除する。
   * /opt/omflow/collector/omcustom/migrations
   * /opt/omflow/collector/omdashboard/migrations
   * /opt/omflow/collector/omflow/migrations
   * /opt/omflow/collector/omformflow/productions
   * /opt/omflow/collector/omformflow/migrations
   * /opt/omflow/collector/omformmodel/migrations
   * /opt/omflow/collector/omldap/migrations
   * /opt/omflow/collector/ommessage/migrations
   * /opt/omflow/collector/ommission/migrations
   * /opt/omflow/collector/ommobile/migrations
   * /opt/omflow/collector/ommonitor/migrations
   * /opt/omflow/collector/omorganization/migrations
   * /opt/omflow/collector/omformflow/migrations
   * /opt/omflow/collector/ompolicymodel/migrations
   * /opt/omflow/collector/omreport/migrations
   * /opt/omflow/collector/omservice/migrations
   * /opt/omflow/collector/omuser/migrations
4. バックアップしたすべてのファイルを上書きする
5. 新しい環境に合わせて修正する /opt/omflow/collector/omflow/setting.py
   * LOCAL\_IP：OMFLOWの接続IP、0.0.0.0は任意のIP。
   * LOCAL\_PORT：OMFLOWの接続IP
6. 以下のサービスを再起動する。
   * /opt/omflow/server/omflow\_collector start
