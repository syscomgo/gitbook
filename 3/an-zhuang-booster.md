# 安裝Booster

## 功能介紹

![](../.gitbook/assets/Booster架構.jpg)

![](../.gitbook/assets/BoosterHA架構.jpg)

支援Python：3.7以上

#### OMFLOW Booster

#### OMFLOW Server

#### OMFLOW Booster Agent

#### OMFLOW Slave

## 安裝



### 1.  安裝 OMFLOW Booster

最優先安裝，並依照情境安裝一台或兩台Booster。兩者無順序要求，安裝時需填入以下資訊：

#### 輸入本機IP/Domain 及 Port：

填寫此Booster所代表的IP/Domain及Port，並確保所有OMFLOW Server與此連通。

#### 輸入 HA Booster IP/Domain 及 Port(非必填)：

當情境為HA架構時，填寫另一台Booster所代表的IP/Domain及Port，並確保兩台Booster彼此能互相連通。



### 2.&#x20;

### 3. 安裝 OMFLOW Server

當Booster安裝完畢後，接著安裝本架構的第一台OMFLOW Server。

#### DB不選擇Sqlite：

Booster架構並不支援Sqlite。同時需要事先建立好對應的資料庫

#### 輸入 Booster IP 及 Port：



#### 輸入 HA Booster IP 及 Port：

#### 先前已安裝OMFLOW Server：



### 4. 安裝 OMFLOW Booster Agent

### 5. 安裝 OMFLOW Slave

#### 輸入 Booster IP：

#### 輸入 Booster Port：

#### 輸入 HA Booster IP：

#### 輸入 HA Booster Port：

## 啟動順序

1. Booster
2. Database
3. Master Booster Agent
4. Slave Booster Agent
