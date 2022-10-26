# Change data center URL

The server will need to change certificates, ports, domains, IPs, etc. due to various factors including but not limited to organizational changes, device structure changes, server abnormalities, etc. This article mainly explains what needs to be modified. In order for the data center to operate normally.

## Windows

### Modify httpd.conf

_File path: C:\Program Files\OMFLOW Server\Apache24\conf\httpd.conf_

Modify the \<IP> and \<Port> in the following two settings

```
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

```
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

Modify **LOCAL**_\*\*\\_**\_**IP **and** LOCAL\_PORT\*\*

```
#omflow type(server/collector)
OMFLOW_TYPE = "server"
#local info
LOCAL_IP = "127.0.0.1"
LOCAL_PORT = "80"
UNIQUE_ID = ""
LOCAL_PROTOCOL = "http"
```

### Restart Service

```
net stop OMFLOWServer
net start OMFLOWServer
```

### Update collector register IP

_檔案路徑：C:\Program Files\OMFLOW Collector\omflow\omflow\settings.py_

修改 **SERVER\_IP** 以及 **SERVER\_PORT**&#x20;

```
#server info
SERVER_IP = "<IP>"
SERVER_PORT = "<Port>"
SERVER_PROTOCOL = "http"
SECOND_SERVER_IP = ""
SECOND_SERVER_PORT = ""
SECOND_SERVER_PROTOCOL = "http"

```

### Restart Service

```
net stop OMFLOWCollector
net start OMFLOWCollector
```



## Linux

### ubuntu

### Modify django.conf

_File path:_ /etc/apache2/sites-available/django.conf

Modify the \<IP> and \<Port> in the following two settings

```
<IfModule mod_ssl.c>
<VirtualHost <IP>:<Port> >
    DocumentRoot /opt/omflow/server

    Alias /static  /opt/omflow/server/staticfiles
```

### Modify settings.py

_File path: /opt/omflow/server/omflow/settings.py_

Modify **LOCAL**_\*\*\\_**\_**IP **and** LOCAL\_PORT\*\*

```
#omflow type(server/collector)
OMFLOW_TYPE = "server"
#local info
LOCAL_IP = "<IP>"
LOCAL_PORT = "<Port>"
LOCAL_PROTOCOL = "http"
```

### Restart service

```
systemctl stop omflow_server
systemctl start omflow_server
```

### Update collector register IP

_檔案路徑：/opt/omflow/collector/omflow/settings.py_

修改 **SERVER\_IP** 以及 **SERVER\_PORT**&#x20;

```
#server info
SERVER_IP = "<IP>"
SERVER_PORT = "<Port>"
SERVER_PROTOCOL = "http"
SECOND_SERVER_IP = ""
SECOND_SERVER_PORT = ""
SECOND_SERVER_PROTOCOL = "http"

```

### Restart Service

```
systemctl stop omflow_collector
systemctl start omflow_collector
```

### centos

### Modify httpd.conf

_File path: /etc/httpd/conf/httpd.conf_

Modify the \<IP> and \<Port> in the following setting.

```
# Change this to Listen on specific IP addresses as shown below to 
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 12.34.56.78:80
Listen <IP>:<Port>
```

### Modify django.conf

_File path:_ /etc/httpd/conf.d/django.conf

Modify the \<IP> and \<Port> in the following setting.

```
<IfModule mod_ssl.c>
<VirtualHost <IP>:<Port> >
    DocumentRoot /opt/omflow/server

    Alias /static  /opt/omflow/server/staticfiles
```

### Modify settings.py

_File path: /opt/omflow/server/omflow/settings.py_

Modify **LOCAL**_\*\*\\_**\_**IP **and** LOCAL\_PORT\*\*

```
#omflow type(server/collector)
OMFLOW_TYPE = "server"
#local info
LOCAL_IP = "<IP>"
LOCAL_PORT = "<Port>"
LOCAL_PROTOCOL = "http"
```

### Restart Service

```
systemctl stop omflow_server
systemctl start omflow_server
```

### Update collector register IP

_檔案路徑：/opt/omflow/collector/omflow/settings.py_

修改 **SERVER\_IP** 以及 **SERVER\_PORT**&#x20;

```
#server info
SERVER_IP = "<IP>"
SERVER_PORT = "<Port>"
SERVER_PROTOCOL = "http"
SECOND_SERVER_IP = ""
SECOND_SERVER_PORT = ""
SECOND_SERVER_PROTOCOL = "http"

```

### Restart Service

```
systemctl stop omflow_collector
systemctl start omflow_collector
```
