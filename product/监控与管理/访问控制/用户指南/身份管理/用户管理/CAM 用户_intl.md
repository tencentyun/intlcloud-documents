CAM users are identities you create in Tencent Cloud, and each CAM user is associated with only one Tencent Cloud account. The Tencent Cloud account you register is **primary account**. You can also create **sub-accounts** with custom permissions in [**User**](https://intl.cloud.tencent.com/login), which further assist you to work with your Tencent Cloud resources. There are 3 types of sub-account: [sub-users](https://intl.cloud.tencent.com/document/product/598/13674), [collaborators](https://intl.cloud.tencent.com/document/product/598/13666) and [message recipients](https://intl.cloud.tencent.com/document/product/598/13667).
<table>
	<tr>
		<th rowspan="2">Account Type</th>
		<th rowspan="2">Primary Account</th>
		<th colspan="3">Sub-Account</th>
	</tr>
	<tr>
		<th>Sub-User</th>
		<th>Collaborator</th>
		<th>Message Recipient</th>
	</tr>
	<tr>
		<td>Definition</td>
		<td>
					<ul>
						<li>A primary account owns all the resources in Tencent Cloud and have the access to any of its resources.</li>
						<li>It is not recommended to work with resources using the primary account. You should create sub-accounts and assign policies to them based on the principle of minimum weight, and then work with the cloud resources using the sub-accounts with limited permissions.</li>
					</ul>
		</td>
		<td>A sub-user is created by a primary account and is subordinate to the primary account.</td>
		<td>When a primary account is added as the collaborator of the current primary account, it becomes one of the sub-accounts of the current primary account. The account can be switched from collaborator back to primary account.</td>
		<td>A message recipient can only receive messages.</td>
	</tr>
	<tr>
		<td>Console access</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>Programmatic access</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>Policy Authorization</td>
		<td>Owns all the policies by default.</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>Message Notification</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
	</tr>
</table>


