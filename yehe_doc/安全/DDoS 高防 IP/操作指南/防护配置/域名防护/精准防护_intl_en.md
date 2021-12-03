## Use Cases
Anti-DDoS supports precise protection for connected web applications. With the precise protection, you can configure protection policies combining multiple conditions of common HTTP fields, such as URI, UA, Cookie, Referer, and Accept to screen access requests. For the requests matched the conditions, you can configure CAPTCHA to verify the requesters or a policy to automatically drop or allow the requests. Precise protection is available for policy customization in various use cases to precisely defend against CC attacks.

The match conditions define the request characteristics to be checked, i.e., the attribute characteristics of the HTTP field in a request. Precise protection supports checking the HTTP fields below:
<table>
    <tr>
        <th>Match Field</th>
        <th>Field Description</th>
				<th>Logic</th>
    </tr>
    <tr>
        <td>URI</td>
        <td>The URI of an access request.</td>
				<td>Equals to, includes, or does not include.</td>
    </tr>
    <tr>
        <td>UA</td>
        <td>The identifier and other information of the client browser that initiates an access request.</td>
				<td>Equals to, includes, or does not include.</td>
    </tr>
    <tr>
        <td>Cookie</td>
        <td>The cookie information in an access request.</td>
				<td>Equals to, includes, or does not include.</td>
    </tr>
    <tr>
        <td>Referer</td>
        <td>The source website of an access request, from which the access request is redirected.</td>
				<td>Equals to, includes, or does not include.</td>
    </tr>
    <tr>
        <td>Accept</td>
        <td>The data type to be received by the client that initiates the access request.</td>
				<td>Equals to, includes, or does not include.</td>
    </tr>
</table>

## Prerequisite
You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select a domain name under an instance ID from the left list, e.g., **212.64.xx.xx bgpip-000002je** -> **http:80** -> **www.xxx.com**.
![](https://main.qcloudimg.com/raw/560df07c97e00d499d0363fa9ae58977.png)
3. Click **Set** in the **Precise Protection** section to view the rule list.
![](https://main.qcloudimg.com/raw/f2177416c56413c6b4bec977468e8255.png)
4. Click **Create** to create a precise protection rule. Fill in the fields and click **OK**.
![](https://main.qcloudimg.com/raw/0b4604f0d97e6059c6d35c3181beee60.png)
5. Now the new rule is added to the rule list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/13ed1705034538fc6fc1b1090a65bc8e.png)
