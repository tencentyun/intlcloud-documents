## Pay-as-You-Go Enterprise Edition Instance

### Precautions
- When you no longer need to use pay-as-you-go instances, **terminate them as soon as possible** to avoid continued fee deductions.
- After an instance is terminated or repossessed, its data is cleared and cannot be recovered.
- Since your actual resource consumption changes constantly, some slight discrepancies may exist for your stated balance.
- When an instance in arrears is automatically repossessed, due to the restrictions of the COS billing policy, the associated backend bucket cannot be automatically deleted. Please go to the [COS console](https://console.cloud.tencent.com/cos) console to manage the COS bucket and avoid continued fee deductions.

### Alerts

<table>
	<tr><th>Type</th><th>Description</th></tr>
	<tr><td><b>Arrears reminder</b></td><td>Pay-as-you-go resources are billed on the hour. When your account balance becomes negative, your Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified via email and SMS.</td></tr>
	<tr><td><b>Arrears alert</b></td><td>This feature is disabled by default.</td></tr>
</table>

### Arrears processing
To ensure that your business app updates are not affected by temporary arrears, you can continue to use TCR for **24 hours** after your account balance becomes negative and will be billed for this time. If your account is still in arrears after 24 hours, the instances in your account will all be isolated and billing will stop.
After instances are isolated, the system will process them as follows:
<table>
	<tr><th>Time Since Isolation</th><th>Description</th></tr>
	<tr><td rowspan=2><b>≤ 7 days</b></td><td>If your account is topped up to a positive balance, billing will resume and the instances will automatically recover to the running status.</td></tr>
	<tr><td>If your account is not topped up to a positive balance, the instances will remain isolated.</td></tr>
	<tr><td><b>> 7 days</b></td><td>If your account is not topped up to a positive balance, your pay-as-you-go instances will be repossessed, and all data in the instances will be irrecoverably erased. When instances are repossessed, the Tencent Cloud account creator and all collaborators will be notified via email and SMS.</td></tr>
</table>

When your account is in arrears, you can delete instances you do not need to avoid continued billing. For more information about deleting instances, see [Terminating/Returning Instances](https://intl.cloud.tencent.com/document/product/1051/39087).

>! When an instance in arrears is automatically repossessed, due to the restrictions of the COS billing policy, the associated backend bucket cannot be automatically deleted. Please go to the [COS console](https://console.cloud.tencent.com/cos) to manually manage the COS bucket.
>


## Data Storage Billing and Arrears
In TCR, when an Enterprise Edition instance is created, a COS bucket will be automatically created in the region of the instance and associated with the instance. During the use of the instance, container images, Helm Charts, and other data are directly stored in the bucket. Users can view and manage relevant data and configure data encryption and backup modes. These resources are directly provided and billed by the COS service. For more information about the billing rules and arrears, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Notes on Arrears](https://intl.cloud.tencent.com/document/product/436/10044).
