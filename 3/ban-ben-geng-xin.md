---
description: OMFLOW版本更新步驟，分為Windows及Linux兩種
---

# 版本更新

## Windows

### 第一步驟，備份OMFLOW

請先備份OMFLOW，備份方式請詳見[備份與還原](bei-fen-yu-huan-yuan.md)

### 第二步驟，執行更新檔

OMFLOW 的 Windows 更新檔可以直接執行，在更新檔按下右鍵後選擇「以系統管理員身份執行」。

### 第三步驟，選擇語系

選擇顯示的語言後按下「確定」。

### 第四步驟，同意使用條款

勾選使用條款須知的「我同意」後按下「下一步」。

### 第五步驟，開始更新

執行檔會檢查你的設備是否可以使用當前的更新，檢查完畢後按下「更新」

{% hint style="info" %}
如果出現版本不符情況，請先檢查OMFLOW版本，與更新檔版本是否可以使用。

OMFLOW 在 1.1.4.0之後的版本，可以直接使用最新的更新檔升級到最新版本。

如果設備上的 OMFLOW 版本小於 1.1.4.0，請依照 OMFLOW 版本順序，

依序更新到 1.1.4.0 後再使用最新的更新檔。
{% endhint %}

### 第六步驟，服務重啟

更新完畢後會自動重啟OMFLOW服務，服務重啟完畢後按下「結束」即完成更新。

{% hint style="info" %}
1.1.4.0 以前的版本更新後，請確認OMFLOW服務已重新啟動後，再繼續更新。
{% endhint %}

現在你可以繼續使用OMFLOW了！

## 版本 1.2.0.0 更新 Python

OMFLOW在1.2.0.0版本後將Python版本升級至3.11，若用戶在過去版本額外安裝python套件，更新過程會要求用戶手動安裝Python，以下為相關步驟：

1. 下載 Python3.11 ( 32 Bit ) Windows Installer 並執行
2. 選擇 Customize installation 自定義安裝路徑
3. 安裝路徑選擇 C:\PROGRA\~1\OMFLOW Server\Python311
4. 安裝完畢後，可在更新視窗點擊「下一步」進行檢查
5. 此時更新視窗會檢查比對原Python及Python311套件清單是否相符，並列出缺失套件。
6. 若有缺失套件，以**管理者權限**開啟CMD視窗，並進入Python311資料夾下
7. 以 python.exe -m pip install 指令進行安裝
8. 安裝後點擊下一步進行檢查，以此循環直到無缺失套件
9. 關閉所有原Python及Python311相關CMD視窗

## Linux

### 第一步驟，備份OMFLOW

請先備份OMFLOW，備份方式請詳見[備份與還原](bei-fen-yu-huan-yuan.md)

### 第二步驟，解壓縮更新檔

解壓縮 patch 檔&#x20;

```bash
tar -zxvf [patch檔路徑]
```

### 第三步驟，執行更新檔

移動至 patch.sh 的路徑上，執行 patch.sh

```bash
cd [patch檔路徑]
sudo ./patch.sh
```

### 第四步驟，重啟服務

確認 OMFLOW 服務是否正常啟動

```bash
/opt/omflow/server/omflow_server status
```

若服務尚未被啟動，請將服務開啟

```bash
/opt/omflow/server/omflow_server start
```

現在你可以繼續使用OMFLOW了！

## 錯誤處理

如果更新完 OMFLOW 後無法啟動服務，請嘗試將備份的 OMFLOW [還原](bei-fen-yu-huan-yuan.md)，再重新執行更新步驟。
