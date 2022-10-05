---
description: OMFLOW的備份還原分為Windows及Linux兩種，步驟基本大同小異，但不同環境間彼此不可互換。
---

# 備份與還原

## Windows

#### 備份步驟

1. 備份資料夾 C:\Program Files\OMFLOW Server
2. 將資料庫 OMFLOW 專用 DB 進行 dump

#### 還原步驟

1. 首先將dump的DB重新進行restore
2. 安裝 OMFLOW Server，參考[安裝在Windows](1.md)
   * 安裝時，選擇「不使用資料庫」選項
   * 更新至與備份之相同版本
3. 關閉以下服務
   * OMFLOW Server
   * OMFLOW Server Web
4. 刪除以下資料夾
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
5. 覆蓋備份的所有檔案
6. 根據新環境修改setting.py
   * DATABASES：確保新DB的IP、Port等相關參數無誤
   * LOCAL\_IP：OMFLOW的連入IP，0.0.0.0為任意IP
   * LOCAL\_PORT：OMFLOW的連入Port
   * LOCAL\_PROTOCOL：OMFLOW的SSL設定，http /https二選一
7. 重新啟動服務
   * OMFLOW Server

## Linux

#### 備份步驟

1. 備份資料夾 /opt/omflow
2. 將資料庫 OMFLOW 專用 DB 進行 dump

#### 還原步驟





1. 首先將dump的DB重新進行restore
2. 安裝 OMFLOW Server，參考[安裝在Linux](2.md)
   * 安裝時，選擇「SQLite」選項
   * 更新至與備份之相同版本
3.  關閉以下服務

    ```
    /opt/omflow/server/omflow_server stop
    ```
4. 刪除以下資料夾
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
5. 覆蓋備份的所有檔案
6. 根據新環境修改setting.py
   * DATABASES：確保新DB的IP、Port等相關參數無誤
   * LOCAL\_IP：OMFLOW的連入IP，0.0.0.0為任意IP
   * LOCAL\_PORT：OMFLOW的連入Port
   * LOCAL\_PROTOCOL：OMFLOW的SSL設定，http /https二選一
7.  重新啟動服務

    ```
    /opt/omflow/server/omflow_server start
    ```
