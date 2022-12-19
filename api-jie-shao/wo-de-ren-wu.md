---
description: this is translated by machine
---

# My Mission

## Query

* Method：POST
* URL：/rest/my-mission/api/my-mission/list/
* Input parameters (postbody): The example format is as follows.

{% hint style="info" %}
All apis must obtain a security code (security) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method.
{% endhint %}

```
{
    "security" : "<security>",
    "omflow_restapi" : 1,
    "search_columns" : [],
    "search_conditions" : [],
    "exclude_conditions" : [],
    "order_columns" : [],
    "limit" : 100,
    "start" : 0
}
```

* secuity：Required, security code.
* omflow\_restapi：Required，1。
*   search\_columns：Optional, **the name of the field** to be queried. The format example is as follows.

    ```
    "search_columns" : ["id", "status", "level"]
    ```

{% hint style="info" %}
If search\_columns is not filled, all **field names** and **field values** of the query form will be returned.
{% endhint %}

* search\_conditions：Optional, filter out the data that meet the conditions. Each condition in the array is a JSON object structure, and each condition has an AND relationship. The default is to query all data.
  * column：Field name, please refer to [_**Return data**_](wo-de-ren-wu.md#hui-chuan-zi-liao)，If it is a **custom form**, please refer to the id value in [_Create Data API_ ](kuai-su-kai-chan-tui-chan.md)_._
  * condition：Condition characters are divided into the following five types.
    * \=：Filter out the data exactly the same as value.
    * \>：Filter out data greater than value.
    * <：Filter out data less than value.
    * in：Filter out the same data as in the value array.
    * contains：Filter out data that contains value.
  * value：Field value,Follow [_**APP Management > Design APP > Form Design**_](../5/6.md#xin-jian-bian-ji-liu-cheng-ye-mian-biao-chan-she-ji)  and fill in the corresponding values.

```
"search_conditions" :
[
    {
        "column" : "status",
        "condition" : "in",
        "value" : ["assigned", "review"]
    },
    {
        "column" : "id",
        "condition" : ">",
        "value" : 3
    },
    <other conditions>,...
]
```

* exclude\_conditions：Optional, exclude data that meets the conditions, the format is the same as search\_conditions, and the default is not to exclude any conditions.
*   order\_columns：Optional, sort according to the specified field. If you need to sort in reverse, please add a "-" sign in front of the field name. The default is to sort by \["id"]. The example format is as follows.

    ```
    #Positive Sort
    "order_columns" : ["id"]

    #Reverse Sort
    "order_columns" : ["-id"]
    ```
* limit：Optional, fill in the number to get to the number of data, the default is 100.
* start：Optional, fill in the number from the first data to obtain, the default is  start from 0.

{% hint style="info" %}
Example 1:start=0,limit=100,return 100 data.

Example 2:start=1,limit=100,return 99 data.

Example 3:start=100,limit=100,return 0 data.
{% endhint %}

## Return data

When successful, an example of the returned data is as follows:

```
{
    "status": 200,
    "message": "Query successful",
    "result": [
        {
            "id": 6,
            "flow_uuid": "67d4cf9a-49cd-4341-90da-b899eb0219b1",
            "flow_name": "Problem Management",
            "status": "assigned",
            "level": "",
            "title": "123",
            "data_no": 1,
            "data_id": 4,
            "history": false,
            "stop_uuid": "FITEM_7",
            "stop_chart_text": "Job Assigned",
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

When it fails, the example of returned data is as follows:

```
{
    "status": 404,
    "message": "Query failed:<error message>",
    "result": []
```
