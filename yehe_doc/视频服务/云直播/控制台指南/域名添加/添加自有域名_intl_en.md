To use CSS, you should have at least two domain names, one as the push domain name, and the other as the playback domain name. Push and playback cannot use the same domain name.

## Prerequisites
You have activated the [CSS](https://cloud.tencent.com/product/css) service.


## Directions
[](id:step1)
### Step 1. Add your own domain name
1. Log in to the [CSS console](https://console.cloud.tencent.com/live) and go to the **Domain Management** page.
2. Click **Add Domain** to enter the domain name adding page and configure as follows:
    1. To add a **push domain**, enter the domain name, select its type as **Push Domain**, and click **Confirm**.
    2. To add a **playback domain**, enter the domain name, select its type as **Playback Domain**, select an acceleration region (**Chinese mainland** by default), and click **Confirm**.

![](https://main.qcloudimg.com/raw/a602d5953a0c0fcfd66ba8801c0266b3.png)
>! 
>- The domain name can be up to **29** characters and cannot contain uppercase letters.
>- By default, each account can add up to 100 domain names. To add more, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to increase the upper limit.
>- After adding your own domain name successfully, you can go to the domain name management list, and click the target domain name or **Manage** on the right to enter the domain name details page. Then, select **Advanced Configuration** to view the **Region Configuration** tab, click **Edit** to enter the region configuration page, reselect an acceleration region, and click **Save**.

[](id:step2)
### Step 2. Configure the CNAME record of the domain name
Once your domain name is added, the system will automatically assign to it a CNAME, which ends with `.tlivecdn.com`. The CNAME can be accessed only after you configure it at your domain name service provider. You will be able to use CSS services once the configuration takes effect. For detailed directions, see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).

>? For how to manage added domain names, please see [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056).

## FAQs
- [What are the requirements for a playback domain name in CSS?](https://intl.cloud.tencent.com/document/product/267/7968)
- [Can I use the same domain name for playback and push? Can I use second-level domain names?](https://intl.cloud.tencent.com/document/product/267/7968)
