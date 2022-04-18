
## Background
HTTPDNS is a DNS service provided for mobile applications, mini programs, and PC clients. It sends DNS requests to the DNS server of Tencent Cloud over the HTTP protocol instead of the local DNS of the ISP over the DNS protocol. This helps avoid domain name hijacking and cross-network access problems in different network environments caused by local DNS and eliminate DNS exceptions in mobile internet services.
>?
>- Because of the upgrade of the technical architecture and the support for new features, the HTTPDNS team has launched HTTPDNS Enterprise Edition `119.29.29.98/99`, and HTTPDNS Free Edition will be gradually disused and eventually stopped **at 00:00 on January 1, 2022**.
>- HTTPDNS **Enterprise Edition with the original IP `119.29.29.29`** will also be gradually scaled in as the server resources expire and will be eventually deactivated. We recommend you [switch to 119.29.29.98/99](https://intl.cloud.tencent.com/document/product/1130/44463) to eliminate any unexpected risks.

The HTTPDNS team will provide [service support](https://intl.cloud.tencent.com/support) to assist you in switching to HTTPDNS Enterprise Edition `119.29.29.98/99`. Therefore, to avoid affecting your business, switch the IP as soon as possible.

## Features of Enterprise Edition
HTTPDNS `119.29.29.29` provides only the basic DNS service, and the following features are exclusive to `119.29.29.98/99`.

<table>
<thead>
  <tr>
    <th>Item</th>
    <th>Description<br></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Unlimited requests </td>
    <td><ul style="margin:0"><li>For `119.29.29.98/99`, there is no limit on the API request rate of the client application.</li><li>For `119.29.29.29`, the request limit is 100 QPS for a single IP and 1,000 QPS for a single domain for testing purposes.</li></ul></td>
  </tr>
  <tr>
    <td>Nodes outside the Chinese mainland </td>
    <td>In recent years, focus has been placed on adding more nodes of Enterprise Edition outside the Chinese mainland, and Anti-DDoS clusters based on the BGP Anycast network have been created.<br></td>
  </tr>
  <tr>
    <td>Accelerated DNSPod DNS </td>
    <td>HTTPDNS can further accelerate the authoritative DNS query of domains hosted in DNSPod.</td>
  </tr>
  <tr>
    <td>Connection to HTTPDNS via HTTP SDK</td>
    <td>HTTPDNS can be quickly connected through SDK for both iOS and Android.<br></td>
  </tr>
  <tr>
    <td>DES, AES, and HTTPS <br>encryption of data</td>
    <td>Encryption with DES, AES, or HTTPS prevents requests in plaintext from being maliciously altered during transfer.<br></td>
  </tr>
  <tr>
    <td>Support for new features</td>
    <td>All new features under development will be available only on Enterprise Edition.</td>
  </tr>
  <tr>
    <td>Alert</td>
    <td>Alarm notification.</td>
  </tr>
  <tr>
    <td>Domain management</td>
    <td>Domain management in the console.<br></td>
  </tr>
  <tr>
    <td>Reports and statistics </td>
    <td>You can collect DNS query volume and view statistical changes.<br></td>
  </tr>
  <tr>
    <td>Service upgrade</td>
    <td>Data audit analysis and industry-specific solution are supported for key accounts.<br></td>
  </tr>
  <tr>
    <td>SLA guarantee</td>
    <td>99.99% service availability is guaranteed.<br></td>
  </tr>
</tbody>
</table>

>?The ECS (EDNS-Client-Subnet) protocol adds the IP address of the user requesting DNS in the DNS request packet, based on which the DNS server can return a server IP address for quicker access by the user.
>
## Switching Guide
>?
>
>- Users who migrate to HTTPDNS Enterprise Edition **by 23:59:59 on September 30, 2021** and **by 23:59:59 on October 31, 2021** will be offered subsidies respectively.
>- If you are using HTTPDNS Enterprise Edition but have currently connected to `119.29.29.29`, you only need to switch the access IP to `119.29.29.99` (for HTTPS encryption) or `119.29.29.98` (for AES/DES encryption) with no need to perform any operations in the console. For directions on connection, see [Connecting to HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44462).
>- If you are using the HTTPDNS Enterprise Edition SDK, update it to the latest version and replace the access IP with `119.29.29.99/98`.

### Step 1. Activate HTTPDNS
For detailed directions, see [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461).

### Step 2. Bind the authorization ID 
- If you already have an authorization ID, bind it first as instructed [here](https://intl.cloud.tencent.com/document/product/1130/44461).
- If you don't have an authorization ID, you can skip this step after activating HTTPDNS.

### Step 3. Add a domain
For detailed directions, see [Adding a Domain](https://intl.cloud.tencent.com/document/product/1130/44465).

### Step 4. Connect to HTTPDNS Enterprise Edition

Select the method for connecting to HTTPDNS Enterprise Edition based on your business and usage:

<dx-tabs>
::: Resolve domain with HTTPDNS APIs
1. 
 You can query in the following two ways:
	- Single query
		- HTTPS encryption:
		` https://119.29.29.99/d?dn=[domain]&token=[HTTPS Token]&ttl=1`
		- AES/DES encryption:
		 `http://119.29.29.98/d?dn=[encrypted domain string]&id=[authorization ID]&ttl=1`
		- For more information on the encryption methods, see [Encryption Guide](https://intl.cloud.tencent.com/document/product/1130/44470).
		- For more information on the request format, see [API Description](https://intl.cloud.tencent.com/document/product/1130/44468).
	- Batch query
HTTPDNS supports batch querying domains. You can enter multiple domains and separate them by comma, and the query results will be separated by `\n`.
For example, you can query `cloud.tencent.com,www.qq.com,www.dnspod.cn` at a time.
2. Client modifications: Change the client DNS to HTTPDNS. Note that you need to **retain the local DNS as a backup** during connection. For more information, see [Best Practices](https://intl.cloud.tencent.com/document/product/1130/44471).

:::
::: Resolve domain with latest HTTPDNS SDK APIs

1. To resolve a domain with HTTPDNS SDK APIs, you need to submit an application for connection to the SDK in the HTTPDNS console as instructed in [SDK Activation Process](https://intl.cloud.tencent.com/document/product/1130/44474).
2. Tencent Cloud's proprietary SDKs provided by HTTPDNS are highly customizable and can be directly embedded in applications. With mature and stable features, they have been widely used on Tencent's various types of game clients. You can choose from the instructions below based on your environment for connection to follow:

 	- [SDK for iOS](https://intl.cloud.tencent.com/document/product/1130/44472)
 	- [SDK for Android](https://intl.cloud.tencent.com/document/product/1130/44473)
 	- [Special Scenario - HTTPS](https://intl.cloud.tencent.com/document/product/1130/44475)
 	- [Special Scenario - Unity Connection](https://intl.cloud.tencent.com/document/product/1130/44476)
 	- [Special Scenario - HTML5 Page](https://intl.cloud.tencent.com/document/product/1130/44477)
:::
</dx-tabs>


>?After migrating the IP, you can continue to use the monthly free tier and the purchased DNS plan, and the specification of and discount on the original plan as well as the billing rules will remain unchanged.

