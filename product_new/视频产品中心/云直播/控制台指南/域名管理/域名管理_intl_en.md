![](https://main.qcloudimg.com/raw/b8b296e72d182446a11b6cf91bac79c4.svg)

### Step 1. Apply for an ICP filing for a domain name

You need to apply for an ICP filing for your domain name before submitting it to the console for management. For more information, see [Domain Name ICP Filing](https://cloud.tencent.com/product/ba) and [FAQs for Domain Name ICP Filing and Configuration](https://cloud.tencent.com/document/product/267/30010).

>! The time needed to complete an ICP filing depends on your domain name service provider. If you have received a notification from the Ministry of Industry and Information Technology (MIIT) that your domain name has been filed on record, please wait for 1 to 24 hours. After your domain name can be found on [MIIT's ICP filing query website](http://www.beian.miit.gov.cn), it can be added to the LVB Console.

### Step 2. Add a domain name

Select **Manage Domain** in the left sidebar in the LVB Console to enter the domain name management page where you can view the domain names that have been created and their type, status, added time and available options.
There are two types of domain names you can add and manage, playback domain names and push domain names.
![](https://main.qcloudimg.com/raw/dc1bae6af06b7fc09dac4af3f378f420.png)


- **Add a playback domain name**
Click **Add a Domain Name**, enter the domain name, set its type as **Playback domain name**, and click **Submit**.
>! The domain name can contain up to 29 characters and only lowercase letters.
>
![](https://main.qcloudimg.com/raw/6071c0aa2fee29a467c96509f8fce2c9.png)

- **Add a push domain name**
Click **Add a Domain Name**, enter the domain name, set its type as **Push domain name**, and click **Submit**.
>! The domain name can contain up to 29 characters and only lowercase letters.
>
![](https://main.qcloudimg.com/raw/0ae9e626ff819deefca4f7dbc4fa81c5.png)


After you add a playback domain name, if an error is displayed stating that no CNAME record has been configured, please configure one following the instructions in [CNAME Configuration](https://cloud.tencent.com/document/product/267/19908).
![](https://main.qcloudimg.com/raw/911b09bc98388c3c93e0a0433a2c8d08.png)



### Step 3. View and configure information
- **Configure a playback domain name**
Click **Manage** to view the basic information and playback settings of the domain name.
![](https://main.qcloudimg.com/raw/bae2c64b74762252db43a951af1f41f2.png)
Click **Playback Configuration** to view the playback addresses in RTMP, FLV, and HLS formats.
![](https://main.qcloudimg.com/raw/a833ed0a0d21cb0af95c871e6b6f99c9.png)

- **Configure a push domain name**
Click **Manage** to view the basic information and push settings of the domain name.
![](https://main.qcloudimg.com/raw/7ed36f55e5367cb1369c3547f1e6db97.png)

By clicking **Push Configuration** > **Generate a Push Address**, you will be able to see a push address in the "Push Address" section.
>! StreamName (stream ID) can only contain letters, numbers, and symbols.

You can view sample PHP and Java codes for a push address at the bottom of the page:
![](https://main.qcloudimg.com/raw/3ccb6118abc4f4e4ed49d6906a5adf74.png)


### Step 4. Disable, enable, or delete a domain name
Once disabled, a domain name cannot be accessed. It can be accessed again once enabled. The steps are the same for playback and push domain names.

- **Disable a domain name**
On the domain name management page, click **Disable** to the right of the domain name to be disabled and click **OK** in the pop-up window.
![](https://main.qcloudimg.com/raw/07c5ea78118b2cc3d9e08e201f651ca6.png)


- **Enable a domain name**
On the domain name management page, click **Enable** to the right of the domain name to be enabled.
![](https://main.qcloudimg.com/raw/f80ed962c0fbb18e7248d9baaead7da6.png)

- **Delete a domain name**
On the domain name management page, click **Delete** to the right of the domain name to be deleted.
![](https://main.qcloudimg.com/raw/b12dfc80839851784176c5380130296c.png)

