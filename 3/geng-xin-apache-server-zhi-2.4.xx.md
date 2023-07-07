---
description: OMFLOW 的運行需搭配 Apache Server，當後者因漏洞修復而釋出新版本時。理應同步進行更新，以下介紹更新步驟：
---

# 更新Apache Server至2.4.XX

## Windows

1. 關閉 OMFLOW Server 服務。&#x20;
2. 備份 C:\Program Files\OMFLOW Server\Apache24\conf\httpd.conf。
3. 備份 C:\Program Files\OMFLOW Server\Apache24\conf\extra\httpd-ssl.conf (OMFLOW啟用SSL憑證時必要)。 &#x20;
4. 備份相關certificate及檔案(若OMFLOW的SSL憑證存放於Apache24資料夾時必要)。&#x20;
   * /bin/OMFLOWServer.exe
   * /bin/OMFLOWCollector.exe
5. 備份各專案因特殊需求而自行加入之檔案。
6. 刪除 C:\Program Files\OMFLOW Server\Apache24 資料夾。
7. 下載 Apache 的最新版本並解壓縮至 C:\Program Files\OMFLOW Server\。
8. 修改解壓縮後的資料夾名稱為 Apache24 。
9. 將第2\~5步驟備份的檔案放回原本的路徑。
10. 重啟 OMFLOW Server 服務。

Windows版本的安裝檔已內建Apache Server，以下為對照表。使用者可自行參考是否須更新Apache Server。

<table><thead><tr><th>OMFLOW installer 版本</th><th>內建 Apache Server 版本</th><th data-hidden></th></tr></thead><tbody><tr><td>1.1.0.0</td><td>2.4.43</td><td></td></tr><tr><td>1.1.4.0</td><td>2.4.51</td><td></td></tr></tbody></table>



## **Linux**

1.  透過下方指令關閉 OMFLOW Server 服務。&#x20;

    ```
    /opt/omflow/server/omflow_server stop
    ```
2.  透過下方指令安裝新版本Apache。

    ```
    apt install -y software-properties-common
    add-apt-repository ppa:ondrej/apache2
    apt install -y apache2
    ```
3.  透過下方指令開啟 OMFLOW Server 服務。

    ```
    /opt/omflow/server/omflow_server start
    ```

