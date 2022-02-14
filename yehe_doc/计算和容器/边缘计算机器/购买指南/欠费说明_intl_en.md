
![](https://qcloudimg.tencent-cloud.cn/raw/b995ac21df93f58b8ec5cfa0b0d4febb.png)

## Notes
- After you stop using an ECM instance, **terminate it as soon as possible** to avoid incurring fees.
- After an ECM instance is terminated or repossessed, the data will be cleared and cannot be recovered.
- Since your actual resource consumption changes constantly, some slight discrepancies may exist for your stated balance.

## Alerts

<table>
	<tr><th>Alert Type</th><th>Description</th></tr>
	<tr><td><b>Overdue payment reminder</b></td><td>Fees for a day will be deducted in the morning the next day. When your account balance becomes negative, your Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified by email and SMS.</td></tr>
	<tr><td><b>Overdue payment alert</b></td><td>This feature is disabled by default.</td></tr>
</table>

## Overdue Payment Policy 
From the time when your account balance becomes negative, ECM can still be used normally and fees will still be deducted for **24 hours**. After 24 hours, the instance will be automatically shut down, but fees will still be incurred until the instance is terminated.
After automatic shutdown, the system will process ECM as follows:
<table>
	<tr><th>Time Since Shutdown</th><th>Description</th></tr>
	<tr><td><b>≥ 24 hours and < 7 days </b></td><td><ul  style="margin: 0;"><li>If your account is topped up to a positive balance, you can start the instance.</li><li>If your account balance remains negative, the instance cannot be started.</li></ul></td></tr>
	<tr><td><b>≥ 7 days</b></td><td>If your account is not topped up to a positive balance, your pay-as-you-go resources will be repossessed and released. All data will be deleted and cannot be recovered. When your resources are repossessed, your Tencent Cloud account creator and all collaborators will be notified by email and SMS.</td></tr>
</table>

## Network Billing by Peak Bandwidth

<table>
	<tr><th>Alert Type</th><th>Description</th></tr>
	<tr><td><b>Balance alert</b></td><td>Network bandwidth consumption tends to fluctuate significantly and is difficult to predict. Therefore, the system does not offer balance alerts.</td></tr>
	<tr><td><b>Overdue payment alert</b></td><td>When your account balance becomes negative, you can still continue using the network service in <b>24 hours</b>, and fees will still be incurred. After 24 hours, the network service will stop.</br></td></tr>
</table>

>! For more information on billing by peak bandwidth, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1119/43404).
>

