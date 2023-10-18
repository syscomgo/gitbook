---
description: 透過組織圖尋找使用者的主管或是組織底下特定職務的使用者
---

# 組織圖

## 查詢組織圖資訊



## 同系職務

以「**使用者帳號/員工代號」**在組織圖的預設組織位置，**往上搜尋**對應的職務對象，如主管：

* Method：POST
* URL：/rest/organization/api/root-position/get/
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

```
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"username" : <使用者帳號>,
	"ad_no" : <員工編號>,
	"position" : <職務名稱/權責名稱>
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。
* username：使用者帳號(與員工編號**二擇一**即可)。
* ad\_no：員工編號(與使用者帳號**二擇一**即可)。
* position：必填，職務名稱或權責名稱，實際名稱可參考「[職務、權責名稱查詢](zu-zhi-tu.md#zhi-wu-quan-ze-ming-chen-cha-xun)」。

API回傳範例如下：

```
{
    "status": 200,
    "message": "查詢成功。",
    "result": {
        "user_ad_no": <使用者員工編號>,
        "username": <使用者帳號>,
        "org_no": <使用者組織代號>
    }
}
```



## 組織職務

以「**組織代號」**在組織圖的位置，**往下搜尋**對應的職務對象：

* Method：POST
* URL：/rest/organization/api/organization-position/get/
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

```
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"org_no" : <組織代號>,
	"position" : <職務名稱/權責名稱>
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。
* org\_no：選填，組織代號。(與組織名稱、組織編號**三擇一**填入)
* org\_name：選填，組織名稱。(與組織代號、組織編號**三擇一**填入)
* org\_id：選填，組織編號。(與組織名稱、組織代號**三擇一**填入)
* position：必填，職務名稱或權責名稱，實際名稱可參考「[職務、權責名稱查詢](zu-zhi-tu.md#zhi-wu-quan-ze-ming-chen-cha-xun)」。

API回傳範例如下：

```
{
    "status": 200,
    "message": "查詢成功。",
    "result": {
        "user_ad_no": <使用者員工編號>,
        "username": <使用者帳號>,
        "org_no": <使用者組織代號>
    }
}
```



## 組織圖匯出

匯出組織圖元件架構：

* Method：POST
* URL：/rest/organization/api/organization/load/
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

```
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。

API回傳範例如下：

```
{
    "status": 200,
    "message": "讀取成功。",
    "result": {
        "value": [<組織圖物件>,<組織圖物件>,...],
        "status": False,
        "org_approver": {
             "group" : <組織圖審核組織>,
             "user" : <組織圖審核人>
         }
    }
}
```

