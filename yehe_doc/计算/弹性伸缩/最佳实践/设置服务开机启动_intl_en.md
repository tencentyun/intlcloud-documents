## Setting the Service to Be Launched upon Boot of the Scaled-out CVM
### Use cases
Manual intervention is not expected througout the scale-out process where auto scaling is used. Therefore, we strongly recommend that you set the service to be launched upon boot of the CVM to be automatically scaled out. Such services include:

- **httpd** service
- **mysqld** service
- **php-fpm** service
- **tomcat** service
- Other services

You can complete this configuration within one minute by modifying the /etc/rc.d/rc.local file.

### Configuration method (by using CentOS as an example)


#### Step 1: Open the rc.local file
Run this command:

    vim /etc/rc.d/rc.local

Keep the existing command line unchange and append extra content to the file name.

>> Operation tips for beginners:
>
> Type "i" to enter the insert mode of vim, then press the arrow down button "↓" to go to the end of the file.


#### Step 2: Specify services to launch

This example demonstrates how to set the httpd, mysqld, and php-fpm services to be launched upon boot on the built website. Accordingly, the following code snippets are appended to rc.local:

    service httpd start
    service mysqld start
    service php-fpm start

![](https://mc.qcloudimg.com/static/img/db828b166419cd933e13573c8838a6aa/image.jpg)

Save the changes and exit. Then, these services can be automatically accessed by the website after the server is started. Note that different websites require different services. Set the services in this step based on your requirements.


> Operation tips for beginners:
>
> After entering the preceding code snippets, press Esc and **hold down Shift and press Z twice**(that is, enter ZZ) to exit.


#### Step 3: (Optional) Verify the configuration
Restart the server (by entering reboot or restarting the server in the console). After the server is restarted, refresh the destination page on the website without logging in to the server to check whether a response is returned. If yes, the configuration was successful.

#### Step 4: Create an image based on this CVM and use this image when creating launch configurations
This step is simple and will not be described in detail. If you have any questions about this step, see the following guides:

[Creating a custom image](https://intl.cloud.tencent.com/document/product/213/4942)

[Creating a launch configuration](https://intl.cloud.tencent.com/document/product/377/8544)


