## Overview

Nextcloud is an open-source client and server software application that helps you create a personal online file storage service on your own.

The Nextcloud server is written in PHP and uses the local disk on the server for underlying storage. You can modify the Nextcloud configuration to use COS as the underlying storage, so as to enjoy a higher reliability, more powerful disaster recovery capabilities, and unlimited storage space at lower storage costs.

This document describes the environment on which the Nextcloud server depends, compares and analyzes the differences between local storage and COS, and explains how to build a personal online file storage service.

>! Switching an existing Nextcloud server instance from local storage to COS may render existing files invisible. To change the storage method of an existing instance, we recommend you build a new Nextcloud server, configure COS as the storage, and migrate the data from the old instance to the new one.
>

## Nextcloud Server Environment Overview

The Nextcloud server is written in PHP and can use SQLite, MySQL, MariaDB, or PostgreSQL as the database. Due to the limits in performance, we generally recommend you not use SQLite in your actual business. Although PHP, MySQL, and relevant server software applications support Windows, according to the Nextcloud community, running the Nextcloud server on Windows may cause problems such as garbled text. Therefore, the Nextcloud team has declared that the Nextcloud server cannot be deployed on Windows.

<span id=1></span>
### Server configuration

Cloud Virtual Machine (CVM) currently provides multiple instance families, with multiple sub-families each. Different instance families have different strengths, such as large memory or high I/O. As Nextcloud is targeted at individual, family, and SME users, it has low requirements for hardware resources, and you can select a Standard model with balanced resources. As for the CVM instance sub-families, the latest ones generally have a higher cost performance, so just select the latest sub-family.

After determining the instance family and sub-family, you need to choose specific vCPU and memory specifications (the private network bandwidth and PPS vary by specification). You can use OPcache for PHP to improve the performance, and the Nextcloud server can use APCu memory cache to further improve the performance, so we recommend you select a large memory.

As you can adjust the CVM instance configuration after purchase, you can first purchase an instance with low specifications such as 1-core and 4 GB MEM and determine whether to upgrade the specifications to improve the performance based on the numbers of users and files as well as CVM monitoring data after your online file storage service is built and launched to the production environment. If you need to use the service in a multi-user scenario such as family or SME, we recommend you purchase a 2-core 8 GB MEM or 4-core 16 GB MEM instance to offer a sufficient performance.

### Server operating system

All mainstream Linux distributions can well sustain the Nextcloud server. Their configurations are basically the same except for the command (i.e., package management tool) used for software package installation.

>? This document takes a CVM instance on CentOS 7.7 as an example.
>

### Databases

As mentioned above, MySQL is generally used together with PHP in the actual business. As MariaDB is a fork from MySQL and highly compatible with MySQL, the Nextcloud server can run well with MySQL 5.7+ or MariaDB 10.2+.

Tencent Cloud offers TencentDB for MySQL and TencentDB for MariaDB. Both services adopt a source-replica high-availability architecture and have a higher reliability compared with self-built databases in CVM. In addition, they support easy-to-use Ops features like automatic backup. Therefore, we strongly recommend you use TencentDB in your actual business.

>? This document takes a TencentDB for MySQL 5.7 instance as an example.
>

### Web server and PHP runtime

Some Nextcloud server configurations are specified in `.htaccess` files, so you can directly use Nextcloud's built-in configuration items when using the Apache server software application. Nginx is a web server software application developing rapidly in recent years and features ease of installation and configuration, less resource usage, and higher load capacity compared with Apache. You can transcript `.htaccess` configurations on the Nextcloud server to Nginx configurations to better sustain the Nextcloud server. This document uses the Nginx server software application and provides a complete Nginx configuration example for reference.

The PHP runtime has been upgraded to PHP 7, and the main maintained versions include 7.2, 7.3, and 7.4, all of which support the Nextcloud server. Here, use the latest version 7.4. Moreover, Nextcloud depends on certain PHP modules. The requirements for specific modules are as detailed below.

### Tencent Cloud network environment

Currently, Tencent Cloud offers the classic network and VPC environments. The classic network is a public network resource pool shared by all Tencent Cloud users, where the private IPs of all CVM instances are assigned by Tencent Cloud and you cannot customize IP ranges or IP addresses. A VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies. Currently, as the classic network resources are insufficient and cannot be expanded, the classic network is no longer supported for new accounts and in some new AZs. Therefore, this document takes a VPC as an example.

>? For more information on VPC, see [Overview](https://intl.cloud.tencent.com/document/product/215/535).
>

## Comparison Between CBS and COS

Cloud Block Storage (CBS) disks are mounted to the operating system as local disks on CVM instances. As Nextcloud uses the file system to store the online file storage data by default, you can directly store Nextcloud data to CBS disks on the operating system. Compared with CBS, COS offers the following benefits:

### Use cases

#### CBS

CBS is a type of block storage and can be directly mounted to the CVM operating system as disks. Generally, a CBS disk is used exclusively by the operating system and can be mounted to only one CVM instance. However, it has a high read/write performance and is suitable for scenarios where a high I/O and a low latency are required and it is used by only one CVM instance exclusively.

#### COS

COS opens up its read/write APIs over the HTTP protocol, so you need to access the objects (files) stored in COS through programming. It uses object keys (like file paths) as indexes and have an unlimited storage capacity. As its data is transferred over the network, COS has a lower speed and higher latency. However, as operations are performed on objects, after an application manipulates an object, another application can immediately manipulate the same object. In conclusion, COS is suitable for scenarios where a high performance is not required but a large cost-effective storage capacity or shared access is needed. It is more suitable to use the online file storage application together with COS for the following reasons: the online file storage application transfers data over the network and doesn't require a low latency; the speed and latency on the linkage from the online file storage client to server and then to COS are mainly subject to the client network; COS doesn't limit its own speed.



### Maintenance

#### CBS

CBS has a fixed capacity, which can be expanded in the console or via TencentCloud API. After expansion, you need to add partitions on the operating system, and partition exceptions may occur, which incur certain maintenance costs.

#### COS

COS is used on demand and doesn't limit the total capacity or the number of objects (files), so it requires no maintenance at all.

### Data security

Both CBS and COS use methods such as multi-copy to guarantee the data reliability.

## Building the Nextcloud Server Runtime Environment

### Preparing Tencent Cloud products on which the Nextcloud server depends

#### CVM
To get started with CVM, see [Custom Configurations](https://intl.cloud.tencent.com/document/product/213/8036).


#### TencentDB for MySQL

To get started with TencentDB for MySQL, see [Creating MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37785).


#### COS

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) (you need to activate COS first if you use it for the first time), go to the **Bucket List** page, click **Create Bucket**, and configure as follows:
<table>
	<tr><th>Configuration Item</th><th>Value</th></tr>
	<tr><td>Name</td><td>Enter a custom bucket name such as `nextcloud`. Note that the name cannot be changed once confirmed.</td></tr>
	<tr><td>Region</td><td>Select the region of the CVM instance.</td></tr>
	<tr><td>Other</td><td>Keep the default settings.</td></tr>
</table>
2. After setting the above configuration items, click **OK**.

### Installing and configuring the web server and PHP runtime

#### Installing Nginx

1. Use an SSH tool to log in to the newly purchased server.
2. Run the following command to install Nginx:
```bash
yum install nginx
```
 If the following information is displayed, press `Y` and `Enter` to confirm the installation (repeat the same operation for similar information).
```bash
Is this ok [y/d/N]:
```
3. If the following information is displayed, the installation is completed:
```bash
Complete!
[root@VM-0-10-centos ~]#
```
4. Run the following command to check whether the Nginx version can be viewed normally:
```bash
nginx -v
```
 If the following information is displayed, the installation is completed:
```bash
nginx version: nginx/1.16.1
```

#### Installing PHP

1. Use an SSH tool to log in to the newly purchased server.
2. Run the following command to install PHP 7.4:
```bash
yum install epel-release yum-utils
```
3. Run the following commands in sequence:
**Command 1:**
```bash
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
>? If command execution is too slow or stuck for a long time, you can press `Ctrl + C` to cancel the execution and run the command again (same for the following commands).
>
**Command 2:**
```bash
yum-config-manager --enable remi-php74
```
 **Command 3:**
```bash
yum install php php-fpm
```
4. After the installation, run the following command to check whether the PHP version can be viewed normally:
```bash
php -v
```
 If the following information is displayed, the installation is completed:
```bash
PHP 7.4.8 (cli) (built: Jul 9 2020 08:57:23) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
```

#### Installing PHP modules

In addition to the basic part of PHP, Nextcloud also depends on other PHP modules to implement some features. For more information on the modules on which Nextcloud depends, see [Prerequisites for manual installation](https://docs.nextcloud.com/server/19/admin_manual/installation/source_installation.html#prerequisites-for-manual-installation).

In this example, the PHP modules required by Nextcloud are installed. If you want to use other optional features of Nextcloud, find and install the PHP modules depended on by yourself.

1. Use an SSH tool to log in to the newly purchased server.
2. Run the following command to install the PHP modules:
```bash
yum install php-xml php-gd php-mbstring php-mysqlnd php-intl php-zip
```
3. After the installation, run the following command to view the installed PHP modules:
```bash
php -m
```
4. To install another module, simply run `yum install <php-module-name>` again.

#### Uploading and decompressing the Nextcloud server code

1. Download the latest installation package of the Nextcloud server from the [Nextcloud website](https://nextcloud.com/install/#instructions-server) and upload it to the `/var/www/` directory on the server as follows:
 1. Run the `wget` command to directly download the installation package from the server. For example, after entering the `/var/www/` directory, run the following command: `wget https://download.nextcloud.com/server/releases/nextcloud-19.0.1.zip`.
 2. Download the installation package to the local PC and upload it to the `/var/www/` directory through SFTP or SCP.
 3. Download the installation package to the local PC and upload it through lrzsz as follows:
    1. Use an SSH tool to log in to the newly purchased server.
    2. Run `yum install lrzsz` to install lrzsz.
    3. Run `cd /var/www/` to enter the target directory.
    4. Run `rz -bye` and select the Nextcloud server installation package downloaded to the local PC in the SSH tool (the operation varies by tool).
2. Use an SSH tool to log in to the newly purchased server.
3. Run `unzip nextcloud-<version>.zip` to decompress the installation package such as `unzip nextcloud-19.0.1.zip`.

#### Configuring PHP

1. Use an SSH tool to log in to the newly purchased server.
2. Run `vim /etc/php-fpm.d/www.conf` to open the PHP-FPM configuration file and modify the following configuration items (for detailed directions on how to use Vim, see its documentation; you can also modify the configuration file in other ways):
 1. Change `user = apache` to `user = nginx`.
 2. Change `group = apache` to `group = nginx`.
3. After the modification, enter `:wq` to save the file and exit Vim (for detailed directions on how to use Vim, see its documentation).
4. Run the following command to change the directory owner to make PHP compatible with Nginx:
```bash
chown -R nginx:nginx /var/lib/php
```
5. Run the following commands in sequence and start the PHP-FPM service:
**Command 1:**
```bash
systemctl enable php-fpm   # Command 1
```
 **Command 2:**
```bash
systemctl start php-fpm   # Command 2
```

#### Configuring Nginx

1. Use an SSH tool to log in to the newly purchased server.
2. Run the following command to change the website directory owner:
```bash
chown -R nginx:nginx /var/www
```
3. Back up the current Nginx configuration file `/etc/nginx/nginx.conf` as follows:
 1. Run `cp /etc/nginx/nginx.conf ~/nginx.conf.bak` to back up the current configuration file to the `HOME` directory.
 2. Use SFTP or SCP to download the current configuration file to the local PC.
4. Change `/etc/nginx/nginx.conf` to the following content:

```plaintext
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections  1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer"'
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /var/www/nextcloud;

        add_header Referrer-Policy "no-referrer" always;
        add_header X-Content-Type-Options "nosniff" always;
        add_header X-Download-Options "noopen" always;
        add_header X-Frame-Options "SAMEORIGIN" always;
        add_header X-Permitted-Cross-Domain-Policies "none" always;
        add_header X-Robots-Tag "none" always;
        add_header X-XSS-Protection "1; mode=block" always;

        client_max_body_size 512M;
        fastcgi_buffers 64 4K;

        gzip on;
        gzip_vary on;
        gzip_comp_level 4;
        gzip_min_length 256;
        gzip_proxied expired no-cache no-store private no_last_modified no_etag auth;
        gzip_types application/atom+xml application/javascript application/json application/ld+json application/manifest+json application/rss+xml application/vnd.geo+json application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/bmp image/svg+xml image/x-icon text/cache-manifest text/css text/plain text/vcard text/vnd.rim.location.xloc text/vtt text/x-component text/x-cross-domain-policy;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            try_files $uri $uri/ =404;
            index index.php;
        }

        location ~ ^\/(?:build|tests|config|lib|3rdparty|templates|data)\/ {
            deny all;
        }
        location ~ ^\/(?:\.|autotest|occ|issue|indie|db_|console) {
            deny all;
        }

        location ~ ^\/(?:index|remote|public|cron|core\/ajax\/update|status|ocs\/v[12]|updater\/.+|oc[ms]-provider\/.+)\.php(?:$|\/) {
            fastcgi_split_path_info ^(.+?\.php)(\/.*|)$;
            set $path_info $fastcgi_path_info;
            try_files $fastcgi_script_name =404;
            include        fastcgi_params;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            fastcgi_param PATH_INFO $path_info;
            fastcgi_param modHeadersAvailable true;
            fastcgi_pass 127.0.0.1:9000;
            fastcgi_intercept_errors on;
            fastcgi_request_buffering off;
        }

        location ~ ^\/(?:updater|oc[ms]-provider)(?:$|\/) {
            try_files $uri/ =404;
            index index.php;
        }

        location ~ \.(css|js|svg|gif)$ {
            add_header Cache-Control "max-age=15778463";
        }

        location ~ \.woff2?$ {
            add_header Cache-Control "max-age=604800";
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2 default_server;
#        listen       [::]:443 ssl http2 default_server;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        location / {
#        }
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}
```

5. Run the following commands in sequence and start the Nginx service:
**Command 1:**
```bash
systemctl enable nginx
```
 **Command 2:**
```bash
systemctl start nginx
```

## Configuring the Nextcloud Server to Use COS

### Getting COS information

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click the name of the newly created bucket.
![](https://main.qcloudimg.com/raw/13e02915f8c2846d7dfa5f2fec0c355b.png)
3. On the left sidebar, select **Overview** and record the information in **Bucket Name** and **Region** in **Basic Information**.
![](https://main.qcloudimg.com/raw/2aef2ba23a6a32305ad39b4ef10a970c.png)

### Getting the API key

We recommend you use a sub-account key and follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to reduce risks. For information about how to obtain a sub-account key, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).



### Modifying the Nextcloud server configuration file

1. Use a text editor to create the `config.php` file, enter the following content, and modify relevant values according to the comments:
```php
<?php
$CONFIG = array(
  'objectstore' => array(
    'class' => '\\OC\\Files\\ObjectStore\\S3',
    'arguments' => array(
      'bucket' => 'nextcloud-1250000000', // Bucket name
      'autocreate' => false,
      'key'  => 'AKIDxxxxxxxx', // Replace it with your `SecretId`
      'secret' => 'xxxxxxxxxxxx', // Replace it with your `SecretKey`
      'hostname' => 'cos.<Region>.myqcloud.com', // Change `<Region>` to the bucket region such as `ap-shanghai`
      'use_ssl' => true,
    ),
  ),
);
```
 As shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yJvR645_b14a23e2cac3ac988745fcd82fe56e18.png)
2. Save the file and upload it to the `/var/www/nextcloud/config/` directory (keep the filename `config.php`) through SFTP or SCP or by running the `rz -bye` command.
3. Run the following command to change the owner of the configuration file:
```bash
chown nginx:nginx /var/www/nextcloud/config/config.php
```

## Configuring a Domain Name

If you want to use your own domain name but not an IP address to access your Nextcloud server, you can register a domain name, resolve it to your CVM IP address, and get the ICP filing for it as instructed in the documentation of your domain registrar.

As the Nextcloud server will record the domain name or IP address used during installation, we recommend you register, resolve, and get the ICP filing for a domain name before installation and use the domain name to go to the security page of the Nextcloud server.

If you need to change the domain name or IP address after installing the Nextcloud server, you can modify `trusted_domains` in the `/var/www/nextcloud/config/config.php` configuration file on your own as instructed in [Trusted domains](https://docs.nextcloud.com/server/19/admin_manual/installation/installation_wizard.html#trusted-domains).

## Installing the Nextcloud Server

1. Access the Nextcloud server in the browser. Create an admin account and record the admin username and password.
2. Expand **Storage & database** and configure as follows:

<table>
	<tr><th>Configuration Item</th><th>Value</th></tr>
	<tr><td>Data folder</td><td>/var/www/nextcloud/data (keep the default value)</td></tr>
	<tr><td>Configure the database</td><td>MySQL/MariaDB</td></tr>
	<tr><td>Database user</td><td>root</td></tr>
	<tr><td>Database password</td><td>Password of the `root` user entered during TencentDB for MySQL initialization.</td></tr>
	<tr><td>Database name</td><td>nextcloud (or another unused name)</td></tr>
	<tr><td>Database host (`localhost` is displayed by default)</td><td>Private network address of the TencentDB for MySQL instance</td></tr>
</table>


3. Click **Finish setup** and wait for the Nextcloud server to be installed.
4. If an error such as `504 Gateway Timeout` is displayed during installation, you can directly refresh the page and try again.
5. After the installation, log in to the Nextcloud server with the admin account to use Nextcloud on web.

## Nextcloud Server Debugging

### Background job

The Nextcloud server sometimes needs to execute some background jobs like database cleanup when there are no user interactions. As the PHP operation characteristics prevent PHP-based programs from maintaining an independent worker process or thread internally, you need to proactively call the corresponding PHP program externally to execute such background jobs.

The Nextcloud server offers three background job call methods. By default, the browser will initiate an Ajax request to start a server background job to execute it if you log in on the web client. However, this method depends greatly on your login status. If there are no users logged in, such background jobs cannot be executed, so this method is the least reliable.

To solve the problem of low reliability of Ajax-based background job execution, we recommend you use cron on Linux to configure background jobs. cron can accurately control the time when a job is started such as every five minutes (the number of minutes must be an integral multiple of five) or the 10th minute at each o'clock. The customizable time granularities include minute, hour, day of month, month, and day of week and even second and year on certain operating systems. Therefore, this method is highly flexible. For more information on and configuration of cron, see cron documentation.

The following steps describe how to configure cron to support Nextcloud server background jobs:

1. Use an SSH tool to log in to the newly purchased server.
2. Run the following command to install the PHP modules:
```bash
yum install php-posix
```
3. Run the following command to open or create a cron configuration for the `nginx` account:
```bash
crontab -u nginx -e
```
4. The editor used here is Vi/Vim. Press `i` to enter the editing mode and insert the following line:
```plaintext
*/5 * * * * php -f /var/www/nextcloud/cron.php
```
Press `ESC` to exit the editing mode and enter `:wq` to save the file and exit the editor (for detailed directions on how to use Vi/Vim, see its documentation).
In the above configurations, the officially recommended execution frequency of once every five minutes is set. After the background jobs are executed in five minutes, you can open the browser, log in to the Nextcloud server, click the first letter of your username in the top-right corner to enter the **Settings** page, select **Administration** > **Basic Settings** on the left sidebar, and you can see that **Cron** is selected by default in **Background jobs**.


### Memory cache

PHP can use OPcache to improve the performance, and the Nextcloud server also can use the APCu memory cache to further improve the performance. You can configure as follows:

1. Use an SSH tool to log in to the newly purchased server.
2. Run the following command to install the PHP modules:
```bash
yum install php-pecl-apcu
```
3. Run the following commands in sequence to restart Nginx and PHP-FPM:
**Command 1:**
```bash
systemctl restart nginx
```
 **Command 2:**
```bash
systemctl restart php-fpm
```
4. Run `vim /var/www/nextcloud/config/config.php` to open the configuration file of the Nextcloud server, add the line `'memcache.local' => '\OC\Memcache\APCu',` in `$CONFIG = array (`, save the file, and exit the editor.
![](https://main.qcloudimg.com/raw/eaa28e013991aad579cf6abc2a34d9bb.png)
5. If cron is configured to optimize the background jobs, you need to modify the apc configuration in PHP as follows: Run `vim /etc/php.d/40-apcu.ini` to open the PHP APCu configuration file, change `;apc.enable_cli=0` to `apc.enable_cli=1` (note that the semicolon at the beginning needs to be removed), save the file, and exit the editor. If the `/etc/php.d/40-apcu.ini` path doesn't exist, search for and edit the `.ini` configuration file whose name contains `apc` or `apcu` in the `/etc/php.d/` directory.
![](https://main.qcloudimg.com/raw/1c57fe0a2078aa0ca5dd7ba07b23fe86.png)

## Configuring Client Access

Nextcloud provides official desktop sync clients and mobile clients, which can be downloaded from the Nextcloud official website or the app stores of different platforms. When configuring Nextcloud, you need to enter its server address (domain name or IP) and your username and password to log in to and use the client.






