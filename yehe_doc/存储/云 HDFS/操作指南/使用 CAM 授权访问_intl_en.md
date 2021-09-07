## Preset Policies for CHDFS
The preset authorization policies for CHDFS are as follows:

| Policy | Description |
|---------|---------|
| QcloudCHDFSReadOnlyAccess | Read-only access to CHDFS | 
| QcloudCHDFSFullAccess | Permission to manage CHDFS |


#### Authorized operations in CHDFS

| **Action**                 | **Resource**                                                  | **Description**             |
| -------------------------- | ------------------------------------------------------------ | -------------------- |
| chdfs:CreateFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/*       | Creates CHDFS instance            |
| chdfs:DeleteFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Deletes CHDFS instance            |
| chdfs:ModifyFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Modifies CHDFS instance attribute        |
| chdfs:DescribeFileSystem   | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Views CHDFS instance details    |
| chdfs:DescribeFileSystems  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Views CHDFS instance list        |
| chdfs:CreateMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Creates mount point            |
| chdfs:DeleteMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | Deletes mount point           |
| chdfs:ModifyMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | Modifies mount point attribute      |
| chdfs:DescribeMountPoint   | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | Views mount point details   |
| chdfs:DescribeMountPoints  | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | Views mount point list       |
| chdfs:AssociateAccessGroups   | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | Associates permission group list  |
| chdfs:DisassociateAccessGroups| qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | Disassociates permission group list |
| chdfs:CreateAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:vpc/${vpc-id}<br>qcs::chdfs:${region-id}:uin/${account-uin}:unVpcId/${unVpcId}     | Creates permission group           |
| chdfs:DeleteAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | Deletes permission group           |
| chdfs:ModifyAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | Modifies permission group attribute       |
| chdfs:DescribeAccessGroup  | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | Views permission group details  |
| chdfs:DescribeAccessGroups | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | Views permission group list       |
| chdfs:CreateAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id}  | Batch creates permission rules     |
| chdfs:DeleteAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessrule/${access-rule-id} | Batch deletes permission rules     |
| chdfs:ModifyAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessrule/${access-rule-id} | Batch modifies the attribute of permission rules |
| chdfs:DescribeAccessRules  | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | Views permission rule list     |
| chdfs:CreateLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | Batch creates lifecycle rules |
| chdfs:DeleteLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:lifecyclerule/${life-cycle-rule-id} | Batch deletes lifecycle rules |
| chdfs:ModifyLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:lifecyclerule/${life-cycle-rule-id} | Batch modifies the attribute of lifecycle rules |
| chdfs:DescribeLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Views lifecycle rule list  |
| chdfs:CreateRestoreTasks    | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | Batch creates restoration tasks    |
| chdfs:DescribeRestoreTasks  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Views restoration task list    |
| chdfs:ModifyResourceTags    | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | Modifies resource tag list    |
| chdfs:DescribeResourceTags  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | Views resource tag list     |


## Sample CHDFS Authorization Policies
Below is a sample policy for granting a sub-account the read-only access to the CHDFS control system:
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": [
			"name/chdfs:Describe*"
		],
		"resource": [
	 		"*"
		]
	}]
}
```

Below is a sample policy for granting a sub-account the permission to view CHDFS:
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": [
 			"name/chdfs:DescribeFileSystem"
  		],
		"resource": [
			"qcs::chdfs::uin/ownerUin:filesystem/fileSystemId"
		]
	}]
}
```
