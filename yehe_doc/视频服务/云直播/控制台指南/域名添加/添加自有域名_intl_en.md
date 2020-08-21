To use LVB, you should have at least **two** domain names, one as the push domain name, and the other as the playback domain name. Push and playback cannot use the same domain name.



## Prerequisites
1. You have activated the [LVB](https://intl.cloud.tencent.com/product/LVB) service.
2. You have prepared your own domain names and obtained ICP filings for their service in Mainland China.
	- If your domain names have not obtained an ICP filing, you can go to Tencent Cloud Website ICP Filing Service to apply for ICP filing.

>- You should apply for ICP filing for your domain names according to the regulations of the Ministry of Industry and Information Technology (MIIT) of China. The application process takes several business days to complete, so you are recommended to start an application in advance. For more information, please see [Domain Name ICP Filing and Configuration](https://intl.cloud.tencent.com/document/product/267/32478).
>- The time needed to complete an ICP filing application depends on your domain name service provider. If you have received a notification from MIIT that your domain name has been filed on record, please wait for 1 to 24 hours. After your domain name can be found on [MIIT's ICP filing query website](http://www.beian.miit.gov.cn), it can be added to the LVB Console.
>- A new ICP filing can be synced to Tencent Cloud servers in one business day; therefore, a newly filed domain name may appear to be not filed when it is added.


## Directions
### Step 1. Add you own domain name
1. Log in to the [LVB Console](https://console.cloud.tencent.com/live) and select **Domain Management**.
2. Click **Add Domain** to enter the domain name adding page and configure as follows:
	1. To add a **push domain**, enter the domain name, select its type as **Push domain**, and click **OK**.
	2. To add a **playback domain**, enter the domain name, select its type as **Playback domain**, select an acceleration region (**Mainland China** by default), and click **OK**.

![](https://main.qcloudimg.com/raw/a602d5953a0c0fcfd66ba8801c0266b3.png)
> 
>- The domain name can be up to**29** bits in length and cannot contain uppercase letters.
>- After your own domain names are added successfully, you can click the domain name to be modified or **Manage** on the right in the domain management list to enter the domain name details page, select **Advanced Configuration** to view the **Region Configuration** tab, click **Edit** to enter the region configuration modification page, select a new acceleration region, and click **Save**.

### Step 2. Configure the CNAME record of the domain name
Once your domain name is added, the system will automatically assign it a CNAME domain name (suffixed with `.liveplay.myqcloud.com`), which cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, LVB can be used properly. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057).

> If you need to manage it, please see [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056).

## FAQs
- [What are the requirements for a playback domain name in LVB?](https://intl.cloud.tencent.com/document/product/267/7968)
- [Can the playback and push domain names in LVB be the same? Can I use second-level domain names for them?](https://intl.cloud.tencent.com/document/product/267/7968)
