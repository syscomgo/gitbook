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
        'column':'closed',
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
con1 = {'column':'data_no','condition':'>','value':5}
condition.append(con1)
con2 = {'column':'formitm_1','condition':'=','value':'test'}
condition.append(con2)
dict寫法：
condition = {'data_no__gt':5, 'formitm_1':'test'}
'''

user_id = '1'                  #使用者編號
files = None                   #檔案
update_duplicate = False       #當條件查詢回來的資料為複數筆時，是否將其全部推進。若否，則全部不推進並回傳失敗訊息。
update_duplicate_interval = 0  #當推進的資料為複數筆時，每一筆推進的間隔時間(秒)
wait_time_max = 0              #當查詢回來的資料筆數為0時，要進行n次重新查詢，n次查詢都為0後回傳錯誤訊息。
wait_time_seconds = 0          #每次重新查詢的間隔時間(秒)
result = inc_flow_obj.advanced_update(condition, user_id, files, update_duplicate, update_duplicate_interval, wait_time_seconds, wait_time_max)

#取得回傳
status = result['status']      #狀態True/False
message = result['message']    #回傳訊息。成功推單的data_id或是失敗訊息。
```



## 使用者

{% hint style="info" %}
OMFLOW版本 **1.1.6.0** 後可用
{% endhint %}

### 1. 建立使用者

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#填入使用者資料(必填)
username = 'a12345'
token = 'aA!123456'
nick_name ='王小明'
email = 'a12345@gmail.com'

#填入使用者資料(選填)
#有下列欄位可填
#birthday, gender, phone1, phone2, company, default_group, ad_no, extension_no
other_param_dict = {}
other_param_dict['ad_no'] = '001234'
other_param_dict['phone1'] = '0911111111'

#建立使用者
result = user_obj.create(username, token, nick_name, email, other_param_dict)

#取得回傳
user_id = result['user_id']    #使用者id
status = result['status']      #狀態True/False
message = result['message']    #錯誤訊息，開單成功則為空字串
```



### 2. 更新使用者

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#選擇要修改的使用者(必填，user_id與username二選一填入)
user_id = None
username = None

#更改密碼(選填)
token = 'aA!123456'

#填入要更新的使用者欄位(選填)
#有下列欄位可填
#email, birthday, gender, phone1, phone2, company, default_group, ad_no, extension_no
other_param_dict = {}
other_param_dict['phone1'] = '0911111111'

#更新使用者
result = user_obj.update(user_id, username, token, other_param_dict)
#若 result = 'success' 代表成功，失敗則會回傳錯誤訊息
```



### 3. 查詢使用者(列表)

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#查詢條件(下為範例，請依照實際需求修改)
search_conditions = [
    {
        'column':'gender',
        'condition':'=',
        'value':'female'
    },                           #查詢條件，查詢女性使用者
]

search_columns = [
    'username',
    'email'
]                                #取得欄位，取得帳號以及信箱

exclude_conditions = [
    {
        'column':'is_active',
        'condition':'=',
        'value':False
    }
]                                #排除條件，排除停用的使用者

order_columns = ['-username']    #使用帳號逆排序
limit = 0                        #取得所有資料(若值給100代表取得前100筆資料)
start = 0                        #從第1筆資料開始

#查詢使用者
result = user_obj.list(search_conditions, search_columns, exclude_conditions, order_columns, limit, start)

#取得回傳
#回傳詳細範例請參閱 REST API介紹>使用者
```



### 4. 查詢使用者(單一)

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#查詢條件(必填，下列三選一填入)
user_id = None
username = None
nick_name = None

#填入要查詢的使用者欄位
#有下列欄位可填
#id, username, nick_name, email, birthday, gender, phone1, phone2, company, default_group, ad_no, extension_no
#若留空代表查詢全部欄位
user_attr = []

#查詢使用者
result = user_obj.load(user_id, username, nick_name, user_attr)

#取得回傳(請依照查詢的欄位取得資料)
#result資料結構如下
{
    'id':123,
    'username':'12312',
    'nick_name':'王小明',
    'email':'123@gamil.com',    #上述欄位會依照user_attr變數不同而有所不同
    'groups':[],                #groups與roles則是固定提供之回傳，與user_attr填入與否無關
    'roles':[],                 #groups回傳使用者所在部門的部門id陣列, roles回傳使用者所在角色的角色id陣列
}
```



### 5. 查詢使用者Email(列表)

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#填入要查詢的使用者id(陣列)
user_id_list = []

#查詢多位使用者email
result = user_obj.listEmail(user_id_list)
#result資料格式如下
['aaa@gmail.com','bbb@gmail.com','ccc@gmail.com','ddd@gmail.com']
```



### 6. 刪除使用者

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#填入要查詢的使用者帳號(陣列)
username_list = []

#刪除使用者
result = user_obj.delete(username_list)
#result若等於空字串代表刪除成功，回傳任何文字訊息代表是錯誤訊息
```



### 7. 使用者加入部門

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#選擇使用者(必填)
user_id = None

#填入要加入的部門id陣列(必填)
group_id_list = []

#使用者加入部門
result = user_obj.addtoGroup(user_id, group_id_list)
#result為boolean，True代表成功，False代表失敗
```



### 8. 使用者移出部門

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#選擇使用者(必填)
user_id = None

#填入要移出的部門id陣列(必填)
group_id_list = []

#使用者移出部門
result = user_obj.removefromGroup(user_id, group_id_list)
#result為boolean，True代表成功，False代表失敗
```



### 9. 透過組織圖尋找人員

```python
#匯入
from omflow.syscom.tools import User

#宣告一個流程的物件
user_obj = User()

#選擇使用者(必填)
user_id = None

#填入要查詢對象的職務名稱或職務代號或權責名稱(必填，下列三選一填入)
position_name = None
position_no = None
responsibilitie_name = None

#查詢組織圖
result = user_obj.getPosition(user_id, position_name, position_no, responsibilitie_name)

#取得回傳
manager_user_id = result.get('user_id','')
manager_group_id = result.get('group_id','')
```



## 部門/角色

{% hint style="info" %}
OMFLOW版本 **1.1.6.0** 後可用
{% endhint %}

### 1. 建立部門

```python
#匯入
from omflow.syscom.tools import Group

#宣告一個部門(角色)的物件
group_obj = Group()

#填入資料(必填)
group_name = 'test'          #部門名稱
is_role = False                #填入True為角色，False為部門

#填入資料(選填)
parent_group_id = None         #父部門id，角色不可填
description = ''               #說明欄位
group_no = ''                  #部門代號

#建立部門
result = group_obj.create(parent_group_id, group_name, description, group_no, is_role)

#取得回傳
group_id = result['group_id']  #部門/角色id
status = result['status']      #狀態True/False
message = result['message']    #錯誤訊息，開單成功則為空字串
```



### 2. 取得部門資訊

```python
#匯入
from omflow.syscom.tools import Group

#宣告一個部門(角色)的物件
group_id = ''
group_no = ''
group_name = ''
#部門id/部門代號/部門名稱請三選一填入值
group_obj = Group(group_id, group_no, group_name)

#讀取部門資訊
result = group_obj.load()

#取得回傳
group_id = result.get('id','')                       #部門id
display_name = result.get('display_name','')         #部門名稱
parent_group_id = result.get('parent_group_id','')   #父部門id
description = result.get('description','')           #說明
group_no = result.get('group_no','')                 #部門代號
group_user_list = result.get('group_user_list','')   #該部門底下有的使用者id
permissions = result.get('permissions','')           #該角色有的權限，查詢部門時回傳為空陣列
```



### 3. 加入使用者

```python
#匯入
from omflow.syscom.tools import Group

#宣告一個部門(角色)的物件
group_id = ''
group_no = ''
group_name = ''
#部門id/部門代號/部門名稱請三選一填入值
group_obj = Group(group_id, group_no, group_name)

#填入使用者id列表
user_id_list = []

#部門加入使用者，result為boolean，True代表成功，False代表失敗
result = group_obj.addUsers(user_id_list)
```



### 4. 移出使用者

```python
#匯入
from omflow.syscom.tools import Group

#宣告一個部門(角色)的物件
group_id = ''
group_no = ''
group_name = ''
#部門id/部門代號/部門名稱請三選一填入值
group_obj = Group(group_id, group_no, group_name)

#填入使用者id列表
user_id_list = []

#部門移出使用者，result為boolean，True代表成功，False代表失敗
result = group_obj.removeUsers(user_id_list)
```



### 5. 透過組織圖尋找人員

```python
#匯入
from omflow.syscom.tools import Group

#宣告一個部門(角色)的物件
group_id = ''
group_no = ''
group_name = ''
#部門id/部門代號/部門名稱請三選一填入值
group_obj = Group(group_id, group_no, group_name)

#填入要查詢對象的職務名稱或職務代號或權責名稱(必填，下列三選一填入)
position_name = None
position_no = None
responsibilitie_name = None

#查詢組織圖
result = group_obj.getPosition(position_name, position_no, responsibilitie_name)

#取得回傳
manager_user_id = result.get('user_id','')
manager_group_id = result.get('group_id','')
```





