# Set up PyPI server

The code components in the OMFlow process can execute python code. Users can find useful sample programs or packages on the Internet and in the community to construct their own processes. At this time, there will be a need to install the python package separately, and then how to install the python package will be explained.

When the server has an external network, the installation of the package can be done directly through omflow. The user only needs to fill in the package name of the package to be installed on the package tab of the python component in the process (for details, please refer to the component introduction).

The system will check whether the package has been installed, and if it has not been installed, it will automatically install the package for the user. If the server does not have an external network, the user needs to set up a server at this time. The following will explain how to create a PyPI server.

## Set up a server

Requirement：python、pip

The most basic of setting up a server is that python must be installed in the environment. How to install python, set environment variables, etc., please go to the official python website to browse, I won’t go into details here.

### Step 1、install package

If the server environment has an external network, open the command prompt and type the following command

```
pip install devpi-server
pip install devpi-client
```

If there is no external network, please obtain the package in an environment with external network. You can directly search for devpi by google and download the package:

{% embed url="https://pypi.org/project/devpi-server/#files" %}

{% embed url="https://pypi.org/project/devpi-client/#files" %}

{% hint style="info" %}
To meet the teaching situation, please download the .whl file.
{% endhint %}

Or download through the python command, the command is as follows:

```
pip download devpi-server -d <download path>
pip download devpi-client -d <download path>
```

Then move the downloaded whl file to the server environment, open the command prompt again and type the following command:

```
pip install <devpi-server.whl>
pip install <devpi-client.whl>
```

### Step 2、initialize devpi server

After the devpi package is installed, the initial settings of the server must be performed. The command is as follows:

```
devpi-init --serverdir="/devpi"
```

{% hint style="info" %}
\--serverdir="" the following path represents the location of the server and can be adjusted by yourself.
{% endhint %}

### Step 3、active PyPI server

After creating an account, you can start the server, the command is as follows:

```
devpi-server --serverdir="/devpi" --restrict-modify=root --port=3141 --host=<IP位置>
```

{% hint style="info" %}
\--port=3141 is the default value and can be modified by yourself.

\--host=Please fill in the ip of the current setup environment.
{% endhint %}

{% hint style="warning" %}
If the environment where the server is set up has an external network, please skip to the step 5 after completing this step.
{% endhint %}

### Step 4、client

When there is no external network, the user can only download the package separately, and finally upload it to the server for unified management. At this time, the client package is needed. The setting command is as follows:

```
#Set the server location pointed to by the client
devpi use http://<IP>:<Port>
```

{% hint style="info" %}
Both ip and port are the positions set in step 3.
{% endhint %}

```
#login
devpi login root --password=<password>

#Create your own folder under the root user
devpi index -c local
```

{% hint style="info" %}
"local" can be changed.
{% endhint %}

```
#Switch to the local folder just created
devpi use root/local

#Upload the downloaded package to the PyPI server
devpi upload --from-dir <whl file path>
```

At this point, the pypi server setup is complete.

### Step 5、config omflow server

After setting up the server, you must go to the omflow setting, so when the application is put on the shelf, the system will download the installation package to the pypi server according to this setting.

Log in to omflow> System Settings> System Settings

![](../.gitbook/assets/pip-server.png)

After filling in the location of the server, the save will take effect.

{% hint style="info" %}
If the pypi server has an external network, an example of the path location to fill in:

http://\<IP>:3141/root/pypi/+simple/
{% endhint %}

{% hint style="info" %}
If there is no external network, the example of the path location to fill in:

http://\<IP>:3141/root/local/
{% endhint %}
