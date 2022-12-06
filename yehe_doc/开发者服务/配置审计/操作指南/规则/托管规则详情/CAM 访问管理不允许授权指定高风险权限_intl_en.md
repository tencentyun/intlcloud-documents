**Description:** Checks whether CAM authorizes specified high-risk permissions.
**Compliance check logic:** If no specified high-risk permission is authorized to CAM users, user groups, and roles, this rule is compliant.
**Rule ID:** `cam-user-risky-policy-bound`
**Risk level:** Low
**Supported resource types:** `QCS::CAM::User`, `QCS::CAM::Group`, `QCS::CAM::Role`
**Trigger type:** Periodic, 24 hours
**Keywords:** User, user group, role, policy
**Input parameters:**
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Default Value</th>
<th>Relationship</th>
</tr>
</thead>
<tbody>
<tr>
<td >policies</td>
<td>AdministratorAcces</td>
<td>Include</td>
</tr>
</table>
