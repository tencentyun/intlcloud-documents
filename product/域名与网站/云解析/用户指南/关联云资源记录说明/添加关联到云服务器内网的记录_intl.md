Do you often add records to /etc/hosts in CVM to configure private domain names for other CVM instances so that you can easily access those instances on the private network? Are you bothered by the task of configuring hosts which is both cumbersome and inconvenient to manage?

Tencent Cloud DNS helps you eliminate those troubles. By setting up records associated with the private network of CVM, you can easily configure the domain names for a group of CVM instances on the private network. Below is an example.

You have added the domain name qcloud-example.com in Tencent Cloud DNS (this is for demonstration only and should be replaced with a real domain name successfully added during actual operations) with the goal to add a private subdomain name "internal.qcloud-example.com" to qcloud-example.com and make it point to a set of selected private IPs of CVM.

### Clicking Add Record on the Record Management Page
![](//mc.qcloudimg.com/static/img/946e83baba710ad61e51263551870afd/image.png)
### Selecting the CVM Resources Associated with the A Record
In the "Add record" pop-up, select "A" for **Record type** and "Yes" for **Associate cloud resources** and enter **internal** for **Host**. The pop-up window will then list all the CVM instances you have purchased. Select a group of instances and click **OK** to submit. The newly added record will appear in the record list, and the subdomain name is only resolved on the private network, as shown in the figure below.
![](//mc.qcloudimg.com/static/img/2a807321f1e64bdd40555269d3cec389/image.png)
![](//mc.qcloudimg.com/static/img/d9f61a3464e523a44ed17be17b386d29/image.png)
![](//mc.qcloudimg.com/static/img/310e795ca0d0136397357c7a97888c8b/image.png)
### Testing
Now, log in to any of your CVM instances and try accessing internal.qcloud-example.com. You can also execute the command "dig internal.qcloud-example.com -t A" on any instance. If the result includes two private IPs of 10.104.117.138 and 10.104.125.171, it means that the resolution of the private subdomain name works well.
