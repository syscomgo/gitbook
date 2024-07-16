# OMFLOW概觀

OMFLOW 是一個相當泛用的流程引擎，你可以隨意的設計表單讓人填寫並定義處理程序，也可以幫你處理資料流和自動化命令。

OMFLOW 分為 Server 以及 Collector，Server的角色為資料中心，負責收集和儲存數據以及流程執行。 Collector(收集器)則是可以被用來做為 Server 分散運算的角色以及被派送定期定期執行的流程。

一般而言，使用者透過瀏覽器連接OMFLOW Server 操作整個OMFLOW系統，並在OMFLOW Server 上設計App。

![](https://syscomgo.com/wp-content/uploads/2023/11/OMFLOW\_2-1\_1.png)

在OMFLOW Server中，你可以設計自己的APP，也可以從雲端下載我們寫好的APP進行使用，APP裡面可以包含多個FLOW，而FLOW是由表單和工作流程所組成，我們透過這種方式，將業務流程和實際的資料或是自動化命令等進行組合。當然，OMFLOW 包含了工作區的概念，你可以隨時匯出匯入和下載任何的APP，只要你不做上架的動作，對系統不會有任何的影響。

![](https://syscomgo.com/wp-content/uploads/2023/11/OMFLOW\_2-1\_2.png)

Collector是我們一個很重要的概念，OMFLOW 使用 Python語言開發，所以你也可以嵌入 Python 程式碼在流程之中，流程中的 Python 程式碼要被執行時，你可以將他設定為分散式運算，如此這些運算的動作就會自動分散到各個 Collector 中。

當然，Collector 顧名思義他也包含了接受外部呼叫將數據傳入中心，以及主動執行流程取得所要的數據。

## 軟體下載

### 商業版 免費(Free License) 可至syscomgo下載

[https://syscomgo.com/products/omflow/](https://syscomgo.com/products/omflow/)

## 軟體授權

* 商業版 免費(Free License) 為自syscomgo網站下載的較多功能版本，這個版本非GPL授權，個人及學術機構與評估用途免費使用.
* 商業版 企業(Enterprise License) 為自syscomgo網站下載的較多功能版本，用於商業目的或企業，組織，政府或教育機構。
