
CAM users are identities you create in Tencent Cloud. Each CAM user is associated with only one Tencent Cloud account. The Tencent Cloud account you registered is the **root account**. You can also create **sub-accounts** with custom permissions in [**Users**](https://console.cloud.tencent.com/cam) to help you manage your Tencent Cloud resources. There are 3 types of sub-account: [sub-users](https://intl.cloud.tencent.com/document/product/598/13674), [collaborators](https://intl.cloud.tencent.com/document/product/598/32639) and [message recipients](https://intl.cloud.tencent.com/document/product/598/13667).

<table>
	<tr>
		<th rowspan="2">Account Types</th>
		<th rowspan="2">Root Account</th>
		<th colspan="3">Sub-account</th>
	</tr>
	<tr>
		<th>Sub-user</th>
		<th>Collaborator</th>
		<th>Message Recipient</th>
	</tr>
	<tr>
		<td>Definition</td>
		<td>
					<ul>
						<li>Owns all Tencent Cloud resources, and can access any of the resources.</li>
						<li>We strongly recommend against using the root account to manage or operate resources. Instead, create sub-accounts and associate them with policies as required. Use these sub-accounts with limited permissions to work with your cloud resources.</li>
					</ul>
		</td>
		<td>Created by the root account, and fully belongs to the root account that created the sub-user.</td>
		<td>When a root account is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account. The account can be switched from collaborator back to root account.</td>
		<td>Only has message receiving capabilities</td>
	</tr>
	<tr>
		<td>Console Access</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>- </td>
	</tr>
	<tr>
		<td>Programming Access</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>- </td>
	</tr>
	<tr>
		<td>Policy Authorization</td>
		<td>Owns all policies by default</td>
		<td>✔</td>
		<td>✔</td>
		<td>- </td>
	</tr>
	<tr>
		<td>Message Notifications</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
	</tr>
</table>

