## Scenario
Yellow dog Updater, Modified (Yum) is the default package manager used in CentOS. It is used to install and update packages from CentOS and 3rd party repositories. Yum offers a centralized interface for software management and a better experience than having to download and install software one by one. Tencent Cloud hosts Yum sources so you can install software without adding sources.

## Directions

### Installing software

1. Log in to your CVM instance using `root`.
2. Run the following command to install software.
> Starting from CentOS 7, MariaDB has become the default database in the YUM source. If you are using CentOS 7 or later, MySQL installed using ‘yum’ will be unusable. You can use the fully compatible MariaDB, or refer to [this article](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7) on how to install an older version of MySQL.
>
```
yum install software_name
``` 
The software you install may need additional software to run. These additional software are called dependencies. Yum automatically search for dependencies and display the results on screen so you can verify whether the software package is suitable.
For example, after you run `yum install PHP` to install PHP, the following is displayed:
![](https://main.qcloudimg.com/raw/18c4a59a3e0e92b0dcafff662d1e3673.png)
4. Enter `y` and press **Enter** to install the software and any dependency it may require.
When the screen displays `Complete`, the installation is complete, as shown in the figure below:
![](https://main.qcloudimg.com/raw/fb2fbd8becd4576f67b47226a82ee033.png)

### Query installed software information

After software installation is complete, you can run different commands to view information.
- Run the following command to view the installation directory of a software package.
```
rpm -ql software name
```
For example, run `rpm -ql php` to view the installation directory of PHP, as shown in the figure below:
![](https://main.qcloudimg.com/raw/fda98060c9f6ba359d7e705de8d336bb.png)
- Run the following command to query the version information of a software package.
```
rpm -q software_name
```
For example, run `rpm -q php` to query the version information of PHP, as shown in the figure below:
![](https://main.qcloudimg.com/raw/35e1ecee46bc55a5d2510dce59360ecc.png)


