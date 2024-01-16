# Upgrade Python & Django

## Windows

### 1. Backup OMFLOW

Disable and back up OMFLOW, please refer to the 'Backup and Restore' section for backup instructions.

### 2. Confirm current Python packages

1. Run the command prompt as "Administrator."
2. Switch to the Python folder of omflow:

```bash
        cd "C:\Program Files\OMFLOW Server\Python"
```

3. List all current packages (please record the package list):

```bash
        python.exe -m pip freeze
```

4. Exit the command prompt from the current directory:

```bash
        cd ..
```

5. Rename the Python folder to "Python\_backup"

### 3. Install a new version of Python

1. Download Python3.x (32 Bit) Windows Installer and run it.
2. Choose Customize installation for a custom installation path.
3. Set the installation path to `C:\PROGRA\~1\OMFLOW Server\Python`

### 4. Install Python packages

> For offline environments, please refer to the following 'Supplementary' section.

1. Switch back to the Python directory in the command prompt:

```bash
        cd "C:\Program Files\OMFLOW Server\Python"
```

2. Start installing the required packages (all packages listed in section 2.3):

```bash
        python.exe -m pip install <package_name>
```

### 5. Modify httpd.conf

Open `C:\Program Files\OMFLOW Server\Apache24\conf\httpd.conf` and modify the following two lines, replacing python37 and mod\_wsgi.cp37 with the new version numbers:

```
        LoadFile "C:\Program Files\OMFLOW Server\Python\python37.dll"
        LoadModule wsgi_module "C:\Program Files\OMFLOW Server\Python\lib\site-packages\mod_wsgi\server\mod_wsgi.cp37-win32.pyd"
```

### 6. Modify custom content

> python 3.7 => 3.11 Django 2.2 => 4.2

The content in this section is an example based on the environment mentioned above. Please refer to the Python or Django official websites for other version-specific modifications.

1. Open `C:\Program Files\OMFLOW Server\omflow\omcustom\urls.py`
2. Delete the following line:

```python
        from django.conf.urls import url
```

3. Modify the following line, changing all url() occurrences to re\_path():

```python
        # Old
        from django.urls import path
        # Change to
        from django.urls import path, re_path
```

4. Save and close the file after making the modifications.

### 7. Restart OMFLOW

Restart the OMFLOW service

## Linux

### 1. Backup OMFLOW

First, back up OMFLOW. Please refer to the 'Backup and Restore' section for backup instructions.

### 2. Stop OMFLOW

```bash
        omflow_server stop
```

### 3. Delete the python folder under /opt/omflow directory

```bash
        rm -rf /opt/omflow/python/
```

### 4. Install Ubuntu packages

> Package list
>
> * python 3.x
> * python3.x-dev
> * python3.x-venv
> * python3-pip

Installation method 1: Online installation (requires an internet connection)

```bash
        # Update package repository
        apt-get update -y
        # Add the 'deadsnakes' repository
        add-apt-repository ppa:deadsnakes/ppa -y
        # Update the package repository
        apt-get update -y

        # Install python3.x and related packages
        apt-get install -y python3.x python3.x-dev python3.x-venv python3-pip
```

Installation method 2: Offline installation (refer to the supplementary section)

> Download the Ubuntu package offline installation package Offline installation of Ubuntu packages

### 5. Set python 3.x as an environment variable (to call python3 with the command python3)

```bash
        update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.x 1
```

### 6. Create a virtual environment for python 3.x under the /opt/omflow directory

```bash
        python3 -m venv /opt/omflow/python
```

### 7. Enter the virtual environment and install python packages

> Python package list
>
> * wheel
> * django==4.2
> * ldap3
> * mod\_wsgi
> * openpyxl
> * Other python packages needed by the DB
> * Other required packages…

Online installation version (requires an internet connection)

```bash
        # Enter the virtual environment
        source /opt/omflow/python/bin/activate

        # Install wheel
        pip install wheel

        # Optional step
        python /usr/lib/python3.11/test/libregrtest/setup.py bdist_wheel

        # Install necessary packages; evaluate other packages for installation
        pip install django==4.2 ldap3 mod_wsgi openpyxl
```

For offline environments, refer to the supplementary section.

> Download python package offline installation package (.whl) Offline installation of python packages

### 8. Modify the path of the wsgi\_module in the apache http.conf to the new path

```bash
        # Modify django.conf
        vim /etc/apache2/sites-enabled/django.conf

        # Modify the path of wsgi_module
```

## Supplementary:

All commands in this chapter are based on python3.11 as an example; please modify for different versions.

### Download Ubuntu package offline installation package

Find an Ubuntu environment identical to the OMFLOW server, with an internet connection.

> Required packages:
>
> * python3.11
> * python3.11-dev
> * python3.11-venv
> * python3-pip

Download command:

```bash
        # Switch to root user
        sudo su
        
        # Add the 'deadsnakes' PPA repository
        add-apt-repository ppa:deadsnakes/ppa
        
        # Update the package list
        apt-get update
        
        # (if needed) Clean the default download folder
        apt-get clean
        
        # Download the packages without installing
        apt-get install --download-only python3.11 python3.11-dev python3.11-venv python3-pip
```

The downloaded installation packages will be saved in the **`/var/cache/apt/archives/`** directory. Retrieve them using an FTP tool and place them in the OMFLOW server environment.

### Offline installation of Ubuntu packages

> Required packages:
>
> * python3.11
> * python3.11-dev
> * python3.11-venv
> * python3-pip

Copy the **`.deb`** files to a directory on Ubuntu, using **`/tmp/Downloads`** as an example.

Ubuntu commands:

```bash
        # Switch to root user
        sudo su
        
        # Move to the directory where the installation packages are located
        cd /tmp/Downloads
        
        # Install the downloaded packages using dpkg
        dpkg -i *.deb
```

The installed packages can be found in the **`/opt/omflow/python`** directory.

### Export the installed python package list from an existing environment

If you already have a list of packages used by the original OMFLOW, you can skip this step.

Reference: [https://pip.pypa.io/en/stable/cli/pip\_freeze/](https://pip.pypa.io/en/stable/cli/pip\_freeze/)

Export command:

```bash
        # Switch to the OMFLOW virtual environment
        source /opt/omflow/python/bin/activate
        
        # Export the python package list to /tmp
        pip freeze > /tmp/requirements.txt
        
        # Change the version of Django to 4.2 or above
        vim /tmp/requirements.txt
```

Retrieve the file using an FTP tool and place it in an Ubuntu environment with an internet connection as a reference for downloading packages later.

### Download python package offline installation package (.whl)

Prepare an environment with python3.11 installed to easily download versions suitable for python3.11. This environment must have internet access.

Download command:

```bash
        # Create a directory to store offline installation packages
        mkdir /tmp/python_package
        cd /tmp/python_package
        
        # [Method 1] Download in batches using requirements.txt
        # If you have already placed requirements.txt in /tmp/
        pip -m install /tmp/requirements.txt
        
        # [Method 2] Manually enter package names for download
        pip -m install <package_name>
        
        # View the number of .whl installation files in the folder after downloading
        ll
```

Retrieve the files using an FTP tool and place them back in the OMFLOW server.

> Note: mod\_wsgi will be in tar.gz format, and its installation is a bit special. Refer to the offline installation of mod\_wsgi.

### Offline installation of python packages

Assuming that the offline installation packages for python (.whl) are located in **`/opt/omflow/tmp`**

Installation command:

```bash
        # Switch to the OMFLOW virtual environment
        source /opt/omflow/python/bin/activate
        
        # Switch to the directory where offline installation packages are located
        cd /opt/omflow/tmp
        
        # Install all .whl files
        pip install *.whl
```

### Offline installation of mod\_wsgi

Installation command:

```bash
        # Switch to the OMFLOW virtual environment
        source /opt/omflow/python/bin/activate
        
        # Extract the mod_wsgi tar.gz file
        tar zxvf <mod_wsgi_file_path>
        
        cd <mod_wsgi_extracted_path>
        
        # Simplified installation of mod_wsgi
        python setup.py install
```

#### Error Handling

If the OMFLOW service fails to start after the update, follow the 'Backup and Restore' section to restore OMFLOW and then re-run the update steps.
