# User

## General search

Query user data that meets specific conditions

* Method：POST
* URL：/rest/accounts/api/user/list/
* postbody:

{% hint style="info" %}
All API must obtain a security code (security) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method.
{% endhint %}

```
{
    "security" : "<code>",
    "omflow_restapi" : 1,
    "search_conditions" : [],
    "search_columns" : [],
    "exclude_conditions" : [],
    "order_columns" : [],
    "limit" : 100,
    "start" : 0
}
```

*   search\_columns：Optional, the name of the field to be queried. The format example is as follows.

    ```
    "search_columns" : ["id", "username", "nick_name"]
    ```

{% hint style="info" %}
If search\_columns is not filled, all field names and field values of the query form will be returned.
{% endhint %}

* search\_conditions：Optional, filter out the data that meet the conditions. Each condition in the array is a JSON object structure, and each condition is an AND relationship. The default is to query all data.
  * column：For the field name, please refer to the example of [returned data.](shi-yong-zhe.md#general-search-return-format)
  * condition：Condition characters are divided into the following five types.
    * \=：Filter out the data exactly the same as value.
    * \>：Filter out data greater than value.
    * <：Filter out data less than value.
    * in：Filter out the same data as in the value array.
    * contains：Filter out data that contains value.
  * value：For the field value, fill in the corresponding value in accordance with [User Data](../5/8.md#user-management).

```
"search_conditions" :
[
    {
        "column" : "username",
        "condition" : "in",
        "value" : ["admin", "user001"]
    },
    {
        "column" : "id",
        "condition" : ">",
        "value" : 3
    },
    <other conditions>,...
]
```

* exclude\_conditions：Optional. Exclude data that meets the conditions. The format is the same as search\_conditions. The default is not to exclude any conditions.
*   order\_columns：Optional, sort according to the specified field. If you need to sort in reverse, please add a "-" sign in front of the field name. The default is to sort by \["id"]. The example format is as follows.

    ```
    #asc
    "order_columns" : ["id"]

    #desc
    "order_columns" : ["-id"]
    ```
* limit：Optional, fill in the number to get to the number of data, the default is 100.
* start：Optional, fill in the number from the number of data to obtain, the default is the 0th.

{% hint style="info" %}
example 1: start=0, limit=100, return 100 rows

example 2: start=1, limit=100, return 99 rows

example 3: start=100, limit=100, return 0 rows
{% endhint %}

## General search return format

API Response:

```
{
    "status": 200,
    "message": "success",
    "result": [
        {
            "id": <user id>,
            "password": <Encrypted password>,
            "last_login": <last login time>,
            "is_superuser": <is superuser>,
            "username": <account>,
            "first_name": <first name>,
            "last_name": <last name>,
            "is_active": <active>,
            "email": <email>,
            "nick_name": <nick name>,
            "birthday": <birthday>,
            "gender": <grnder>,
            "phone1": <phone>,
            "phone2": <cell phonr>,
            "extension_no": <extension>,
            "company": <company name>,
            "ad_flag": <ad>,
            "ad_sid": <ad sid>,
            "frequency": <Front-end refresh rate>,
            "updatetime": <update time>,
            "delete": <delete>,
            "default_group": <default organization>,
            "ad_no": <employee ID>
        },...
    ]
}
```

## Organization Search

Use the **group\_no** to search for users under these organizations.

* Method：POST
* URL：/rest/accounts/api/user/list-by-group/
* postbody:

{% hint style="info" %}
All apis must obtain a security code (security) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method.
{% endhint %}

```
{
    "security" : "<code>",
    "omflow_restapi" : 1,
    "group_no" : []
}
```

* security：Require
* omflow\_restapi：Require, 1.
* group\_no：Require, organization No，Multiple organization No can be placed in the array.

API Response:

```
{
    "status": 200,
    "message": "success",
    "result": {
        "<group_no>": [
            {
                "user": <user id>, #This is the number used by the omflow database
                "user__nick_name": <user nick name>,
                "user__username": <user account>,
                "user__ad_no": <user ad_no>
            },...
        ],
        "<group_no>": [
            {
                "user": <user id>, #This is the number used by the omflow database
                "user__nick_name": <user nick name>,
                "user__username": <user account>,
                "user__ad_no": <user ad_no>
            },...
        ],
    }
}
```
