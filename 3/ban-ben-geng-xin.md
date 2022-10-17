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
