---
title: "Oracle 19 Installation on RHEL 9.xx"
date: 2022-01-19
draft: false
description: "Place Holder"
tags: ["new", "docs"]
series: ["Documentation"]
series_order: 1
---



{{< alert icon="circle-info" cardColor="#00AD32" iconColor="#1d3557" textColor="#000000" >}}
**Note:** This Guide is Production Ready.
{{< /alert >}}



## Prerequisites

### Install required X11 packages
Install X11 packages with following command based on your operating system release and version:

```bash
yum install xorg-x11-xauth -y
```
### Configure X11 forwarding

To enable X11 Forwarding, change the “X11Forwarding” parameter using vi or nano editor to `yes` in the `/etc/ssh/sshd_config` file if either commented out or set to no.

```bash
vi /etc/ssh/sshd_config
```
or 

```bash
nano /etc/ssh/sshd_config
```

You should see similar output as the following:

`X11Forwarding yes`

### Install the Dependencies

```bash
yum install libnsl* -y
```

```bash
yum update -y
```
``` bash title="To check if Development Tools are installed"
yum grouplist
```

```bash title="If Development tools have not been installed"
yum group install "Development Tools"

```


### Create Oracle Groups and add user
```bash
groupadd -g 3001 oinstall
groupadd -g 3002 dba
groupadd -g 3003 oper
useradd -u 3001 -g oinstall -G dba,oper oracle
```

```bash
passwd oracle
```

### Create the required directories
```bash
mkdir -p /u01/app/oracle/product/19.3/db_home
```

### Change Ownership & Access Permissions
```bash
chown -R oracle:oinstall /u01
chmod -R 775 /u01
```

```bash title="Login with Oracle User"
su - oracle
```

```
export CV_ASSUME_DISTID=RHEL8.5
```

### Update the .bash_profile
```title="Using vi editor"
vi .bash_profile
```
```title="Using vi editor"
nano .bash_profile
```

Update the Bash Profile with the following:
```bash
export ORACLE_BASE=/u01/app/oracle
export ORACLE_HOME=/u01/app/oracle/product/19.3/db_home
export CLIENT_HOME=/u01/app/oracle/product/19.3/client
#export ORACLE_SID=CDB
export LD_LIBRARY_PATH=\$ORACLE_HOME/lib:$CLIENT_HOME/lib:/lib:/usr/lib
export CLASSPATH=\$ORACLE_HOME/jlib:\$ORACLE_HOME/rdbms/jlib:$CLIENT_HOME/rdbms/jlib$
export NLS_LANG=american_america.al32utf8
export NLS_DATE_FORMAT="yyyy-mm-dd:hh24:mi:ss"
export PATH=$PATH:$HOME/.local/bin:$ORACLE_HOME/bin:$CLIENT_HOME/bin
```


Copy the Oracle Database Software in `ORACLE_HOME` location and unzip the software and run below cmd
```bash
./runInstaller
```


Oracle 19c DB Software Installation Wizard will appear.


{{< alert icon="fire" cardColor="#e63946" iconColor="#1d3557" textColor="#f1faee" >}}
If you encounter the following error, then run the following command!
{{< /alert >}}

```bash
export CV_ASSUME_DISTID=RHEL8.5
```

![](os_error.png)


![](https://i.imgur.com/hLbY4kt.png)
![](https://i.imgur.com/9xuINtL.png)
![](https://i.imgur.com/7ENP9hM.png)
![](https://i.imgur.com/zZuWJvU.png)
![](https://i.imgur.com/sIBXEQj.png)
![](https://i.imgur.com/Ce16Gfa.png)
![](https://i.imgur.com/FlGhzv7.png)
![](https://i.imgur.com/26mtUOY.png)
![](https://i.imgur.com/YCsy1Kz.png)
![](https://i.imgur.com/d8La3WB.png)





