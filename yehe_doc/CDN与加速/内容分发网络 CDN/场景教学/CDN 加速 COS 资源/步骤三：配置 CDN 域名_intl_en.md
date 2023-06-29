
1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Domain Management** on the left sidebar to enter the domain name management page, and click **Create a Distribution**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ds3Z834_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423153247.png)
2. Domain name configuration
Configure your website as below:
<br>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Aw8L098_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423153500.png" width="80%">
<br>
When you add a domain name for the first time, add a wildcard domain name, or add a domain name that is already added by another account, you must verify your ownership of the domain name, as shown in the preceding figure. If your DNS service provider is Tencent Cloud, you can configure a TXT record for the primary domain name based on the following figure and verify the domain name ownership. For more information, see <a href="https://intl.cloud.tencent.com/document/product/228/42693">Domain Name Ownership Verification</a>.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/iX89276_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423154418.png">
3. Origin configuration
The origin server stores the resources of your website. When a client requests resources from a CDN node but the requested resources are not cached on the node, the node reads the origin server settings configured for the domain name, pulls the resources from the origin server, and caches the resources on the node. Therefore, it is important to correctly configure the origin server settings to ensure that CDN pulls the requested resources from the origin server.
Configure the origin server settings based on the following example:
<br>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/8dKk701_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423153800.png" width="90%">
<table>
<thead>
<tr>
<th>Configuration</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Origin server type</td>
<td>The origin server of your website is the server that maintains the stable business operation. If you own the server, select <strong>Customer Origin</strong>.</td>
</tr>
<tr>
<td>Origin-pull Protocol</td>
<td>If you select <strong>Customer Origin</strong> for <strong>Origin type</strong>, only HTTP origin-pull is supported and you can select only <strong>HTTP</strong>.<br>If your origin server supports other origin-pull protocols, you can select a protocol as needed.</td>
</tr>
<tr>
<td>Origin server address</td>
<td><strong>Enter the IP address of the origin server.</strong><br>• You can configure multiple origin server addresses, and then CDN will perform round-robin origin-pull.<br>• You can also configure the port (0 - 65535) and weight (1 - 100), so that the origin server address is in the format of `origin server IP address:port:weight`. You can also leave the port unspecified, so that the origin server address is in the format of `origin server IP address::weight`. At present, the HTTPS protocol supports only port 443.<br>• You can configure a domain name as the origin server, which must be different from the CDN acceleration domain name.</td>
</tr>
<tr>
<td>Host</td>
    <td>• Definition: This configuration item refers to the domain name accessed on the origin server by a CDN node during origin-pull.<br>• Differences between <b>Origin address</b> and <b>Origin Domain</b>: The IP address or domain name that is configured on the origin server allows a CDN node to find the corresponding origin server during origin-pull. If multiple websites run on the origin server, the value of <b>Origin Domain</b> specifies the website where the resources are stored.<br>• Configuration instruction: If the resources can be obtained by using the acceleration domain name during origin-pull, you do not need to modify the value. If the resources can be obtained by using another domain name rather than the acceleration domain name during origin-pull, you need to enter the corresponding domain name.</td>
</tr>
</tbody></table>

4. Click **OK**. Note that Tencent Cloud CDN allows you to use recommended configurations based on the acceleration type. For more information, see [Configuring CDN from Scratch](https://intl.cloud.tencent.com/document/product/228/32978). If you do not want to set the recommended configurations at the moment, you can click **Back** to return to the domain name management list.
