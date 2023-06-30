## Overview
YUM (Yellowdog Updater, Modified) allows you to easily download and install software, and simplifies your installations on a CVM instance, saving you time and efforts. With it, you only need to run the `yum` command to install software in the CentOS environment. Tencent Cloud provides a YUM repository so you can directly install software packages without adding sources.

## Directions

### Installing software
Log in to your CVM instance with the root account and run the following commands to install software according to the operating system of your CVM.

#### CentOS 8 or later versions
1. Run the following command to install software.
```
dnf install [software name]
```
The system will automatically search for the relevant software package and dependencies, and ask for your confirmation.
For example, after you run the `dnf install php` command to install PHP, the following prompt will appear:
![](https://main.qcloudimg.com/raw/ab6cdf18a685debff13c8f978b38d43f.png)
2. Confirm that the software package is correct. Enter `y` and press **Enter** to start the installation.
The `Complete` prompt indicates the installation is completed.

#### CentOS 7 or earlier versions
1. Run the following command to install software.
>! Starting from CentOS 7, MariaDB has become the default database in the YUM repository. If you are using CentOS 7 or later versions, MySQL installed using `yum` will be unusable. You can use the fully compatible MariaDB, or [click here](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7) to learn about how to install an older version of MySQL.
>
```
yum install [software name]
``` 
The system will automatically search for the relevant software package and dependencies, and ask for your confirmation.
For example, after you run the `yum install PHP` command to install PHP, the following prompt will appear:
![](https://main.qcloudimg.com/raw/18c4a59a3e0e92b0dcafff662d1e3673.png)
2. Confirm that the software package is correct. Enter `y` and press **Enter** to start the installation.
The `Complete` prompt indicates the installation is completed.

### Viewing installed software information

After software installation is completed, you can run different commands to view related information.
- View the installation directory of a software package
```
rpm -ql [software name]
```
For example, run `rpm -ql php` to view the installation directory of PHP, as shown in the figure below:
![](https://main.qcloudimg.com/raw/fda98060c9f6ba359d7e705de8d336bb.png)
- View the version of the software package
```
rpm -q
```
For example, run `rpm -q php` to view the version of PHP, as shown in the figure below:
![](https://main.qcloudimg.com/raw/35e1ecee46bc55a5d2510dce59360ecc.png)

