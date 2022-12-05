**Description:** Checks whether CAM users' keys are changed within a specified period of time.
**Compliance check logic:** If CAM users' keys is changed within a specified period of time, this rule is complaint.
**Rule ID:** `cam-user-ak-rotated`
**Risk level:** High
**Supported resource types:** `QCS::CAM::User`
**Trigger type:** Periodic, 24 hours
**Keywords:** User, key
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
