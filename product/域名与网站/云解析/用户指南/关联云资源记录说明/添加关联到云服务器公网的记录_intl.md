Usually, when you need to set up a public subdomain name for a group of CVM instances, you can do so easily with Tencent Cloud DNS. Below is an example.

Suppose that you have added the domain name qcloud-example.com (this is for demonstration only and should be replaced with a real domain name successfully added during actual operations) with the goal to set a public subdomain name `www.qcloud-example.com` for a set of CVM.

### Clicking Add Record on the Record Management Page
![](//mc.qcloudimg.com/static/img/946e83baba710ad61e51263551870afd/image.png)
### Selecting the CVM Resources Associated with the A Record
In the **Add record** pop-up, enter www for the **Host** field (the www in `www.qcloud-example.com` is called the host), select "A" for "Record type" and select **Associate cloud resources**. The pop-up window will then list all the CVM instances with public IPs you have purchased. Select a group of instances and click **OK** to submit. The newly added record will appear in the record list, and the line type of the subdomain name is default, as shown in the figure below.
![](//mc.qcloudimg.com/static/img/9fa144ec34bea93527d22b1555d108a0/image.png)
![](//mc.qcloudimg.com/static/img/b3db9a0a7a8b3c0b3e28a3ada5c4b371/image.png)
![](//mc.qcloudimg.com/static/img/2f4c31232aef6185e03bf0c8121fce6f/image.png)
### Testing
Now you can try accessing `www.qcloud-example.com` or execute the command "dig www.qcloud-example.com -t A". If the returned result includes the public IPs of 123.207.67.60 and 123.207.43.183, it means that the resolution of the record works well.
