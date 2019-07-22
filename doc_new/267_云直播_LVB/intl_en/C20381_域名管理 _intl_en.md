![](https://main.qcloudimg.com/raw/8be06ffb4bec3c5eacb6af233d19fdf2.png)

### Step 1. Apply for an ICP filing for a domain name

You need to apply for an ICP filing for your domain name before submitting it to the console for management. 

>The time it takes to complete an ICP filing application depends on your domain name service provider. If you have received a notification from the Ministry of Industry and Information Technology (MIIT) that your application has been completed, please wait patiently for 1 to 24 hours. After your filed domain name can be found at the [MIIT's ICP filing query website](http://www.beian.miit.gov.cn), it can be added to the LVB Console.

### Step 2. Add a domain name

Select **Domain Name Management** in the left sidebar in the LVB Console to enter the domain name management page, where you can view the created domain names and their type, status, and added time and perform desired operations.
The types of domain names that can be added and managed include playback domain names and push domain names.
![](https://main.qcloudimg.com/raw/041d511b12a5b4eb1abe5c35116e3f12.png)


- **Add a playback domain name**
Click **Add a Domain Name**, enter the domain name, select its type as **Playback domain name**, and click **Submit**.
>The domain name can contain up to 29 characters and cannot contain uppercase letters.
>
![](https://main.qcloudimg.com/raw/16037f1c0aa5db8b5f93b550307ffc69.png)

- **Add a push domain name**
Click **Add a Domain Name**, enter the domain name, select its type as **Push domain name**, and click **Submit**.
>The domain name can contain up to 29 characters and cannot contain uppercase letters.
>
![](https://main.qcloudimg.com/raw/96c374036b96bf8bae3337c232f0f3d2.png)

After you add a playback domain name, if an error is displayed stating that no CNAME record has been configured, please configure one as instructed in [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057).
![](https://main.qcloudimg.com/raw/f759db973bb8b6403facee964d3511aa.png)



### Step 3. View and configure information
- **Configure a playback domain name**
Click **Manage** to view the basic information and playback settings of the domain name.
![](https://main.qcloudimg.com/raw/dc6ac37c931bf98b1a2f39e61b6949d0.png)
Click **Playback Configuration** to view the playback addresses in RTMP, FLV, and HLS formats.
![](https://main.qcloudimg.com/raw/6e3b2cfa52b166db46931293c107daab.png)

- **Configure a push domain name**
Click **Manage** to view the basic information and push settings of the domain name.
![](https://main.qcloudimg.com/raw/946e39a65dad84e978bd3200068ce2ef.png)

Click **Push Configuration** > **Generate a Push Address** and a push address will be displayed in the "Push Address" section.
> StreamName (stream ID) can contain only letters, numbers, and symbols.

You can view the PHP and Java sample code for a push address at the bottom of the page:
![](https://main.qcloudimg.com/raw/7d96140eb1e256b364e8003b2ffa5fdf.png)


### Step 4. Disable, enable, or delete a domain name
Once disabled, a domain name cannot be accessed. It can be accessed again once enabled. The operating steps are the same for both playback and push domain names.

- **Disable a domain name**
On the domain name management page, click **Disable** to the right of the domain name to be disabled and click **OK** in the pop-up window.
![](https://main.qcloudimg.com/raw/6518debbdad6e10210a76917de24001b.png)


- **Enable a domain name**
On the domain name management page, click **Enable** to the right of the domain name to be enabled.
![](https://main.qcloudimg.com/raw/46038b6e486050fb8b86b071d14c489a.png)

- **Delete a domain name**
On the domain name management page, click **Delete** to the right of the domain name to be deleted.
![](https://main.qcloudimg.com/raw/8629b7c4687fde07d3cd63f0e85a546b.png)

