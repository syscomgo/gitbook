# Booster

## Features

### Load balancing architecture

When the user needs to bill a large number of bills for a long time or many users go online at the same time and other extremely performance-consuming situations occur, which makes it difficult for a single OMFLOW Server to load. OMFLOW also provides a load balancing mechanism. Multiple OMFLOW Servers can be built at the same time to distribute performance, and Booster can coordinate deployment to improve overall efficiency. The architecture diagram is as follows:

![](<../.gitbook/assets/OMFLOW架構 (2).png>)

### Load balancing and high availability architecture

At the same time, OMFLOW also provides a high-availability architecture. The Booster is divided into two "master and slave". All OMFLOW Servers will report to the Booster in this order to ensure that the system can still operate normally when any node of this architecture loses contact.

![](../.gitbook/assets/HA架構.png)

#### OMFLOW Booster

Acting as the data transfer center, it is mainly responsible for cooperating with all OMFLOW Servers to jointly process the form process. Normally, the main Booster will do the work. When the primary Booster loses contact, the secondary Booster will take over to form a high-availability architecture.

#### OMFLOW Booster Agent

When using the Booster architecture, the Booster Agent needs to be installed on the same environment as the OMFLOW Server. Its function is that when any OMFLOW Server updates the Patch, all other OMFLOW Servers will also be automatically updated.

## Installation Steps

### 1. Environmental requirements

**Booster server**: recommended at least 4 core 8 GB for installing OMFLOWBooster&#x20;

**Python**: Make sure that the Python version of Booster and OMFLOWServer is 3.7.7 or above&#x20;

**Port**: Make sure that the port 5169 between Booster and OMFLOWServer is open to each other

### 2. Install OMFLOW Booster

Install the most priority, and install one or two Boosters according to the situation. There is no sequence requirement for the two, and the following information needs to be filled in during installation:

#### Enter the local IP/Domain and Port:

Fill in the IP/Domain and Port represented by this Booster, and ensure that all OMFLOW Servers are connected to this.

{% hint style="info" %}
In addition to Booster, OMFLOW Server also needs to open port 5169.
{% endhint %}

#### Enter HA Booster IP/Domain and Port (optional):

When the scenario is an HA architecture, fill in the IP/Domain and Port represented by another Booster, and ensure that the two Boosters can communicate with each other.

{% hint style="info" %}
Under the HA architecture, one is the primary Booster and the other is the secondary Booster
{% endhint %}

{% hint style="info" %}
How to install Linux&#x20;

Unzip it under the path where the installation package is placed, and enter and execute **install.sh**.
{% endhint %}

```
tar xvf Booster_1140.tar.gz
cd Booster_1140
./install.sh
```

### 3. Build Database

The Booster architecture does not support Sqlite, and the corresponding database needs to be established in advance. The databases supported by OMFLOW are as follows:

* PostgreSQL
* MySQL
* SQL Server
* Oracle
* DBMaker

{% hint style="info" %}
Prepare the database and an account with permissions to create tables and read and write the database
{% endhint %}



### 4. Install OMFLOW Server

After the Booster is installed, install the first OMFLOW Server of this architecture. The installation process will require the following additional information:

#### Enter DB related information:

Please enter the information about the database prepared in [step 2](booster.md#2.-jian-zhi-zi-liao-ku).

#### Enter Booster IP and Port:

Please enter the relevant information to be considered as the main Booster.

#### Enter HA Booster IP and Port:

Please enter the relevant information to be regarded as a secondary Booster.

#### If OMFLOW Server was previously installed:

If there is already a running OMFLOWServer before installing Booster, follow the steps below:

{% hint style="warning" %}
Please back up your database before installation.
{% endhint %}

{% hint style="warning" %}
Make sure the running OMFLOW Server database is not Sqlite
{% endhint %}

1. Update OMFLOW Server to the latest version
2. Modify the setting.py file and fill in the Booster related information into the four parameters BOOSTER\_IP, BOOSTER\_PORT, SECOND\_BOOSTER\_IP, SECOND\_BOOSTER\_PORT
3. Restart OMFLOW Server

### 5. Install OMFLOW Booster Agent

After the first OMFLOW Server is installed, continue to install OMFLOW Booster Agent on the same environment.

{% hint style="info" %}
BoosterAgent needs to be installed on the same server as OMFLOWServer.
{% endhint %}

{% hint style="info" %}
How to install Linux&#x20;

Unzip it under the path where the installation package is placed, and enter and execute **install.sh**.
{% endhint %}

```
tar xvf BoosterAgent_1140.tar.gz
cd BoosterAgent_1140
./install.sh
```

### 6. Install OMFLOW Slave

{% hint style="warning" %}
lease backup the following before installation:

1. Database for step 3
2. OMFLOW Server of step 4
{% endhint %}

After the above steps are completed, the last step is to install more than one OMFLOWSlave according to the needs of the situation. OMFLOWSlave already contains OMFLOW Server and OMFLOWBooster Agent, the installation process will need to fill in the following additional information:

#### Enter Booster IP and Port:

Please enter the relevant information to be considered as the main Booster.

#### Enter HA Booster IP and Port (optional):

Please enter the relevant information to be regarded as a secondary Booster.

{% hint style="info" %}
Windows installation

There is an independent installation file **omflow\_slave\_1\_1\_X\_X.exe** to provide execution.
{% endhint %}

{% hint style="info" %}
Linux installation

The installation method is the same as [Server](2.md#kai-shi-an-zhuang-omflow-server), only need to input the type into "**Slave**".
{% endhint %}

## Boot Sequence

In the startup sequence, Booster and DB are the highest priority, and then start all Booster Agents.

1. Booster、Database
2. Booster Agent

{% hint style="info" %}
OMFLOW Server is automatically started when the Booster Agent starts.
{% endhint %}

{% hint style="info" %}
How to start a service in Linux

Booster

```
/opt/omflow/Booster/omflow_booster_service { start | stop | status }
```

BoosterAgent

```
/opt/omflow/BoosterAgent/omflow_booster_agent_service { start | stop | status }
```
{% endhint %}

## Upload License

1. Click "Left Main Menu > System Settings > System Settings"
2. Drag to the bottom of the main screen to find the "Booster Authorization Information" block.
3. Click the "Upload" button to upload the license file

{% hint style="info" %}
Booster still has a trial period of 7 days without uploading the license.
{% endhint %}

