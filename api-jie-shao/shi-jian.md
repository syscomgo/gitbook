---
description: this is translated by machine
---

# Event

## Create Event

When an abnormal situation occurs, this API can be called to generate an event.

* Method：POST
* URL：/rest/monitor/api/event/create/
* Post body：

```text
{
  "security": "",
  "title": "",
  "content": "",
  "severity": "1-5>",
  "omflow_restapi": 1,
  "source2": ""
}
```

The above post body is the basis for the content to be converted into the event. The severity level is divided into five levels, namely 1 \(Info\), 2 \(Normal\), 3 \(Warning\), 4 \(Major\), 5 \(Critical\), for example, If the severity level is Warning, enter 3 in the severity parameter. In addition, source2 is the index string of the same event of the same device in series, which will be further explained in the next chapter.

{% hint style="info" %}
All apis must obtain a security code \(security\) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method
{% endhint %}

## Close Event

When the abnormal situation is eliminated, you can call this API to close the event, and the system will close all events that match the specified source2 string.

* Method：POST
* URL：/rest/monitor/api/event/close/
* Post body：如下

```text
{
  "security": "",
  "omflow_restapi": 1,
  "source2": ""
}
```

{% hint style="info" %}
All apis must obtain a security code \(security\) before using it, please refer to [Security](an-quan-ma.md) for the obtaining method
{% endhint %}

## System

In addition to the use of the event API on this website, there are also instructions on the system. You can go to the main menu&gt;data collection&gt;event management to view it on the "event API" tab, as shown in the figure below:

![](../.gitbook/assets/image%20%2849%29.png)



