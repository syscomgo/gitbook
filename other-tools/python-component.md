---
description: 在程式碼元件中可使用的物件與方法範例，範例中所有變數值請依照實際情況進行修改。
---

# 程式碼元件

## 流程相關

### 1. 開單

{% hint style="info" %}
OMFLOW版本 **1.1.5.2** 後可用
{% endhint %}

```python
#匯入
from omflow.syscom.tools import OmData

#宣告一個流程的物件
api_path = 'incident-managment'
inc_flow_obj = OmData(api_path)

#填入表單資料(非必要，視流程需求)
inc_flow_obj.setFormData('formitm_1', 'Apache服務異常')
inc_flow_obj.setFormData('formitm_2', 'red')
inc_flow_obj.setFormData('formitm_3', '1')

#填入流程變數(非必要，視流程需求)
inc_flow_obj.setFlowVariable('message', 'success')
inc_flow_obj.setFlowVariable('password', '1234567')

#送出開單
user_id = '1'   #使用者編號
files = None    #檔案
result = inc_flow_obj.create(user_id, files)

#取得回傳
data_no = result['data_no']    #單號
status = result['status']      #狀態True/False
message = result['message']    #錯誤訊息，開單成功則為空字串
```

### 2. 推單

{% hint style="info" %}
OMFLOW版本 **1.1.5.2** 後可用
{% endhint %}

<pre class="language-python"><code class="lang-python">#匯入
from omflow.syscom.tools import OmData

#宣告一個流程的物件
api_path = 'incident-managment'
inc_flow_obj = OmData(api_path)

#填入表單資料(非必要，視流程需求)
inc_flow_obj.setFormData('formitm_1', 'Apache服務異常')
inc_flow_obj.setFormData('formitm_2', 'red')
inc_flow_obj.setFormData('formitm_3', '1')

#推單
data_id = '345' #資料編號(可透過列表取得)
user_id = '1'   #使用者編號
files = None    #檔案
<strong>result = inc_flow_obj.update(data_id, user_id, files)
</strong><strong>
</strong>#取得回傳
data_no = result['data_no']    #單號
status = result['status']      #狀態True/False
message = result['message']    #錯誤訊息，推單成功則為空字串</code></pre>

### 3. 列表

{% hint style="info" %}
OMFLOW版本 **1.1.5.2** 後可用
{% endhint %}

```python
#匯入
from omflow.syscom.tools import OmData

#宣告一個流程的物件
api_path = 'incident-managment'
inc_flow_obj = OmData(api_path)

#列表
search_conditions = [
    {
        'column':'history',
        'condition':'=',
        'value':False
    },                           #查詢條件，查詢非歷史資料
    {
        'column':'running',
        'condition':'=',
        'value':False
    },                           #查詢條件，查詢非執行中資料
    {
        'column':'error',
        'condition':'=',
        'value':False
    },                           #查詢條件，查詢非異常資料
]
search_columns = [
    'data_no',
    'formitm_1'
]                                #取得欄位，取得單號以及欄位1
exclude_conditions = [
    {
        'column':'close',
        'condition':'=',
        'value':True
    }
]                                #排除條件，排除已關單資料
order_columns = ['-data_no']     #使用單號逆排序
limit = 0                        #取得所有資料(若值給100代表取得前100筆資料)
start = 0                        #從第1筆資料開始
result = inc_flow_obj.list(search_conditions, search_columns, exclude_conditions, order_columns, limit, start)

#取得回傳
#回傳詳細範例請參閱 REST API介紹>查詢表單
```

### 4. 刪單

{% hint style="info" %}
OMFLOW版本 **1.1.6.0** 後可用
{% endhint %}

```python
#匯入
from omflow.syscom.tools import OmData

#宣告一個流程的物件
api_path = 'incident-managment'
inc_flow_obj = OmData(api_path)

#刪單
data_no_list = []    #單號陣列
result = inc_flow_obj.delete(data_no_list)

#取得回傳
status = result['status']      #狀態True/False
message = result['message']    #錯誤訊息，推單成功則為空字
```



### 5. 進階推單

此方法將不使用data\_id進行推單，而是透過使用者給予的條件進行查詢，查詢後依照後續設定進行推單。

{% hint style="info" %}
OMFLOW版本 **1.1.6.0** 後可用
{% endhint %}

```python
#匯入
from omflow.syscom.tools import OmData

#宣告一個流程的物件
api_path = 'incident-managment'
inc_flow_obj = OmData(api_path)

#填入表單資料(非必要，視流程需求)
inc_flow_obj.setFormData('formitm_1', 'Apache服務異常')
inc_flow_obj.setFormData('formitm_2', 'red')
inc_flow_obj.setFormData('formitm_3', '1')

#推單
condition = {}              #查詢條件
'''
condition可接受兩種資料型態(list/dict)
情境一、查詢 單號等於5 的單並推進
list寫法：
condition = []
con = {'column':'data_no','condition':'=','value':5}
condition.append(con)
dict寫法：
condition = {'data_no':5}

情境二、查詢 單號大於5 的單並推進
list寫法：
condition = []
con = {'column':'data_no','condition':'>','value':5}
condition.append(con)
dict寫法：
condition = {'data_no__gt':5}

情境三、查詢 單號大於5且某個輸入欄位的值等於test 的單並推進
list寫法：
condition = []
con = {'column':'data_no','condition':'>','value':5}
con = {'column':'formitm_1','condition':'=','value':'test'}
condition.append(con)
dict寫法：
condition = {'data_no__gt':5, 'formitm_1':'test'}
'''

user_id = '1'               #使用者編號
files = None                #檔案
update_duplicate = False    #當條件查詢回來的資料為複數筆時，是否將其全部推進。若否，則全部不推進並回傳失敗訊息。
wait_time_max = 0           #當查詢回來的資料筆數為0時，要進行n次重新查詢，n次查詢都為0後回傳錯誤訊息。
wait_time_seconds = 0       #每次重新查詢的間隔時間(秒)
result = inc_flow_obj.advanced_update(condition, user_id, files, update_duplicate, wait_time_seconds, wait_time_max)

#取得回傳
status = result['status']      #狀態True/False
message = result['message']    #回傳訊息。成功推單的data_id或是失敗訊息。
```



## 使用者



```
//some code
```



## 部門/角色



```
//some code
```

