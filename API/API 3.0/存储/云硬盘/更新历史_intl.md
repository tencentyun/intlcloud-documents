## Release 14

Release time: 2019-06-14 08:52:05

This release contains:

Improves existing documents

New API:

* [ModifyAutoSnapshotPolicyAttribute](/document/api/362/35482)

## Release 13

Release time: 2019-05-30 21:22:47

This release contains:

Improves existing documents

Modified API:

* [CreateDisks](/document/api/362/16312)
	* **Deleted input parameter: **DeleteWithInstance
* [DetachDisks](/document/api/362/16316)
	* New input parameter added: InstanceId

## Release 12

Release time: 2019-05-09 17:16:40

This release contains:

Improves existing documents

Modified API:

* [CreateDisks](/document/api/362/16312)
	* New input parameter: Shareable

## Release 11

Release time: 2019-04-12 11:13:22

This release contains:

Improves existing documents

Modified data structure:

* [Disk](/document/api/362/15669#Disk)
	* New members: Shareable, InstanceIdList

## Release 10

Release time: 2019-03-08 17:29:54

This release contains:

Improves existing documents

New APIs:

* [BindAutoSnapshotPolicy](/document/api/362/33559)
* [CreateAutoSnapshotPolicy](/document/api/362/33558)
* [DeleteAutoSnapshotPolicies](/document/api/362/33557)
* [DescribeAutoSnapshotPolicies](/document/api/362/33556)
* [DescribeDiskAssociatedAutoSnapshotPolicy](/document/api/362/33555)
* [UnbindAutoSnapshotPolicy](/document/api/362/33554)

New data structures:

* [AutoSnapshotPolicy](/document/api/362/15669#AutoSnapshotPolicy)
* [Policy](/document/api/362/15669#Policy)

## Release 9

Release time: 2019-02-22 14:29:13

This release contains:

Improves existing documents

Modified API:

* [ModifyDiskAttributes](/document/api/362/15659)
	* New input parameter: DiskType

New data structure:

* [Image](/document/api/362/15669#Image)

Modified data structure:

* [Placement](/document/api/362/15669#Placement)
	* New members: CdcId, CageId, CdcName
* [Snapshot](/document/api/362/15669#Snapshot)
	* New members: Images, ImageCount
	* **Deleted member: **ImageIds

## Release 8

Release time: 2019-01-10 20:01:16

This release contains:

Improves existing documents

New API:

* [DescribeSnapshotOperationLogs](/document/api/362/32490)

New data structure:

* [SnapshotOperationLog](/document/api/362/15669#SnapshotOperationLog)

Modified data structures:

* [Disk](/document/api/362/15669#Disk)
	* New members: Migrating, MigratePercent
* [Price](/document/api/362/15669#Price)
	* New member: UnitPriceDiscount
* [Snapshot](/document/api/362/15669#Snapshot)
	* New member: ImageIds

## Release 7

Release time: 2018-10-26 14:34:03

This release contains:

Improves existing documents

New API:

* [DescribeDiskOperationLogs](/document/api/362/30162)

Modified API:

* [CreateDisks](/document/api/362/16312)
	* New input parameter: DeleteWithInstance
* [DescribeInstancesDiskNum](/document/api/362/16311)
	* New output parameter: AttachDetail
	* **Deleted output parameters: **AttachedDiskCount, MaxAttachCount
* [InquiryPriceRenewDisks](/document/api/362/16317)
	* **Modified output parameter: **DiskPrice
* [InquiryPriceResizeDisk](/document/api/362/16320)
	* **Modified output parameter: **DiskPrice

New data structures:

* [AttachDetail](/document/api/362/15669#AttachDetail)
* [DiskOperationLog](/document/api/362/15669#DiskOperationLog)
* [PrepayPrice](/document/api/362/15669#PrepayPrice)

Modified data structure:

* [Disk](/document/api/362/15669#Disk)
	* New member: DifferDaysOfDeadline
	* **Modified member: **ReturnFailCode

## Release 6

Release time: 2018-07-26 12:20:04

This release contains:

Improves existing documents

Modified API:

* [ModifyDiskAttributes](/document/api/362/15659)
	* New input parameter: DeleteWithInstance

Modified data structure:

* [Disk](/document/api/362/15669#Disk)
	* New member: DeleteWithInstance

## Release 5

Release time: 2018-06-28 15:15:08

This release contains:

Improves existing documents

Modified API:

* [AttachDisks](/document/api/362/16313)
	* New input parameter: DeleteWithInstance

Modified data structure:

* [Price](/document/api/362/15669#Price)
	* New members added: UnitPrice, ChargeUnit

## Release 4

Release time: 2018-06-21 14:34:22

This release contains:

Improves existing documents

Modified API:

* [CreateDisks](/document/api/362/16312)
	* New input parameter: Tags

## Release 3

Release time: 2018-05-31 14:45:35

This release contains:

Improves existing documents

New data structures:

* [Tag](/document/api/362/15669#Tag)

Modified data structure:

* [Disk](/document/api/362/15669#Disk)
	* New member: Tags

## Release 2xi

Release time: 2018-05-24 17:08:50

This release contains:

Improves existing documents

Modified API:

* [DescribeDiskConfigQuota](/document/api/362/16318)
	* New input parameter: DiskTypes
	* **Deleted input parameter:** DiskType

Modified data structure:

* [Snapshot](/document/api/362/15669#Snapshot)
	* New members: CopyingToRegions, CopyFromRemote

## Release 1

Release time: 2018-04-24

This release contains:

Improves existing documents

New APIs:

* [ApplySnapshot](/document/api/362/15643)
* [AttachDisks](/document/api/362/16313)
* [CreateDisks](/document/api/362/16312)
* [CreateSnapshot](/document/api/362/15648)
* [DeleteSnapshots](/document/api/362/15645)
* [DescribeDiskConfigQuota](/document/api/362/16318)
* [DescribeDisks](/document/api/362/16315)
* [DescribeInstancesDiskNum](/document/api/362/16311)
* [DescribeSnapshots](/document/api/362/15647)
* [DetachDisks](/document/api/362/16316)
* [InquiryPriceCreateDisks](/document/api/362/16314)
* [InquiryPriceRenewDisks](/document/api/362/16317)
* [InquiryPriceResizeDisk](/document/api/362/16320)
* [ModifyDiskAttributes](/document/api/362/15659)
* [ModifyDisksRenewFlag](/document/api/362/15668)
* [ModifySnapshotAttribute](/document/api/362/15650)
* [RenewDisk](/document/api/362/16319)
* [ResizeDisk](/document/api/362/16310)
* [TerminateDisks](/document/api/362/16321)

New data structures:

* [Disk](/document/api/362/15669#Disk)
* [DiskChargePrepaid](/document/api/362/15669#DiskChargePrepaid)
* [DiskConfig](/document/api/362/15669#DiskConfig)
* [Filter](/document/api/362/15669#Filter)
* [Placement](/document/api/362/15669#Placement)
* [Price](/document/api/362/15669#Price)
* [Snapshot](/document/api/362/15669#Snapshot)

