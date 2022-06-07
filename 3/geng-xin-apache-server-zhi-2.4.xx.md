---
description: OMFLOW 的運行需搭配 Apache Server，當後者因漏洞修復而釋出新版本時。理應同步進行更新，以下介紹更新步驟：
---

# 更新Apache Server至2.4.XX

## Windows

1. 關閉 OMFLOW Server 服務。&#x20;
2. 備份 C:\Program Files\OMFLOW Server\Apache24\conf\httpd.conf。
3. 備份 C:\Program Files\OMFLOW Server\Apache24\conf\extra\httpd-ssl.conf (OMFLOW啟用SSL憑證時必要)。 &#x20;
4. 備份相關certificate檔案(若OMFLOW的SSL憑證存放於Apache24資料夾時必要)。&#x20;
5. 備份各專案因特殊需求而自行加入之檔案。&#x20;
6. 刪除 C:\Program Files\OMFLOW Server\Apache24 資料夾。
7. 下載 Apache 的最新版本並解壓縮至 C:\Program Files\OMFLOW Server\。
8. 修改解壓縮後的資料夾名稱為 Apache24 。
9. 將第2\~5步驟備份的檔案放回原本的路徑。
10. 重啟 OMFLOW Server 服務。

Windows版本的安裝檔已內建Apache Server，以下為對照表。使用者可自行參考是否須更新Apache Server。

| OMFLOW installer 版本 | 內建 Apache Server 版本 |   |
| ------------------- | ------------------- | - |
| 1.1.0.0             | 2.4.43              |   |
| 1.1.4.0             | 2.4.51              |   |

****

## **Linux**

****
