## Overview

Linux, Apache, MySQL, PHP (LAMP) is an internationally popular web application framework. It encompasses the Linux OS, Apache web server, MySQL/MariaDB database, PHP environment, and related components.

<dx-alert infotype="explain" title="">
The LAMP application image is based on CentOS 7.6 64-bit.
</dx-alert>



## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse).
![](https://qcloudimg.tencent-cloud.cn/raw/0a3adf01ba4390699c76b6522fc7f097.png)
 - **Region**: Select a region near your target users to reduce the network latency and improve their access speed.
 - **Availability zone**: **Randomly assigned** is selected by default. You can select one as well.
 - **Image**: Select the **LAMP 7.4.16** application image.
 - **Instance bundle**: Select an instance bundle according to the required instance configuration (including CPU, memory, system disk, bandwidth, and monthly traffic).
 - **Instance name**: Enter a custom instance name. If it is left empty, the selected image name will be used as the name by default. When multiple instances are created in a batch, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and create three instances, the three instances are named "LH1", "LH2", and "LH3".
 - **Purchase period**: Default to **1 month**.
 - **Quantity**: Default to **1**.
3. Click **Buy now** to submit your order and make the payment as prompted.

## Relevant Operations
### Viewing LAMP configuration items
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse).
2. In the instance list, select the target instance created with the LAMP application image to enter its details page.
3. Select the **Pre-installed application** tab to enter the application details page.
![](https://qcloudimg.tencent-cloud.cn/raw/b497c304a862b74a762bbbe671a05d22.png)
You can view the configuration items of the LAMP application.
 - Apache's homepage address and website root directory.
 - MariaDB's admin account (root) and password, database address, and database name.
<dx-alert infotype="explain" title="">
You can get the admin password by logging in to the instance via webshell and running the `cat ~lighthouse/credentials.txt` command.
</dx-alert>
 - Apache, MariaDB, and PHP software installation paths on CentOS.
<dx-alert infotype="explain" title="">
Access `http://LAMP instance public IP/phpinfo.php` to view the PHP configuration information.
</dx-alert>



### Enabling HTTPS access
Install the SSL certificate and enable HTTPS access for your LAMP instance as instructed in [Apache Server Certificate Installation](https://intl.cloud.tencent.com/document/product/1103/47407).
