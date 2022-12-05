**Description:** Checks whether CAM users log in within a specified period of time.
**Compliance check logic:** If CAM users log in within a specified period of time, this rule is complaint.
**Rule ID:** `cam-user-logged-in`
**Risk level:** Medium
**Supported resource types:** `QCS::CAM::User`
**Trigger type:** Periodic, 24 hours
**Keywords:** User, login
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
<td >days</td>
<td>90</td>
<td>Less than or equal to</td>
</tr>
</table>


