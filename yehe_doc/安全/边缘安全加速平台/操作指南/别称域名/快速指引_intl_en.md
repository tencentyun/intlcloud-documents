This document describes how to create a domain alias for the target domain name and apply for a free certificate.

#### Scenario
You have connected `target.xxxxxx.cn` to EdgeOne. Many merchant domain names are configured the same as this domain name. To reuse the acceleration and security capabilities of the domain name for the merchant domain names, you can use the domain alias feature.
- **Target domain name:** `target.xxxxxx.cn`.
- **Domain alias:** For example, `alias.xxxxxx.net`, with the same configuration as `target.xxxxxx.cn`.


## Prerequisites
You have [purchased](https://console.cloud.tencent.com/edgeone) the EdgeOne Enterprise plan, [connected your site](https://intl.cloud.tencent.com/document/product/1145/45966), and created the target domain name.
Below is the target domain name in this example:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/2MQU031_1-en.png" width=800px>


## Step 1. Create a domain alias
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Domain Alias** on the left sidebar.
2. On the domain alias list page, click **Create domain alias**, configure parameters, and click **OK**.<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/zKxu074_2-en.png" width=900px>
<table>
<thead>
<tr>
<th width="10%">Parameter</th>
<th width="90%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Domain alias</td>
<td><code>alias.xxxxxx.net</code> is entered here.</td>
</tr>
<tr>
<td>Target domain name</td>
<td><code>target.xxxxxx.cn</code> is selected here.</td>
</tr>
<tr>
<td>Certificate configuration</td>
<td>When creating a domain alias, you can select <strong>Do not configure</strong> or <strong>SSL managed certificate</strong>. To select <strong>Apply for free certificate</strong>, add a domain name and point the CNAME record of the domain alias to the target domain at your DNS service provider. <strong>Do not configure</strong> is selected here.</td>
</tr>
</tbody></table>

## Step 2. Add the CNAME record of the domain alias that points to the target domain name
1. After the domain alias is added successfully, it is **not activated** by default as shown below:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/gknM234_3-pro-en.png" width=800px>
2. Go to your DNS service provider and add a CNAME record that points to the target domain name to activate the domain alias. 
3. EdgeOne will automatically perform a check and change the status of the domain alias to **Activated**.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/784p027_5-pro-en.png" width=800px>

## Step 3. Apply for a free certificate (optional)
If you have pointed the CNAME record of the domain alias to the target domain name at your DNS service provider, you can apply for a free certificate in EdgeOne.   
1. On the [domain alias list page](https://console.cloud.tencent.com/edgeone/alias-domain), click **Edit**, select **Apply for free certificate**, and click **OK**. 
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/LraQ905_6-en.png" width=800px>
2. After the free certificate is obtained, go to the [domain alias list page](https://console.cloud.tencent.com/edgeone/alias-domain) and click **Domain alias HTTPS** to view the information of the deployed certificate:   
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/My6z824_7-en.png" width=800px>

## Step 4. Verify the effect
1. Verify the target domain name.      
   Access the target domain name through the browser and send a curl request to it. The results are as shown below:<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/BGZb893_1.png" width=800px><br>
	 <img src="https://qcloudimg.tencent-cloud.cn/raw/24167e0f207e7657e4c54cff5ee59bde.png" width=800px>
2. Verify the domain alias.      
   After getting the result of the request to the target domain name, access the domain alias through the browser and send a curl request to it. Check whether the results are the same:<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Wb7z933_2.png" width=900px><br><img src="https://qcloudimg.tencent-cloud.cn/raw/f8369022667d2b3b258fc092b202b430.png" width=800px>

As shown above, the same response is obtained for the requests to the domain alias and target domain name, indicating that the domain alias has taken effect as expected.
