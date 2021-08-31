## Overview
This document describes how to enable services at startup for auto scale-out CVMs by modifying the `/etc/rc.d/rc.local` file. Manual intervention is not expected throughout the scale-out process where auto scaling is used. Therefore, we recommend that you set the service to be started upon starting of the CVM to be automatically added. Such services include:
- **httpd** service
- **mysqld** service
- **php-fpm** service
- **tomcat** service
- Other services

## Directions
### Setting the services to be launched at startup
>!This document uses the scale-out CentOS CVMs as an example.
>
1. [Log in to a Linux instance using the standard login method (recommended)](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to open the `rc.local` file.
```
vim /etc/rc.d/rc.local
```
3. Press **i** to enter the edit mode, and then press **↓** to go to the end of the file.
4. Append the following content to the file to set services to be automatically started. This example shows how to set the httpd, mysqld, and php-fpm services to be automatically started. Note that the required services vary by website, set them as needed.
```
service httpd start
service mysqld start
service php-fpm start
```
The result should be as follows:
![](https://main.qcloudimg.com/raw/910cd7fd40cfce498e68b037430d20ef.png)
5. Press **:wq** to save and exit. Then, the website can be automatically accessed after the instance is restarted.

### (Optional) Verifying the configuration
Restart the server (with the `reboot` command, or through the console). After the server is restarted, refresh the page on the website without logging in to the server to check whether a response is returned. If yes, the configuration was successful.

### Creating images
You can create an image based on the instance and use this image when creating the launch configuration. For more information, see
- [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942)
- [Creating a Launch Configuration](https://intl.cloud.tencent.com/document/product/377/8544)





