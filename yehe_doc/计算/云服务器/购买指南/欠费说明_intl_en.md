## Pay-as-you-go CVMs

![](https://main.qcloudimg.com/raw/9bdaf733b5a50e486254ba36db76240d.jpg)

### Notes
- When you no longer use pay-as-you-go resources, **please terminate them as soon as possible** to avoid additional fees.
>- After a CVM is terminated or repossessed, the data will be cleared and cannot be recovered.
> Since your actual resource consumption may change from time to time, deviation in the timing of the balance alert may exist.

### Alerts

<table>
	<tr><th>Alert Type</th><th>Description</th></tr>
	<tr><td><b>Arrears Reminder</b></td><td>Fees for pay-as-you-go resources are charged by the hour. If your account balance becomes negative, we will notify the Tencent Cloud account creator, global resource collaborators, and financial collaborators via email and SMS.</td></tr>
	<tr><td><b>Arrears Alert</b></td><td>This feature is off by default. To enable it, please see <a href="https://intl.cloud.tencent.com/document/product/213/2181#arrears-reminder"> Arrears Alert </a> to subscribe.</td></tr>
</table>

### Arrears Processing
When your account balance becomes negative, you can continue to use CVM for the **next 2 hours**. You will be billed for this usage. After 2 hours, if your account is not topped up to a positive balance, CVM service and billing will automatically stop.
After automatic shutdown, the system will perform the following operations on its CVM:
<table>
	<tr><th>Time after automatic shutdown</th><th>Description</th></tr>
	<tr><td rowspan=2><b>≤ 24 Hours</b></td><td>If your account is topped up to a positive balance, billing will continue and you can start your CVM.</td></tr>
	<tr><td>If your account is not topped up to a positive balance, you will not be able to start your CVM.</td></tr>
	<tr><td><b>＞ 24 Hours</b></td><td>If your account is not topped up to a positive balance, your pay-as-you-go CVM will be repossessed. All data will be deleted and cannot be recovered. When your CVM is repossessed, we will notify the Tencent Cloud account creator and all collaborators via email and SMS.</td></tr>
</table>

## Bill-by-traffic Network
<table>
	<tr><th>Alert Type</th><th>Description</th></tr>
	<tr><td><b>Balance Alert</b></td><td>Network traffic consumption fluctuates significantly and is difficult to predict. Therefore, we do not provide balance alert.</td></tr>
	<tr><td><b>Arrears Alert</b></td><td>When your balance becomes negative, you can continue to use the bill-by-traffic network for <b>the next 2 hours<b>. You will be billed for this usage. After 2 hours, the bill-by-traffic network service will automatically stop. </br>After your account is topped up to a positive balance, the traffic service will resume. Please check your network settings and restore the binding between the affected CVM and the Cloud Load Balancer.</td></tr>
</table>

> For more information on traffic fees, please see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).
>
