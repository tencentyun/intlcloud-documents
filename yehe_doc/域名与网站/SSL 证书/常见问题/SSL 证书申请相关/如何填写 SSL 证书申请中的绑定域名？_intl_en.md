
### How to fill in the domains bound to an SSL certificate during the application?
After purchasing the SSL certificate, you need to go to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) to submit the materials for review. The SSL Certificate Service console will prompt you the type and number of domain names based on the certificate you purchased, as shown in the following figure:
![](https://main.qcloudimg.com/raw/1d7c5362e48996c7deb9bc0d5a761bc6.png)

>? To ensure that your SSL certificate can be issued and HTTPS can be used properly, please fill in information about the bound domains correctly.

Based on the brand of your certificate and the domains bound, SSL Certificate Service will offer the corresponding parent domain for free. Details are described as follows:

<table>
<thead>
  <tr>
    <th style ="width:150px;height:45px;position:relative;text-align:left;padding:7px 10px;font-weight:700;" valign="top" ><div style="position:absolute;width:1px;height:158px;top:0;left:0;background-color: #d9d9d9;display:block;transform:rotate(-69deg);transform-origin:top;valign=top;"></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Certificate Type<br>Rule</th>
    <th>GlobalSign</th>
    <th>TrustAsia (OV/EV)</th>
    <th>TrustAsia (DV)</th>
    <th>GeoTrust</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>If the bound domain is not prefixed with `www.`, the `www.` sub-domain is offered for free.</td>
    <td>No</td>
    <td>If the bound domain is a primary domain, the `www.` sub-domain is offered for free.</td>
    <td>If the bound domain is a primary domain, the `www.` sub-domain is offered for free.</td>
    <td>If the bound domain is a primary domain, the `www.` sub-domain is offered for free.</td>
  </tr>
  <tr>
    <td>If the bound domain is a general or wildcard domain, the parent domain is offered for free.</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Yes</td>
  </tr>
</tbody>
</table>

### Wildcard domains
A wildcard domain is one with a wildcard, for example, `*.tencent.com` and `*.cloud.tencent.com`. It includes all sub-domains at the same level.
>!Cross-level domains are not supported. For example, `*.tencent.com` does not include the `*.cloud.tencent.com` child domains.
