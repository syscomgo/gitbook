# 版本更新

## 版本更新

OMFLOW版本更新步驟，分為Windows及Linux兩種。其中版本號分為四碼，如1.2.0.0。當需要升級版本時，需查看當前OMFLOW前三碼與更新版本是否相同，若有差異如

### Windows

#### 一般版本更新步驟

1. **備份OMFLOW**

請先備份OMFLOW，備份方式請詳見「備份與還原」章節

2. **執行更新檔**

OMFLOW 的 Windows 更新檔可以直接執行，在更新檔按下右鍵後選擇「以系統管理員身份執行」。

3. **選擇語系**

選擇顯示的語言後按下「確定」。

4. **同意使用條款**

勾選使用條款須知的「我同意」後按下「下一步」。

5. **開始更新**

執行檔會檢查你的設備是否可以使用當前的更新，檢查完畢後按下「更新」

> 如果出現版本不符情況，請先檢查OMFLOW版本，與更新檔版本是否可以使用。\
> OMFLOW 在 1.1.4.0之後的版本，可以直接使用最新的更新檔升級到最新版本。\
> 如果設備上的 OMFLOW 版本小於 1.1.4.0，請依照 OMFLOW 版本順序，依序更新到 1.1.4.0 後再使用最新的更新檔。

6. **服務重啟**

更新完畢後會自動重啟OMFLOW服務，服務重啟完畢後按下「結束」即完成更新。

> 1.1.4.0 以前的版本更新後，請確認OMFLOW服務已重新啟動後，再繼續更新。

現在你可以繼續使用OMFLOW了！

#### 1.2.0.0注意事項

OMFLOW在1.2.0.0版本後將Python版本升級至3.11，若用戶在過去版本額外安裝python套件，更新過程會要求用戶手動安裝Python，以下為相關步驟：

1. 下載 `Python3.11 ( 32 Bit ) Windows Installer` 並執行
2. 選擇 `Customize installation` 自定義安裝路徑
3. 安裝路徑選擇 `C:\PROGRA~1\OMFLOW Server\Python311` (如安裝路徑錯誤可用複製方式移動資料夾)
4. 安裝完畢後，可在更新視窗點擊「下一步」進行檢查
5. 此時更新視窗會檢查比對原Python及Python311套件清單是否相符
6. 若有缺失套件，以**管理者權限**開啟CMD視窗，並進入Python311資料夾下，在1.2.0.1版本會看到 `requirements.txt` 檔案
7. 如有網路環境，以 `pip install -r requirements.txt` 指令進行安裝
8. 或是以 `python.exe -m pip install` 指令針對`requirements.txt`內逐一套件進行安裝
9. 安裝後點擊下一步進行檢查，以此循環直到無缺失套件
10. 關閉所有原Python及Python311相關CMD視窗

### Linux

#### 一般更新步驟

1. **備份OMFLOW**

請先備份OMFLOW，備份方式請詳見「備份與還原」章節

2. **解壓縮更新檔**

解壓縮 patch 檔

```bash
        tar -zxvf [patch檔路徑]
```

3. **執行更新檔**

移動至 patch.sh 的路徑上，執行 patch.sh

```bash
        cd [patch檔路徑]
        sudo ./patch.sh
```

4. **重啟服務**

確認 OMFLOW 服務是否正常啟動

```bash
        /opt/omflow/server/omflow_server status
```

若服務尚未被啟動，請將服務開啟

```bash
        /opt/omflow/server/omflow_server start
```

現在你可以繼續使用OMFLOW了！

#### Linux 更新 1.2.0.0 版本步驟

OMFLOW在1.2.0.0版本對環境需求進一步提升，使用Linux環境之用戶需手動更新，以下為相關步驟：

> python version: 3.8 → 3.11\
> django version: 2.2 → 4.2

1. **停止OMFLOW**

```bash
        omflow_server stop
```

2. **刪除/opt/omflow資料夾底下的python資料夾**

```bash
        rm -rf /opt/omflow/python/
```

3. **安裝ubuntu套件**

> 套件清單
>
> * python 3.11
> * python3.11-dev
> * python3.11-venv
> * python3-pip

安裝方式一：線上安裝版(需連線網際網路)

```bash
        # 更新套件庫
        apt-get update -y
        # 增加套件庫
        add-apt-repository ppa:deadsnakes/ppa -y
        # 更新套件庫
        apt-get update -y

        # 安裝python3.11及相關套件
        apt-get install -y python3.11 python3.11-dev python3.11-venv python3-pip
```

安裝方式二：無網路環境、離線安裝方式請見補充

> 下載Ubuntu套件離線安裝包\
> 離線安裝Ubuntu套件

4. **設定python 3.11為環境變數(使得python3.11可用指令python3呼叫)**

```bash
        update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1
```

5. **建立python 3.11的虛擬環境在/opt/omflow資料夾底下**

```bash
        python3 -m venv /opt/omflow/python
```

6. **進入虛擬環境並安裝python套件**

> python套件清單
>
> * wheel
> * django==4.2
> * ldap3
> * mod\_wsgi
> * openpyxl
> * DB會用到的python套件
> * 其他會用到的套件…
> * 線上安裝版(需連線網際網路)

```bash
        # 進入虛擬環境
        source /opt/omflow/python/bin/activate

        # 安裝 wheel
        pip install wheel

        # 非必要可略
        python /usr/lib/python3.11/test/libregrtest/setup.py bdist_wheel

        # 安裝必要套件，其他套件請自行評估安裝
        pip install django==4.2 ldap3 mod_wsgi openpyxl
```

無網路環境、離線安裝方式請見補充

> 下載python套件離線安裝包(.whl)\
> 離線安裝python套件

7. **修改apache http.conf裡的wsgi\_module路徑改成新的路徑**

```bash
        # 修改django.conf
        vim /etc/apache2/sites-enabled/django.conf

        # 修改wsgi_module的路徑
```

8. **更新並啟動OMFLOW 1.2.0.0**

```bash
        # 進入tmp
        cd /tmp/

        # 解壓縮patch檔
        tar zxvf /tmp/omflow_patch_1_1_6_4_upgrade3.tar.gz

        # 進入patch資料夾
        cd omflow_patch_1_1_6_4_upgrade4/

        # 執行patch
        ./patch.sh
```

#### 補充:

**下載Ubuntu套件離線安裝包**

找一台環境與OMFLOW server相同的Ubuntu，需有網際網路連線。

> 需要套件:
>
> * python3.11
> * python3.11-dev
> * python3.11-venv
> * python3-pip

下載指令:

```bash
        # 切換root身分
        sudo su
        
        # 新增套件庫**deadsnakes** PPA
        add-apt-repository ppa:deadsnakes/ppa
        
        # 更新套件列表: 
        apt-get update
        
        # (如果需要的話)清理預設的下載資料夾
        apt-get clean
        
        # 下載但不安裝套件
        apt-get install --download-only python3.11 python3.11-dev python3.11-venv python3-pip
```

下載的安裝包將被保存在 **`/var/cache/apt/archives/`** 目錄下，自行使用FTP軟體取出並放至OMFLOW server環境。

**離線安裝Ubuntu套件**

> 需要套件:
>
> * python3.11
> * python3.11-dev
> * python3.11-venv
> * python3-pip

將 **`.deb`** 文件複製到Ubuntu的某個目錄，此用 \*\*`/tmp/Downloads`\*\*舉例

Ubuntu指令:

```bash
        # 切換root身分
        sudo su
        
        # 移動到安裝包所在的路徑底下
        cd /tmp/Downloads
        
        # 使用 dpkg 安裝下載的套件包
        dpkg -i *.deb
```

**從現有環境匯出已安裝的python套件清單**

如果您已經有原OMFLOW使用的套件清單可略過本步驟。

參考資料: [https://pip.pypa.io/en/stable/cli/pip\_freeze/](https://pip.pypa.io/en/stable/cli/pip\_freeze/)

匯出指令:

```bash
        # 切換到OMFLOW的虛擬環境
        source /opt/omflow/python/bin/activate
        
        # 匯出python套件清單至/tmp底下
        pip freeze > /tmp/requirements.txt
        
        # 將django的版本改為4.2以上版本
        vim /tmp/requirements.txt
```

自行使用FTP軟體取出並放至有網路的Ubuntu環境，作為後續下載套件的參考。

**下載python套件離線安裝包(.whl)**

請準備一台已經安裝好python3.11的環境，方便下載python3.11適用的套件版本，此環境必須能連到網路。

下載指令:

```bash
        # 新增一個存放離線安裝包的資料夾
        mkdir /tmp/python_package
        cd /tmp/python_package
        
        # [方法一]使用requirements.txt批次下載
        # 假設您已經將前一步的requirements.txt放在/tmp/底下
        pip -m install /tmp/requirements.txt
        
        # [方法二]手動輸入套件名稱下載
        pip -m install <套件名稱>
        
        # 下載完成後檢視資料夾內有多少.whl安裝檔
        ll
```

自行使用FTP軟體取出並放回OMFLOW server。

> 補充: mod\_wsgi會得到tar.gz，安裝方式較為特別，請見離線安裝mod\_wsgi。

**離線安裝python套件**

假設python套件的離線安裝包(.whl)放在此路徑`**/opt/omflow/tmp**`底下

安裝指令:

```bash
        # 切換到OMFLOW的虛擬環境
        source /opt/omflow/python/bin/activate
        
        # 切換到離線安裝包的檔案路徑底下
        cd /opt/omflow/tmp
        
        # 安裝所有whl
        pip install *.whl
```

**離線安裝mod\_wsgi**

安裝指令:

```bash
        # 切換到OMFLOW的虛擬環境
        source /opt/omflow/python/bin/activate
        
        # 解壓縮mod_wsgi的tar.gz
        tar zxvf <mod_wsgi的檔案路徑>
        
        cd <mod_wsgi解壓縮後的路徑>
        
        # 簡易安裝mod_wsgi
        python setup.py install
```

#### 注意:

更換完python & django後，要更新OMFLOW版本至1.2.0.0才能成功啟動；之前的版本無法搭配django 4.2使用。

#### 錯誤處理

如果更新完 OMFLOW 後無法啟動服務，請依照「備份與還原」章節將 OMFLOW 進行還原，再重新執行更新步驟。
