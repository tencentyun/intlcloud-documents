CBS replication is a feature that asynchronously replicates data between disks across regions or across zones within the same region. You can use this feature to implement disaster recovery for critical business, implement high-available infrastracture to improve business continuity.

## Use scenarios

### Disaster recovery scenario
When CBS replication is activated between two disks, if the primary disk in a replication pair fails, you can use the failover feature to switch the primary and secondary disks over. After switchover, the the new primary disk (original secondary disk) is available to be attached to an instance to recover business.

### Cross-region migration scenario
If you want to migrate your business data across regions, you can use the reverse replication sub-feature, instead of the image or snapshot replication feature.

## Feature description
CBS replication feature allows data to be asynchronously replicated from a disk(primary disk) to another disk (secondary disk) that has the same specifications. The primary and secondary disks can reside in different zones within the same region or reside in different regions. If the primary disk fails, you can fail over to the secondary disk. After the primary disk recovers, you can restore data to the primary disk from the secondary disk.

## Billing
You are charged for the use of CBS replication on subscription and must pay the bandwidth fees.

## Precautions
Support Regions/AZs: Southeast Asia (Bangkok) Zone 1, Northeast Asia (Seoul)
Replication gap between primary and secondary disks: 15 minute
Replication pairs can be created for a disk: 1
primary disk: must be premium disk or SSD disk
secondary disk:	A secondary disk must be the same disk type and size as the associated primary disk

The limits described in the following table apply to primary and secondary disks when you associate them in a replication pair.
| Operations              | Primary Disk  | Secondary Disk |
| ------------------ | ------- | ---------------------------------------- |
| Attach disk     | √ | ×|
| Detach disk      | √ | ×|
| Disk read/write IO |  √ | ×|
| Use as system disk|  × | ×|
| Delete disk |  × | ×|
| Resize disk |  × | ×|
| create image| × | ×|
| create snapshot| × | ×|
| Restore from snapshot|  × | ×|
| Change disk type|  × | ×|
| Encrypt disk|  × | ×|
| Multi-attach disk|  × | ×|

## Create replication pair

### Prerequisites
The primary disk and the secondary disk in different AZs/Regions must be created. Note that the two disks must be the same type and size. 
### Procedure
1. Log in to the CBS console.
2. Click on the primary disk to the detail page, choose CBS Replication tab
3. Click Create Replication Pair button
4. On the new page, choose the destination AZ/Region where the secondary disk is located.Then select the ID of secondary disk.Enter the name and description of this pair.
5. Confirm the replication pair configurations, then click OK button.
6. After complete the payment, you can back to the detail page to view the replication pair.
7. If the replication pair is no longer useful, click Delete button to release the connection between the primary and secondary disks.