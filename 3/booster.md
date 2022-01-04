---
description: 支援Python：3.7以上
---

# Booster

## 功能介紹 <a href="#gong-neng-jie-shao" id="gong-neng-jie-shao"></a>

### 負載平衡架構 <a href="#fu-zai-ping-heng-jia-gou" id="fu-zai-ping-heng-jia-gou"></a>

當用戶需要長時間大量開單或是眾多使用者同時上線等極耗效能情境出現，導致單台OMFLOW Server難以負荷時。OMFLOW也提供了負載平衡的機制，可同時建置多台OMFLOW Server分散效能，並由Booster進行協同調配進而提升整體效率，架構圖如下：

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M6SrengyyhO1h0\_BsJ\_-887967055%2Fuploads%2FDUxpuyBy8A1zF1gzYHeD%2FBooster%E6%9E%B6%E6%A7%8B.jpg?alt=media\&token=c543a601-44f9-4db8-80e2-4c01a5002e06)

### 負載平衡兼高可用架性構 <a href="#fu-zai-ping-heng-jian-gao-ke-yong-jia-xing-gou" id="fu-zai-ping-heng-jian-gao-ke-yong-jia-xing-gou"></a>

同時OMFLOW也提供了高可用性的架構，將Booster分為「主、副」兩台，所有OMFLOW Server都會依此順序向Booster報到，以確保此架構任一節點失去聯繫時，系統仍能正常運作。

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M6SrengyyhO1h0\_BsJ\_-887967055%2Fuploads%2F0Q0pS32qtvMERVEO5lEp%2FBoosterHA%E6%9E%B6%E6%A7%8B.jpg?alt=media\&token=f2c9db39-202e-47c0-86ec-0837fd6fae24)

#### OMFLOW Booster <a href="#omflow-booster" id="omflow-booster"></a>

擔任資料傳遞中心，主要負責協同所有OMFLOW Server共同處理表單流程。平時由主Booster進行作業。當主Booster失去聯繫時，會改由副Booster接替作業，形成高可用性架構。

#### OMFLOW Booster Agent <a href="#omflow-booster-agent" id="omflow-booster-agent"></a>

使用Booster架構時，Booster Agent需要與OMFLOW Server安裝在同一環境上，其作用為當任一台OMFLOW Server更新Patch時，所有其他的OMFLOW Server也會自動更新。

## 安裝步驟 <a href="#an-zhuang-bu-zhou" id="an-zhuang-bu-zhou"></a>

### 1. 安裝 OMFLOW Booster <a href="#1.-an-zhuang-omflow-booster" id="1.-an-zhuang-omflow-booster"></a>

最優先安裝，並依照情境安裝一台或兩台Booster。兩者無順序要求，安裝時需填入以下資訊：

#### 輸入本機IP/Domain 及 Port： <a href="#shu-ru-ben-ji-ipdomain-ji-port" id="shu-ru-ben-ji-ipdomain-ji-port"></a>

填寫此Booster所代表的IP/Domain及Port，並確保所有OMFLOW Server與此連通。

#### 輸入 HA Booster IP/Domain 及 Port(非必填)： <a href="#shu-ru-ha-booster-ipdomain-ji-port-fei-bi-tian" id="shu-ru-ha-booster-ipdomain-ji-port-fei-bi-tian"></a>

當情境為HA架構時，填寫另一台Booster所代表的IP/Domain及Port，並確保兩台Booster彼此能互相連通。HA架構下，一台為主Booster，一台為副Booster

### 2. 建置資料庫 <a href="#2.-jian-zhi-zi-liao-ku" id="2.-jian-zhi-zi-liao-ku"></a>

Booster架構並不支援Sqlite，需要事先建立好對應的資料庫。OMFLOW支援的資料庫如下：

* PostgreSQL
* MySQL
* SQL Server
* Oracle

準備好資料庫以及具備建立資料表和讀寫該資料庫權限的帳號​

### 3. 安裝 OMFLOW Server <a href="#3.-an-zhuang-omflow-server" id="3.-an-zhuang-omflow-server"></a>

當Booster安裝完畢後，接著安裝本架構的**第一台OMFLOW Server**。安裝過程會需要額外填入以下資訊：

#### 輸入DB相關資訊： <a href="#shu-ru-db-xiang-guan-zi-xun" id="shu-ru-db-xiang-guan-zi-xun"></a>

請輸入[步驟2](https://app.gitbook.com/s/-M6SrengyyhO1h0\_BsJ\_-887967055/3/an-zhuang-booster#2.-jian-zhi-zi-liao-ku)所準備的資料庫相關資訊。

#### 輸入 Booster IP 及 Port： <a href="#shu-ru-booster-ip-ji-port" id="shu-ru-booster-ip-ji-port"></a>

請輸入視為主Booster的相關資訊。

#### 輸入 HA Booster IP 及 Port： <a href="#shu-ru-ha-booster-ip-ji-port" id="shu-ru-ha-booster-ip-ji-port"></a>

請輸入視為副Booster的相關資訊。

#### 先前已安裝OMFLOW Server： <a href="#xian-qian-yi-an-zhuang-omflow-server" id="xian-qian-yi-an-zhuang-omflow-server"></a>

若在安裝Booster之前已有運行中的OMFLOWServer，可按照以下步驟進行：

1. 確保運行中的OMFLOW Server資料庫並非Sqlite
2. 將OMFLOW Server更新至最新版本
3. 修改setting.py文件，將Booster相關資訊填入BOOSTER\_IP、BOOSTER\_PORT、SECOND\_BOOSTER\_IP、SECOND\_BOOSTER\_PORT四個參數
4. 重啟OMFLOW Server

### 4. 安裝 OMFLOW Booster Agent <a href="#4.-an-zhuang-omflow-booster-agent" id="4.-an-zhuang-omflow-booster-agent"></a>

待第一台OMFLOW Server安裝完畢後，在同一環境上繼續安裝OMFLOW Booster Agent。BoosterAgent需與OMFLOWServer安裝在同一台伺服器上。

### 5. 安裝 OMFLOW Slave <a href="#5.-an-zhuang-omflow-slave" id="5.-an-zhuang-omflow-slave"></a>

待以上步驟皆完成後，最後便是依照情境的需求安裝一台以上的OMFLOWSlave。OMFLOWSlave內已包含OMFLOW Server及OMFLOWBooster Agent，安裝過程會需要額外填入以下資訊：

#### 輸入 Booster IP 及 Port： <a href="#shu-ru-booster-ip-ji-port-1" id="shu-ru-booster-ip-ji-port-1"></a>

請輸入視為主Booster的相關資訊。

#### 輸入 HA Booster IP 及 Port： <a href="#shu-ru-ha-booster-ip-ji-port-1" id="shu-ru-ha-booster-ip-ji-port-1"></a>

請輸入視為副Booster的相關資訊。

## 啟動順序 <a href="#qi-dong-shun-xu" id="qi-dong-shun-xu"></a>

在啟動順序上，Booster及DB為最高優先順序，再來啟動所有的Booster Agent。

1. Booster、Database
2. Booster Agent

Booster Agent 啟動時會自動啟動 OMFLOW Server。
