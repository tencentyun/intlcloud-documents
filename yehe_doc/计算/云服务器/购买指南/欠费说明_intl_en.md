## Pay-as-you-go CVM Instances

![](https://main.qcloudimg.com/raw/463d6b815dcf2677ebe28f9683d14430.jpg)

### Notes
- After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deduction.
- After a CVM instance is terminated or repossessed, its data will be cleared and cannot be recovered.
- Since your actual resource consumption changes constantly, some slight discrepancies may exist for your stated balance.

### Alerts

<table>
	<tr><th>Alert Type</th><th>Description</th></tr>
	<tr><td><b>Arrears reminder</b></td><td>Pay-as-you-go resources are billed on the hour. When your account balance becomes negative, your Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified via email and SMS.</td></tr>
	<tr><td><b>Arrears alert</b></td><td>This feature is disabled by default.</td></tr>
</table>

### Arrears policy
When your account balance falls below zero, you can continue to use CVM instances for the next 2 hours. We will also continue to bill you for this usage. After that, if your account balance remains negative, your CVM instances are shut down automatically and billing stops.
After automatic shutdown, your CVM instances go through the following stages:
<table>
	<tr><th>Time Since Shutdown</th><th>Description</th></tr>
	<tr><td rowspan=2><b>≤ 15 days</b></td><td>If your account is topped up to a positive balance, billing resumes and you can continue to use your CVM instances.</td></tr>
	<tr><td>If your account balance remains negative, you will not be able to start your CVM instances.</td></tr>
	<tr><td><b>> 15 days</b></td><td>If your account is not topped up to a positive balance, your pay-as-you-go CVMs will be repossessed. All data will be erased and cannot be recovered. When your CVM is repossessed, Tencent Cloud account creator and all collaborators will be notified via email and SMS.</td></tr>
</table>

## Bill-by-traffic Network
<table>
	<tr><th>Alert Type</th><th>Description</th></tr>
	<tr><td><b>Balance alert</b></td><td>Network traffic consumption tends to fluctuate significantly and is hardly predictable. Therefore, we do not offer balance alerts.</td></tr>
	<tr><td><b>Arrears alert</b></td><td>When your balance becomes negative, you can continue to use the bill-by-traffic network for <b>the next 2 hours<b>. We will also continue to bill you for this usage. After that, if your account balance remains negative, the bill-by-traffic network service automatically stops. </br>After your account is topped up to a positive balance, the service resumes. Check the affected CVM instances and CLB instances and resume their association if necessary.</td></tr>
</table>

>! For information on traffic fees, see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).
>
