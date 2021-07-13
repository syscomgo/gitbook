# Change data center URL

The server will need to change certificates, ports, domains, IPs, etc. due to various factors including but not limited to organizational changes, device structure changes, server abnormalities, etc. This article mainly explains what needs to be modified. In order for the data center to operate normally.

## Windows

### Modify httpd.conf

_File path: C:\Program Files\OMFLOW Server\Apache24\conf\httpd.conf_

Modify the &lt;IP&gt; and &lt;Port&gt; in the following two settings

```text
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, instead of the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on specific IP addresses as shown below to 
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 12.34.56.78:80
Listen <IP>:<Port>
```

```text
# ServerName gives the name and port that the server uses to identify itself.
# This can often be determined automatically, but we recommend you specify
# it explicitly to prevent problems during startup.
#
# If your host doesn't have a registered DNS name, enter its IP address here.
#
ServerName <IP>:<Port>
```

### Modify settings.py

_File path: C:\Program Files\OMFLOW Server\omflow\omflow\settings.py_

Modify **LOCAL**_\*\*\_**\_**IP **and** LOCAL\_PORT\*\*

```text
#omflow type(server/collector)
OMFLOW_TYPE = "server"
#local info
LOCAL_IP = "127.0.0.1"
LOCAL_PORT = "80"
UNIQUE_ID = ""
LOCAL_PROTOCOL = "http"
```

### Restart Service

![](../.gitbook/assets/zhong-qi-fu-wu-%20%281%29%20%281%29.png)

### Update collector register IP

restart and login OMFLOW

Home &gt; System Setting &gt; System Setting

![](../.gitbook/assets/tong-bu-collector.png)

After the update is completed, all the collectors that have been reported to will modify the reported objects to the new IP.

## Linux

### ubuntu

### Modify django.conf

_File path:_ /etc/apache2/sites-available/django.conf

Modify the &lt;IP&gt; and &lt;Port&gt; in the following two settings

```text
<IfModule mod_ssl.c>
<VirtualHost <IP>:<Port> >
    DocumentRoot /opt/omflow/server

    Alias /static  /opt/omflow/server/staticfiles
```

### Modify settings.py

_File path: /opt/omflow/server/omflow/settings.py_

Modify **LOCAL**_\*\*\_**\_**IP **and** LOCAL\_PORT\*\*

```text
#omflow type(server/collector)
OMFLOW_TYPE = "server"
#local info
LOCAL_IP = "<IP>"
LOCAL_PORT = "<Port>"
LOCAL_PROTOCOL = "http"
```

### Restart service

```text
systemctl stop omflow_server
systemctl start omflow_server
```

### Update collector register IP

Restart and login OMFLOW

Home &gt; System Setting &gt; System Setting

![](../.gitbook/assets/tong-bu-collector.png)

After the update is completed, all the collectors that have been reported to will modify the reported objects to the new IP.

### centos

### Modify httpd.conf

_File path: /etc/httpd/conf/httpd.conf_

Modify the &lt;IP&gt; and &lt;Port&gt; in the following setting.

```text
# Change this to Listen on specific IP addresses as shown below to 
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 12.34.56.78:80
Listen <IP>:<Port>
```

### Modify django.conf

_File path:_ /etc/httpd/conf.d/django.conf

Modify the &lt;IP&gt; and &lt;Port&gt; in the following setting.

```text
<IfModule mod_ssl.c>
<VirtualHost <IP>:<Port> >
    DocumentRoot /opt/omflow/server

    Alias /static  /opt/omflow/server/staticfiles
```

### Modify settings.py

_File path: /opt/omflow/server/omflow/settings.py_

Modify **LOCAL**_\*\*\_**\_**IP **and** LOCAL\_PORT\*\*

```text
#omflow type(server/collector)
OMFLOW_TYPE = "server"
#local info
LOCAL_IP = "<IP>"
LOCAL_PORT = "<Port>"
LOCAL_PROTOCOL = "http"
```

### Restart Service

```text
systemctl stop omflow_server
systemctl start omflow_server
```

### Update collector register IP

Restart and login OMFLOW

Home &gt; System Setting &gt; System Setting

![](../.gitbook/assets/tong-bu-collector.png)

After the update is completed, all the collectors that have been reported to will modify the reported objects to the new IP.

