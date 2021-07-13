---
description: >-
  Use the organization chart to find the user's supervisor or a user with a
  specific position under the organization
---

# Organization

## Direct Position

Use "user account/employee code" in the default organization position of the organization chart to search for the corresponding job object, such as supervisor:

* Method：POST
* URL：/rest/organization/api/root-position/get/
* postbody:

{% hint style="info" %}
All apis must obtain a security code \(security\) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method
{% endhint %}

```text
{
    "security" : "",
    "omflow_restapi" : 1,
    "username" : "",
    "ad_no" : "",
    "position" : ""
}
```

* secuity：Require
* omflow\_restapi：Require, 1.
* username：user account\(Just choose one with the ad\_no\)。
* ad\_no：employee ID\(Just choose one with the username\)。
* position：Required, job title or responsibility name, actual name can refer to "Where to get Job, Responsibility Name".

Response Example:

```text
{
    "status": 200,
    "message": "查詢成功。",
    "result": {
        "user_ad_no": "",
        "username": "",
        "org_no": ""
    }
}
```

## Department position

Use "Organization No" in the position of the organization chart to search for the corresponding job object:

* Method：POST
* URL：/rest/organization/api/organization-position/get/
* postbody：Required, job title or responsibility name, actual name can refer to "Where to get Job, Responsibility Name".

{% hint style="info" %}
All apis must obtain a security code \(security\) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method
{% endhint %}

```text
{
    "security" : "",
    "omflow_restapi" : 1,
    "org_no" : "",
    "position" : ""
}
```

* secuity：Required
* omflow\_restapi：Required, Fill in 1
* org\_no：Required, Fill in Organization No \(Just choose one between org\_no, org\_name, org\_id\)
* org\_name：Required, Fill in Organization No \(Just choose one between org\_no, org\_name, org\_id\)
* org\_id：Required, Fill in Organization No \(Just choose one between org\_no, org\_name, org\_id\)
* position：Required, job title or power and responsibility name, the actual name can refer to "Job, Power and Responsibility Name Query".

API Response example：

```text
{
    "status": 200,
    "message": "查詢成功。",
    "result": {
        "user_ad_no": "",
        "username": "",
        "org_no": ""
    }
}
```

## Where to get Job, Responsibility Name

Reference Organization Chart

![Location: Main Menu&amp;gt;Staff Management&amp;gt;Group Tree Management&amp;gt;Organization&amp;gt;Postion \(Suitcase Icon\)](../.gitbook/assets/image%20%2856%29.png)

![Click the &quot;gear&quot; icon on the job, you can see the job title and the name of the responsibility](../.gitbook/assets/image%20%288%29.png)

Reference Position Management

![Location: Main Menu&amp;gt; Staff Management&amp;gt; Position Management](../.gitbook/assets/image%20%2812%29.png)

![Click the &quot;Edit&quot; button for any position, you can see the name of the responsibilities included](../.gitbook/assets/image%20%2861%29.png)

## Organization chart export

Export the organization chart component structure in Json format:

* Method：POST
* URL：/rest/organization/api/organization/load/
* postbody:

{% hint style="info" %}
All apis must obtain a security code \(security\) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method
{% endhint %}

```text
{
    "security" : "<security_code>",
    "omflow_restapi" : 1
}
```

* secuity：Required
* omflow\_restapi：Required, Fill in 1.

API Response example：

```text
{
    "status": 200,
    "message": "讀取成功。",
    "result": {
        "value": [<org_obj>,<org_obj>,...],
        "status": False,
        "org_approver": {
             "group" : <org_group>,
             "user" : <org_user>
         }
    }
}
```

