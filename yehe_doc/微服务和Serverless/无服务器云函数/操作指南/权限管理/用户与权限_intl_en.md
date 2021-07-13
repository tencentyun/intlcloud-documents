## Operation Scenarios
When you use the SCF Console or CLI, you may need to manipulate the permissions to SCF or other products. For example, you can grant the permissions to query the CMQ topic list, VPC information, or Cloud Monitor statistics.

SCF provides preset policies for granting access to SCF and other associated resources. For more information, please see [Notes on User Policy Update](#Strategy). SCF updates preset policies as needed to ensure that you have access to newly released features. You can also create custom policies to manage user permissions.


## Directions
>If you are currently a subuser/collaborator, authorization should be performed by the root account in the following steps. After the authorization is completed, both the root account and subuser can log in and use the SCF service.
>
You may receive `you are not authorized to perform xxx` or other prompts for "no access" while accessing the SCF Console to view function monitoring or execution information.
You can create a custom policy as instructed in the [CAM documentation](https://intl.cloud.tencent.com/document/product/598/32677) or configure two preset policies for fast authorization by following the steps below:
1. Log in to the CAM Console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. Select **Authorize** to the right of the row of the user for whom to add a policy.
3. In the "Associate Policy" window that pops up, check one of the preset policies in the table below and click **OK** to complete the authorization:
This document uses the `QcloudSCFFullAccess` preset policy as an example, and you can choose an appropriate policy based on your actual needs.
<table>
	<tr>
	<th>Preset Policy</th><th>Purpose</th>
	</tr>
	<tr>
	<td>QcloudSCFFullAccess</td><td>Grants full access to SCF and other relevant resources</td>
	</tr>
	<tr>
	<td>QcloudSCFReadOnlyAccess</td><td>Grants read-only access to SCF and other relevant resources</td>
	</tr>
</table>


## Notes on User Policy Update<spoan id="Strategy"></span>
SCF improved the preset permission policies in December 2019. The preset policies `QcloudSCFFullAccess` and `QcloudSCFReadOnlyAccess` were modified, and the `QcloudAccessForScfRole` policy was added for the configuration role `SCF_QcsRole`. For more information, please see [Notes on User Policy Update](https://intl.cloud.tencent.com/document/product/583/31444).

