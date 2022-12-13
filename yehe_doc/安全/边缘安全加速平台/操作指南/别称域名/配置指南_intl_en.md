This document describes how to create, edit, and delete a domain alias, configure the CNAME record of the domain alias to point to the target domain name, and configure a certificate for the domain alias.

## Prerequisites
You have [purchased](https://console.cloud.tencent.com/edgeone) the EdgeOne Enterprise plan, [connected your site](https://intl.cloud.tencent.com/document/product/1145/45966), and created the target domain name.

## Creating a Domain Alias

### Step 1. Create a domain alias
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Domain Alias** on the left sidebar.
2. On the domain alias list page, click **Create domain alias**, configure parameters, and click **OK**.<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/8wtm193_1-en.png" width=800px>
<table>
<thead>
<tr>
<th width="10%">Parameter</th>
<th width="90%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Domain alias</td>
<td>It can contain up to 81 characters. Wildcard domain names such as <code>*.test.com</code> are not supported. If the acceleration region of your site is in the Chinese mainland, you need to get an ICP filing for your domain alias.</td>
</tr>
<tr>
<td>Target domain name</td>
<td>You can select a domain name of the current site in the **Activated** or **Deploying** status. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1145/46354">CNAME Connection</a> and <a href="https://intl.cloud.tencent.com/document/product/1145/46353">NS Connection</a>.</td>
</tr>
<tr>
<td>Certificate configuration</td>
<td><ul><li>Do not configure: It indicates not to configure the HTTPS certificate. If you select this option, the domain alias has only HTTPS access capabilities.</li><li>SSL managed certificate: It indicates to select a certificate managed in SSL. To purchase or upload an external certificate, <a href="https://intl.cloud.tencent.com/contact-us">contact us</a>.</li><li> Apply for free certificate: The platform implements the application and automatic update of free certificates. To select this option, add a domain name and point the CNAME record of the domain alias to the target domain name at your DNS service provider.</li></ul></td>
</tr>
</tbody></table>


### Step 2. Add the CNAME record of the domain alias that points to the target domain name
1. After the domain alias is added successfully, it is **not activated** by default as shown below:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/DW7n261_2-en.png" width=800px>
2. Go to your DNS service provider and add a CNAME record that points to the target domain name to activate the domain alias. 
3. EdgeOne will automatically perform a check and change the status of the domain alias to **Activated**.

### Step 3. Apply for a free certificate (optional)
If you have pointed the CNAME record of the domain alias to the target domain name at your DNS service provider, you can apply for a free certificate in EdgeOne.   
1. On the [domain alias list page](https://console.cloud.tencent.com/edgeone/alias-domain), click **Edit** and select **Apply for free certificate**.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/C7tD159_4-en.png" width=800px>
2. Click **OK**. 

## Editing a Domain Alias
1. On the [domain alias list page](https://console.cloud.tencent.com/edgeone/alias-domain), select the target domain alias and click **Edit**.
2. Modify the target domain name and certificate configuration type as needed and click **OK**.

## Deleting a Domain Alias
>!
>- A domain alias not disabled cannot be directly deleted.
>- The data cannot be recovered once a domain alias is deleted. Proceed with caution.

1. On the [domain alias list page](https://console.cloud.tencent.com/edgeone/alias-domain), select the target domain alias and click **Disable** > **Delete**.
2. In the pop-up window, click **OK**.<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/wrVH295_5-en.png" width=600px>

## Searching for a Domain Alias
On the [domain alias list page](https://console.cloud.tencent.com/edgeone/alias-domain), enter a keyword in the search input box and press Enter to search for a domain alias.  
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/8yBE228_6-en.png" width=800px>