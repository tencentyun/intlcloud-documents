To use CSS, you must have at least **two** domains, one push domain and one playback domain. You cannot use the same domain for both push and playback.


## Prerequisites
1. You have activated [CSS](https://cloud.tencent.com/product/css).


[](id:step1)
## Adding Your Own Domain
1. Log in to the [CSS console](https://console.cloud.tencent.com/live) and select **Domain Management** on the left sidebar.
2. Click **Add Domain** and complete the following settings in the pop-up window:
    1. To add a **push domain**, select **Push Domain** as the **Type**, enter the domain name, and click **Next**.
    2. To add a **playback domain**, select **Playback Domain** as the **Type**, select an acceleration region (the default is Chinese mainland), enter the domain name, and click **Next**.

![](https://qcloudimg.tencent-cloud.cn/raw/b6687c4c83f8f2fcfd5732f017cc7b13.png)
>! 
>- The domain name can be up to **45** characters long and cannot contain uppercase letters.
>- By default, you can add up to 100 domains under each Tencent Cloud account. If you you need to add more than 100 domains, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to raise the limit.
>- You can change the acceleration region of a domain added. On the **Domain Management** page, click the name of the domain or click **Manage** on the right. Select the **Advanced Configuration** tab, click **Edit** in the **Region configuration** area, select the acceleration region again in the pop-up window, and click **Save**.



## Verifying Your Domain
To make sure that a domain can only be added by its owner, you need to verify your ownership of a domain before you can add it in the CSS console. For example, to add `a.test.com`, you need to verify your ownership of `test.com`. You don’t need to verify again when adding domains with the same parent domain, such as `b.test.com`. You can verify a domain either by adding a DNS record or by uploading an HTML file. If a previously added domain is not verified, when you add a domain with the same parent domain, verification is still required.

[](id:DNS)
### DNS record
You can verify your ownership of a domain by adding a DNS record at your DNS provider. If you use Tencent Cloud’s DNS service, follow the steps below to add a DNS record.
1. Log in to the [DNSPod console](https://console.dnspod.com/).
2. Select **DNS > My Domains** on the left sidebar and click the parent domain of the domain you want to add.
3. On the **Record Management** page, click **Add Record**.
4. Enter the following information:
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Host</td>
<td>Enter “cssauth”.</td>
</tr><tr>
<td>Record Type</td>
<td>Select “TXT”.</td>
</tr><tr>
<td>Record Value</td>
<td>CSS assigns a unique record value for each domain. You can view it in the CSS console when adding your domain.</td>
</tr></tbody></table>

5. Click **Confirm**. The TXT record will take effect in about five minutes.
6. Return to the CSS console, click **Verify now**. If the verification succeeds, you can proceed to the next step.
![](https://qcloudimg.tencent-cloud.cn/raw/2ba35210b6afd68653d32aef998b009c.png)

### HTML file
You can also verify your domain by uploading an HTML file.
1. When asked to verify your domain in the CSS console, select **HTML file**.
2. Download the file.
3. Upload the file to the root directory of the second-level domain.
4. Make sure you can access the file via `http://second-level domain/second-level domain_cssauth.html`.
5. Click **Verify now**. If the verification succeeds, you can proceed to the next step.
![](https://qcloudimg.tencent-cloud.cn/raw/e2f4412681655ec81b55965ed4216a9d.png)

>! After finishing the **Basic settings**, you can proceed to the **CNAME configuration** step. For more information about CNAME configuration, see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).
