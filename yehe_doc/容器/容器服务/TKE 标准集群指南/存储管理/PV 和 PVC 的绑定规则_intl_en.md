## PV Status Introduction
<table>
	<tr>
	<th>PV Status</th><th>Description</th>
	</tr>
	<tr>
	<td>Available</td>
	<td>When a created PV is not bound with a PVC, the PV is in the `Available` status.</td>
	</tr>
	<tr>
	<td>Bound</td>
	<td>After a PVC is bound with a PV, the PVC is in the `Bound` status.</td>
	</tr>
	<tr>
	<td>Released</td>
	<td>For a PV with the Retain reclaim policy, after its bound PVC is deleted, the status of the PV will change from `Bound` to `Released`. <br><b>Note: </b>for a PV in the `Released` status, you need to manually delete the claimRef field in the YAML configuration file so that the PV can be successfully bound with a new PVC.</td>
	</tr>
</table>


## PVC Status Introduction
<table>
	<tr>
	<th>PVC Status</th><th>Description</th>
	</tr>
	<tr>
	<td>Pending</td>
	<td>When no eligible PV can be bound with a PVC, the PVC is in the `Pending` status.</td>
	</tr>
	<tr>
	<td>Bound</td>
	<td>After a PVC is bound with a PV, the PVC is in the `Bound` status.</td>
	</tr>
</table>

## Binding Rules
When binding a PVC with a PV, consider the following parameters to check whether PVs that meet the binding rules are available in the current cluster.
<table>
	<tr>
	<th>Parameter</th> <th>Description</th>
	</tr>
	<tr>
	<td>VolumeMode</td>
	<td>Specifies whether the volume is of the `FileSystem` type or `Block` type. The PV to be selected must match the PVC in terms of the VolumeMode label.</td>
	</tr>
	<tr>
	<td>Storageclass</td>
	<td>The `storageclass` of the PV and PVC must be the same (or both empty).</td>
	</tr>
	<tr>
	<td>AccessMode</td>
	<td>Specifies the volume access mode. The AccessMode of the PV and that of the PVC must be the same.</td>
	</tr>
	<tr>
	<td>Size</td>
	<td>Specifies the storage capacity of the volume. The specified capacity of the PVC must be less than or equal to that of the PV. If multiple eligible PVs are available, bind the PV with the smallest capacity to the PVC.</td>
	</tr>
</table>

>? After a PVC is created, the system will bind an eligible PV with the PVC based on the above parameters. If the PV resources in the current cluster are insufficient, the system will dynamically create an eligible PV and bind it with the PVC.

## StorageClass Selection and PV/PVC Binding
The following figure shows the principle of StorageClass selection and PV/PVC binding on TKE platform:
![](https://main.qcloudimg.com/raw/9eb0904f597763938a8c3af02586aaf6.png)







