---
description: 使用API查詢我的任務清單。
---

# 我的任務

## 查詢

* Method：POST
* URL：/rest/my-mission/api/my-mission/list/
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

```
{
	"security" : "<安全碼>",
	"omflow_restapi" : 1,
	"search_columns" : [],
	"search_conditions" : [],
	"exclude_conditions" : [],
	"order_columns" : [],
	"limit" : 100,
	"start" : 0
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。
*   search\_columns：選填，要查詢的**欄位名稱**。格式範例如下。

    ```
    "search_columns" : ["id", "status", "level"]
    ```

{% hint style="info" %}
若未填 search\_columns ，會回傳查詢表單所有**欄位名稱、欄位值**。
{% endhint %}

* search\_conditions：選填，篩選出符合條件的資料。陣列中每個條件為JSON物件結構，每個條件之間為AND關係，預設為查詢所有資料。
  * column：欄位名稱，可參考[_**回傳資料範例**_](wo-de-ren-wu.md#hui-chuan-zi-liao)，若為**自訂表單**可參考[_開單API_](kuai-su-kai-chan-tui-chan.md#kai-chan)中的id值。
  * condition：條件字元，分為下列五種。
    * \=：篩選出與value完全相同的資料。
    * \>：篩選出大於value的資料。
    * <：篩選出小於value的資料。
    * in：篩選出與value陣列中相同的資料。
    * contains：篩選出包含value的資料。
  * value：欄位值，依照 [_**應用管理 > 應用設計 > 表單設計**_](../5/6.md#xin-jian-bian-ji-liu-cheng-ye-mian-biao-chan-she-ji) 而填入對應值。

```
"search_conditions" :
[
    {
        "column" : "status",
        "condition" : "in",
        "value" : ["指派", "審核中"]
    },
    {
        "column" : "id",
        "condition" : ">",
        "value" : 3
    },
    <其他條件>,...
]
```

* exclude\_conditions：選填，排除掉符合條件的資料，格式與search\_conditions相同，預設為不排除任何條件。
*   order\_columns：選填，依照指定欄位進行排序。需要逆向排序請在欄位名稱前方加上"-"號，預設為以 \["id"] 進行排序。範例格式如下。

    ```
    #正排序
    "order_columns" : ["id"]

    #逆排序
    "order_columns" : ["-id"]
    ```
* limit：選填，填入數字取得至第幾筆資料，預設為100筆。
* start：選填，填入數字從第幾筆資料開始取得，預設為第 0 筆。

{% hint style="info" %}
例1：start=0，limit=100，回傳100筆資料。

例2：start=1，limit=100，回傳99筆資料。

例3：start=100，limit=100，回傳0筆資料。
{% endhint %}

### 回傳資料

成功時，回傳資料範例如下所示：

```
{
    "status": 200,
    "message": "查詢成功。",
    "result": [
        {
            "id": 6,
            "flow_uuid": "67d4cf9a-49cd-4341-90da-b899eb0219b1",
            "flow_name": "問題管理",
            "status": "指派",
            "level": "",
            "title": "123",
            "data_no": 1,
            "data_id": 4,
            "history": false,
            "stop_uuid": "FITEM_7",
            "stop_chart_text": "指派人工",
            "create_user_id": "system",
            "update_user_id": null,
            "ticket_createtime": "2020-07-07T13:50:21.494",
            "createtime": "2020-07-07T13:50:21.589",
            "updatetime": "2020-07-07T13:50:21.589",
            "assignee_id": null,
            "assign_group_id": 1,
            "action": ",",
            "attachment": false,
            "closed": false
        },.....
    ]
}
```

失敗時，回傳資料範例如下：

```
{
    "status": 404,
    "message": "查詢失敗，錯誤訊息如下：<錯誤訊息>",
    "result": []

```



## 推單

* Method：POST
* URL：/rest/flowmanage/api/omdata/edit/\<api\_path>
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

{% hint style="danger" %}
目前URL上的api\_path只能透過手動查詢。

如何查詢api路徑請參考[應用管理](../5/6.md#yi-shang-jia-liu-cheng-lie-biao)。

後續版本更新會在我的任務列表中新增api\_path的欄位。
{% endhint %}

```
{
  "security": "<security>",
  "omflow_restapi": 1,
  "action": "update",
  "data_id": "<data_id>",
  "formdata": [
    {
      "id": "<FORMITM_X>",
      "value": "<欄位值>"
    },
    {
      "id": "FORMITM_X",
      "value": "<欄位值>"
    },......
  ]
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。
* action：必填，填入"update"即可。
* data\_id：必填，填入查詢API所查詢到的data\_id。
* formdata：選填，填入要修改的欄位及欄位內容。

### 回傳資料

成功時，回傳資料範例如下：

```
{
  "status": "200",
  "message": "推單成功",
  "result": ""
}
```



## 快速操作

* Method：POST
* URL：/rest/flowmanage/api/omdata/edit/\<api\_path>
* 輸入參數(postbody)：範例格式如下。

{% hint style="info" %}
所有api使用前須取得安全碼(security)，取得方式請參閱[取得安全碼](an-quan-ma.md)。
{% endhint %}

{% hint style="danger" %}
目前URL上的api\_path只能透過手動查詢。

如何查詢api路徑請參考[應用管理](../5/6.md#yi-shang-jia-liu-cheng-lie-biao)。

後續版本更新會在我的任務列表中新增api\_path的欄位。
{% endhint %}

```
{
  "security": "<security>",
  "omflow_restapi": 1,
  "action": "update",
  "data_id": "<data_id>",
  "quick_action": "<action1/action2>"
}
```

* secuity：必填，安全碼。
* omflow\_restapi：必填，1。
* action：必填，填入"update"即可。
* data\_id：必填，填入查詢API所查詢到的data\_id。
* quick\_action：必填，填入 action1 或是 action2。

### 回傳資料

成功時，回傳資料範例如下：

```
{
  "status": "200",
  "message": "推單成功",
  "result": ""
}
```



## 範例程式碼

### Python

查詢我的任務列表，並針對指定的表單流程進行推單動作

```
#====================================
# OMFLOW 我的任務範例
# 請參考 https://doc.omflow.com.tw/api-jie-shao/wo-de-ren-wu
#====================================
import sys,requests,json

url = 'https://1.2.3.4' # OMFLOW 伺服器的位址
url_login = '/accounts/api/security/get/'
url_my_mission = '/rest/my-mission/api/my-mission/list/'
url_action = '/rest/flowmanage/api/omdata/edit/'

api_path = 'some-api-path-syscom' #指定要處理的任務的 API Path(應用管理,已上架應用中可看到)
api_id = '38ea93dc82za39as0a38ei1'  #指定要處理任務的 uuid (點開該表單，網址列可看到)


data_security = '' #存放登入成功的安全碼

#====================================
# 登入OMFLOW
# 全域變數: data_security , url , url_login
# 輸入 : user=帳號 , pwd=密碼
# 回傳 : 200 = 成功
#====================================
def login(user,pwd):
    global data_security
    response = requests.get( url + url_login, auth=( user, pwd ))
    data = response.json()
    data_code_int = data['status']
    data_security = data['result']['security']
    return data_code_int
#====================================
# 取得我的任務清單
# 全域變數: data_security , url , url_my_mission
# 輸入 : 無
# 回傳 : 我的任務列表(JSON格式)
#====================================
def myMissonList():
    values={
        "security" : data_security,
        "omflow_restapi" : 1,
        "search_columns" : [],
        "search_conditions" : [],
        "exclude_conditions" : [],
        "order_columns" : [],
        "limit" : 100,
        "start" : 0
    }
    response = requests.post( url + url_my_mission, data=values )
    data = response.json()
    data_list = data['result']
    return data_list

#====================================
# 針對指定的流程進行核准
# 全域變數: data_security , url , url_action , api_path , api_id
# 輸入 : 我的任務列表(JSON格式)
# 回傳 : 無
#====================================
def approve(data_list):
    #列印 data_list 可取得所有資料
    for item in data_list:
        data_flow_uuid = item['flow_uuid']
        data_data_id = item['data_id']
        if data_flow_uuid.replace('-','') == api_id:
            #組織送單內容，可在應用管理,已上架應用中可範例
            values = {
                    "security": data_security,
                    "omflow_restapi": 1,
                    "action": "update",
                    "data_id": data_data_id,
                    "formdata": [
                        {
                            "id": "FORMITM_5",
                            "value": "審核通過"
                        }
                    ]
                }
            response = requests.post(  url + url_action + api_path, data= json.dumps(values))
            print('flow:' + data_flow_uuid + ',data:' + str(data_data_id) + ',approved.')

#MAIN
if len(sys.argv) != 3:
    print('error')
else:
    if login(sys.argv[1] , sys.argv[2]) == 200:
        approve(myMissonList())

```

### PowerShell

查詢我的任務列表

```
#====================================
# OMFLOW my mission example
# refrence https://doc.omflow.com.tw/api-jie-shao/wo-de-ren-wu
#====================================

#url = OMFLOW Server URL
#token = user password
#user = user name

$url = 'https://1.2.3.4' 
$token='password' 
$user ='user'
$api_path = 'some-api-path-syscom' 
$api_id = '1ko2kme1o9a120a03a0dfs' 

$url_login = '/accounts/api/security/get/'
$url_my_mission = '/rest/my-mission/api/my-mission/list/'
$url_action = '/rest/flowmanage/api/omdata/edit/'




$security = ''


$auth = $user + ':' + $token
$encoded = [System.Text.Encoding]::UTF8.GetBytes($auth)
$authorizationInfo = [System.Convert]::ToBase64String($encoded)
$headers = @{"Authorization"="Basic $($authorizationInfo)"}

$result = Invoke-WebRequest -Uri "$url$url_login" -Method GET -Headers $headers
if ($result.StatusCode -eq 200)
{
    $result_json = $result.Content | ConvertFrom-Json
	#echo $result_json.status
	#echo $result_json.message
	$security = $result_json.result.security
}
else
{
    echo "login fail."
}

if ($security -ne "")
{
    $postParams = @{
        "security"=$security;
        "omflow_restapi"=1;
        "search_columns"=@();
        "search_conditions"=@();
        "exclude_conditions"=@();
        "order_columns"=@();
        "limit"=100;
        "start"=0
		}
	$result = Invoke-WebRequest -Uri "$url$url_my_mission" -Method POST -Body $postParams
	$result_json = $result.Content | ConvertFrom-Json
	$count = $result_json.result.length
	echo "total $count mission"
}

```
