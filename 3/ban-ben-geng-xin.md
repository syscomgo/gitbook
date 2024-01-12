---
description: OMFLOW版本更新步驟，分為Windows及Linux兩種
---

# 版本更新

## OMFLOW 1.1.6.4(1.2.0.0): python & django升級

## 目標:

1. python version: 3.8 → 3.11
2. django version: 2.2 → 4.2
3. OMFLOW: 1.1.6.\* → 1.1.6.4

## 步驟:

1.  停止OMFLOW

    ```bash
    omflow_server stop
    ```
2.  刪除/opt/omflow資料夾底下的python資料夾

    ```bash
    rm -rf /opt/omflow/python/
    ```
3. 安裝ubuntu套件
   1. python 3.11
   2. python3.11-dev
   3. python3.11-venv
   4. python3-pip
   5.  線上安裝版(需連線網際網路)

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

       ## 更新套件庫

       ## 新增套件庫

       ## 更新套件庫

       ## 安裝python 3.11及相關套件

       ## 確認python 3.11已經安裝好
   6. 無網路環境、離線安裝方式請見補充
      * 下載Ubuntu套件離線安裝包
      * 離線安裝Ubuntu套件
4.  設定python 3.11為環境變數(可用python 3呼叫)

    ```bash
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1
    ```

    ## 設定<指令>python3指向python 3.11
5.  建立python 3.11的虛擬環境在/opt/omflow資料夾底下

    ```bash
    python3 -m venv /opt/omflow/python
    ```

    ## 建立虛擬環境
6. 進入虛擬環境並安裝python套件
   1. wheel
   2. django==4.2
   3. ldap3
   4. mod\_wsgi
   5. openpyxl
   6. DB會用到的python套件
   7. 其他會用到的套件…
   8.  線上安裝版(需連線網際網路)

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

       ## 進入虛擬環境

       ## 安裝 wheel

       ## 安裝必要套件，其他套件請自行評估安裝
   9. 無網路環境、離線安裝方式請見補充
      * 下載python套件離線安裝包(.whl)
      * 離線安裝python套件
7.  修改apache http.conf裡的wsgi\_module路徑改成新的路徑

    ```bash
    # 修改django.conf
    vim /etc/apache2/sites-enabled/django.conf

    # 修改wsgi_module的路徑
    ```

    修改前，把python3.8、py38、cpython-38改成python3.11、py311、cpython-311

    修改成新的路徑
8.  更新OMFLOW 1.1.6.4

    ```bash
    # 進入tmp
    cd /tmp/

    # 解壓縮patch檔
    tar zxvf /tmp/omflow_patch_1_1_6_4_upgrade3.tar.gz
    ```

    ## 進入tmp、解壓縮patch檔

    ```bash
    # 進入patch資料夾
    cd omflow_patch_1_1_6_4_upgrade4/

    # 執行patch
    ./patch.sh
    ```

    ## 進入patch資料夾、 執行patch

    ## 同意(yes)合併

    ## 回報升版成功
9. 啟動OMFLOW(通常無須手動啟動)

***

* 補充:
  * 下載Ubuntu套件離線安裝包
    * 找一台環境與OMFLOW server相同的Ubuntu，需有網際網路連線。
    * 需要套件:
      * python3.11
      * python3.11-dev
      * python3.11-venv
      * python3-pip
    *   下載指令:

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
    * 下載的安裝包將被保存在 **`/var/cache/apt/archives/`** 目錄下，自行使用FTP軟體取出並放至OMFLOW server環境。
  * 離線安裝Ubuntu套件
    * 需要套件:
      * python3.11
      * python3.11-dev
      * python3.11-venv
      * python3-pip
    * 將 **`.deb`** 文件複製到Ubuntu的某個目錄，此用 \*\*`/tmp/Downloads`\*\*舉例
    *   Ubuntu指令:

        ```bash
        # 切換root身分
        sudo su

        # 移動到安裝包所在的路徑底下
        cd /tmp/Downloads

        # 使用 dpkg 安裝下載的套件包
        dpkg -i *.deb
        ```
    *
  * 從現有環境匯出已安裝的python套件清單
    * 如果您已經有原OMFLOW使用的套件清單可略過本步驟。
    * 參考資料: [https://pip.pypa.io/en/stable/cli/pip\_freeze/](https://pip.pypa.io/en/stable/cli/pip\_freeze/)
    *   匯出指令:

        ```bash
        # 切換到OMFLOW的虛擬環境
        source /opt/omflow/python/bin/activate

        # 匯出python套件清單至/tmp底下
        pip freeze > /tmp/requirements.txt

        # 將django的版本改為4.2以上版本
        vim /tmp/requirements.txt
        ```
    * 自行使用FTP軟體取出並放至有網路的Ubuntu環境，作為後續下載套件的參考。
  * 下載python套件離線安裝包(.whl)
    * 請準備一台已經安裝好python3.11的環境，方便下載python3.11適用的套件版本，此環境必須能連到網路。
    *   下載指令:

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
    * 自行使用FTP軟體取出並放回OMFLOW server。
    * 補充: mod\_wsgi會得到tar.gz，安裝方式較為特別，請見離線安裝mod\_wsgi。
    *
  * 離線安裝python套件
    * 假設python套件的離線安裝包(.whl)放在此路徑`**/opt/omflow/tmp**`底下
    *   安裝指令:

        ```bash
        # 切換到OMFLOW的虛擬環境
        source /opt/omflow/python/bin/activate

        # 切換到離線安裝包的檔案路徑底下
        cd /opt/omflow/tmp

        # 安裝所有whl
        pip install *.whl
        ```
  * 離線安裝mod\_wsgi
    *   安裝指令:

        ```bash
        # 切換到OMFLOW的虛擬環境
        source /opt/omflow/python/bin/activate

        # 解壓縮mod_wsgi的tar.gz
        tar zxvf <mod_wsgi的檔案路徑>

        cd <mod_wsgi解壓縮後的路徑>

        # 簡易安裝mod_wsgi
        python setup.py install
        ```
    *

## 補充:

1. 更換完python & django後，要更新OMFLOW至1.1.6.4(之後可能是1.2.0.0)才能成功啟動
