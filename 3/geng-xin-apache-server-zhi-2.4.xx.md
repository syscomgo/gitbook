---
description: OMFLOW 的運行需搭配 Apache Server，當後者因漏洞修復而釋出新版本時。理應同步進行更新，以下介紹更新步驟：
---

# 更新Apache Server至2.4.XX

1. 關閉 Apache 服務。&#x20;
2. 備份 Apache **原文件夾**。&#x20;
3. 下載 Apache 的最新版本並解壓縮至**新文件夾**。
4. 將**原文件夾**以下檔案複製至**新文件夾**相同位置：
   * httpd.conf
   * httpd-ssl.conf(OMFLOW啟用SSL憑證時必要)
   * 相關certificate檔案(若OMFLOW的SSL憑證存放於原文件夾時必要)
   * 各專案因特殊需求而自行加入之檔案
5. 移除**原文件夾。**
6. 將**新文件夾**重新命名為**原文件夾**路徑。&#x20;
7. 啟動 Apache 服務。

Windows版本的安裝檔已內建Apache Server，以下為對照表。使用者可自行參考是否須更新Apache Server。

| OMFLOW installer 版本 | 內建 Apache Server 版本 |   |
| ------------------- | ------------------- | - |
| 1.1.0.0             | 2.4.43              |   |
| 1.1.4.0             | 2.4.51              |   |

****
