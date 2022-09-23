### Overdue Payment
Your managed clusters will be processed as instructed below since **your account balance falls below 0**.
- Within 24 hours: Your TKE managed clusters can be used and are billed.
- After 24 hours: All managed clusters under the account are in **isolated** status and are not billed. You cannot access the API Server. Applications deployed on the nodes are not affected.
>? If your account balance is below 0 **before 10:00, April 1, 2022 (UTC +8)**, the **TKE managed clusters created before 10:00, March 21, 2022 (UTC +8)** are isolated after 10:00, April 1, 2022 (UTC +8).
>

### Processing for Overdue Payments
When the managed clusters are in **isolated** status, Tencent Cloud will take the following actions:
>! The following description of overdue payment is only for managed clusters. For [Overdue Payment of CVM Instances](https://intl.cloud.tencent.com/document/product/213/2181), see the corresponding descriptions.
>
<table>
	<tr><th>Time Since Isolation</th><th>Description</th></tr>
	<tr><td rowspan=2><b>≤ 15 days</b></td><td>If your account is topped up to a positive balance, billing will resume and the clusters will automatically resume the running status.</td></tr>
	<tr><td>If your account is not topped up to a positive balance, the clusters will remain isolated.</td></tr>
	<tr><td><b>＞ 15 days</b></td><td>If overdue payment of your account persists, the clusters will be deleted and cannot be recovered. All nodes remaining in the clusters will be removed. We will notify the creator and all collaborators of the Tencent Cloud account through email and SMS when the clusters under the account are deleted.</td></tr>
</table>
