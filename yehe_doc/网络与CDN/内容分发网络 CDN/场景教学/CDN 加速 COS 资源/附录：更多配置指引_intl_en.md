
CDN provides advanced features to enhance the acceleration performance and access security.
Click **Manage** in the **Operation** column of the domain name.

<table>
<thead>
<tr>
<th>Use Case</th>
<th>Description</th>
<th>Specification</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="2">Increase cache hit rate</td>
<td>Proper cache policies can effectively improve the cache hit rate. We recommend that you perform the following operations:<br>• Set a cache validity period of more than 30 days for static files that are rarely updated, such as images and texts.<br>• Set a cache validity period based on your business requirements for frequently updated files, such as JS and CSS files.<br>• Do not cache general dynamic files, such as PHP, JSP, ASP, and ASPX files.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/38424">Node Cache Configuration</a></td>
</tr>
<tr>
<td>If your business URLs contain parameters and the change of all or some of the parameter values has no effect on the target file, we recommend that you ignore caching parameters.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35316">Cache Key Rule Configuration</a></td>
</tr>
<tr>
<td rowspan="2">Increase access security</td>
<td>You can enable HTTPS access for your website.<br>• If you already have a certificate, you can directly upload it.<br>• You can also go to <a href="https://console.cloud.tencent.com/ssl">SSL Certificate Management</a> to apply for a free DV SSL certificate issued by TrustAsia.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35213">HTTPS Configuration Guide</a></td>
</tr>
<tr>
<td>You can enable hotlink protections by using the following configurations:<br>IP allowlist/blocklist, referer allowlist/blocklist, UA allowlist/blocklist, and URL authentication.</td>
<td><a href="https://www.tencentcloud.com/document/product/228/7865">Access Control</a></td>
</tr>
<tr>
<td>Avoid high bills</td>
<td>You can enable related protections to help prevent extra costs for extensive bandwidth and traffic caused by malicious attacks and hotlinking.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/42355">Preventing High Bills</a></td>
</tr>
</tbody></table>

