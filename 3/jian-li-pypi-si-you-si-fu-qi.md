# 架設PyPI伺服器

OMFlow流程中的程式碼元件可以執行python程式碼，使用者可以在網路、社群尋找好用的範例程式或套件，來架構出屬於自己的流程。此時就會有需要另外安裝python套件的需求產生，接下來會說明如何安裝python套件。

當伺服器有對外網路時，安裝套件可以直接透過omflow來完成，使用者只需要在流程中python元件的套件頁籤(詳細可參考[元件介紹](../5/6.md#cheng-shi-ma))，填入需要安裝的套件名稱，上架流程時系統會檢查是否已經安裝該套件，若是尚未安裝則會自動幫使用者安裝套件。

若是伺服器沒有對外網路，此時就需要使用者架設伺服器了，下面會說明如何建立PyPI伺服器。

## 架設伺服器

基本需求：python、pip

架設伺服器最基本就是環境中必須要有安裝python，python如何安裝、設定環境變數等請自行至python官方網站瀏覽，這裡就不多贅述了。

#### 步驟一、安裝套件

如果伺服器的環境有對外網路，打開命令提示字元，鍵入以下指令

```
pip install devpi-server
pip install devpi-client
```

如果沒有對外網路，請在有對外網路的環境中，取得該套件，可以直接google搜尋devpi並下載套件：

{% embed url="https://pypi.org/project/devpi-server/#files" %}

{% embed url="https://pypi.org/project/devpi-client/#files" %}

{% hint style="info" %}
為符合教學情境，請下載.whl的檔案。
{% endhint %}

或是透過python指令下載，指令如下：

```
pip download devpi-server -d <下載路徑>
pip download devpi-client -d <下載路徑>
```

接著將下載下來的whl檔案移至伺服器的環境中，再次打開命令提示字元鍵入下列指令：

```
pip install <devpi-server.whl路徑>
pip install <devpi-client.whl路徑>
```



#### 步驟二、初始化devpi伺服器

安裝好devpi套件之後，接著要進行伺服器的初始設定，指令如下：

```
devpi-init --serverdir="/devpi"
```

{% hint style="info" %}
\--serverdir後面的路徑，代表伺服器的位置，可以自行調整。
{% endhint %}

#### 步驟三、啟動伺服器

建立帳號之後，即可啟動伺服器，指令如下：

```
devpi-server --serverdir="/devpi" --restrict-modify=root --port=3141 --host=<IP位置>
```

{% hint style="info" %}
\--port=3141是預設值，可以自行修改。

\--host=請填入當前架設環境的ip。
{% endhint %}

{% hint style="warning" %}
如果架設伺服器的環境有對外網路，完成至此步驟後請跳至第五步驟。
{% endhint %}

#### 步驟四、設定client

在沒有對外網路的情況下，使用者只能另外下載套件，最後上傳至伺服器作統一管理，此時就需要用到client套件，設定指令如下：

```
#設定client指向的server位置
devpi use http://<IP位置>:<Port>
```

{% hint style="info" %}
ip與port都是步驟三所設定的位置。
{% endhint %}

```
#登入
devpi login root --password=<密碼>

#在root使用者下建立自己的資料夾
devpi index -c local
```

{% hint style="info" %}
local可以自行更換。
{% endhint %}

```
#切換至剛才建立的local資料夾
devpi use root/local

#上傳已經下載好的套件至PyPI伺服器
devpi upload --from-dir <各式自行下載的套件whl檔案路徑>
```

至此，PyPI伺服器架設就完成了。

#### 步驟五、設定omflow server

架設完伺服器後，必須要到omflow設定，這樣上架應用時，系統就會根據此設定至pypi server下載安裝套件。

登入omflow > 系統設定 > 系統設定

![](../.gitbook/assets/pip-server.png)

紅匡位置填入伺服器的位置後，儲存即可生效。

{% hint style="info" %}
如果pypi伺服器有對外網路，填入的路徑位置範例：

http://\<IP>:3141/root/pypi/+simple/
{% endhint %}

{% hint style="info" %}
如果沒有對外網路，填入的路徑位置範例：

http://\<IP>:3141/root/local/
{% endhint %}

