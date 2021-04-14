## Release 14

Release time: 2019-06-14 08:52:05

This release contains:

Improves existing documents

New API:

* [ModifyAutoSnapshotPolicyAttribute](https://cloud.tencent.com/document/api/362/35482)

## Release 13

Release time: 2019-05-30 21:22:47

This release contains:

Improves existing documents

Modified API:

* [CreateDisks](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16312)
	* **Deleted input parameter: **DeleteWithInstance
* [DetachDisks](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16316)
	* New input parameter added: InstanceId

## Release 12

Release time: 2019-05-09 17:16:40

This release contains:

Improves existing documents

Modified API:

* [CreateDisks](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16312)
	* New input parameter: Shareable

## Release 11

Release time: 2019-04-12 11:13:22

This release contains:

Improves existing documents

Modified data structure:

* [Disk](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Disk)
	* New members: Shareable, InstanceIdList

## Release 10

Release time: 2019-03-08 17:29:54

This release contains:

Improves existing documents

New APIs:

* [BindAutoSnapshotPolicy](https://cloud.tencent.com/document/api/362/33559)
* [CreateAutoSnapshotPolicy](https://cloud.tencent.com/document/api/362/33558)
* [DeleteAutoSnapshotPolicies](https://cloud.tencent.com/document/api/362/33557)
* [DescribeAutoSnapshotPolicies](https://cloud.tencent.com/document/api/362/33556)
* [DescribeDiskAssociatedAutoSnapshotPolicy](https://cloud.tencent.com/document/api/362/33555)
* [UnbindAutoSnapshotPolicy](https://cloud.tencent.com/document/api/362/33554)

New data structures:

* [AutoSnapshotPolicy](https://cloud.tencent.com/document/api/362/15669#AutoSnapshotPolicy)
* [Policy](https://cloud.tencent.com/document/api/362/15669#Policy)

## Release 9

Release time: 2019-02-22 14:29:13

This release contains:

Improves existing documents

Modified API:

* [ModifyDiskAttributes](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15659)
	* New input parameter: DiskType

New data structure:

* [Image](https://cloud.tencent.com/document/api/362/15669#Image)

Modified data structure:

* [Placement](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Placement)
	* New members: CdcId, CageId, CdcName
* [Snapshot](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Snapshot)
	* New members: Images, ImageCount
	* **Deleted member: **ImageIds

## Release 8

Release time: 2019-01-10 20:01:16

This release contains:

Improves existing documents

New API:

* [DescribeSnapshotOperationLogs](https://cloud.tencent.com/document/api/362/32490)

New data structure:

* [SnapshotOperationLog](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#SnapshotOperationLog)

Modified data structures:

* [Disk](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Disk)
	* New members: Migrating, MigratePercent
* [Price](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Price)
	* New member: UnitPriceDiscount
* [Snapshot](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Snapshot)
	* New member: ImageIds

## Release 7

Release time: 2018-10-26 14:34:03

This release contains:

Improves existing documents

New API:

* [DescribeDiskOperationLogs](https://cloud.tencent.com/document/api/362/30162)

Modified API:

* [CreateDisks](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16312)
	* New input parameter: DeleteWithInstance
* [DescribeInstancesDiskNum](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16311)
	* New output parameter: AttachDetail
	* **Deleted output parameters: **AttachedDiskCount, MaxAttachCount
* [InquiryPriceRenewDisks](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16317)
	* **Modified output parameter: **DiskPrice
* [InquiryPriceResizeDisk](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16320)
	* **Modified output parameter: **DiskPrice

New data structures:

* [AttachDetail](https://cloud.tencent.com/document/api/362/15669#AttachDetail)
* [DiskOperationLog](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#DiskOperationLog)
* [PrepayPrice](https://cloud.tencent.com/document/api/362/15669#PrepayPrice)

Modified data structure:

* [Disk](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Disk)
	* New member: DifferDaysOfDeadline
	* **Modified member: **ReturnFailCode

## Release 6

Release time: 2018-07-26 12:20:04

This release contains:

Improves existing documents

Modified API:

* [ModifyDiskAttributes](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15659)
	* New input parameter: DeleteWithInstance

Modified data structure:

* [Disk](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Disk)
	* New member: DeleteWithInstance

## Release 5

Release time: 2018-06-28 15:15:08

This release contains:

Improves existing documents

Modified API:

* [AttachDisks](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16313)
	* New input parameter: DeleteWithInstance

Modified data structure:

* [Price](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Price)
	* New members added: UnitPrice, ChargeUnit

## Release 4

Release time: 2018-06-21 14:34:22

This release contains:

Improves existing documents

Modified API:

* [CreateDisks](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16312)
	* New input parameter: Tags

## Release 3

Release time: 2018-05-31 14:45:35

This release contains:

Improves existing documents

New data structures:

* [Tag](https://cloud.tencent.com/document/api/362/15669#Tag)

Modified data structure:

* [Disk](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Disk)
	* New member: Tags

## Release 2xi

Release time: 2018-05-24 17:08:50

This release contains:

Improves existing documents

Modified API:

* [DescribeDiskConfigQuota](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16318)
	* New input parameter: DiskTypes
	* **Deleted input parameter:** DiskType

Modified data structure:

* [Snapshot](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Snapshot)
	* New members: CopyingToRegions, CopyFromRemote

## Release 1

Release time: 2018-04-24

This release contains:

Improves existing documents

New APIs:

* [ApplySnapshot](https://cloud.tencent.com/document/api/362/15643)
* [AttachDisks](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16313)
* [CreateDisks](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16312)
* [CreateSnapshot](https://cloud.tencent.com/document/api/362/15648)
* [DeleteSnapshots](https://cloud.tencent.com/document/api/362/15645)
* [DescribeDiskConfigQuota](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16318)
* [DescribeDisks](https://cloud.tencent.com/document/api/362/16315)
* [DescribeInstancesDiskNum](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16311)
* [DescribeSnapshots](https://cloud.tencent.com/document/api/362/15647)
* [DetachDisks](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16316)
* [InquiryPriceCreateDisks](https://cloud.tencent.com/document/api/362/16314)
* [InquiryPriceRenewDisks](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16317)
* [InquiryPriceResizeDisk](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/16320)
* [ModifyDiskAttributes](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15659)
* [ModifyDisksRenewFlag](https://cloud.tencent.com/document/api/362/15668)
* [ModifySnapshotAttribute](https://cloud.tencent.com/document/api/362/15650)
* [RenewDisk](https://cloud.tencent.com/document/api/362/16319)
* [ResizeDisk](https://cloud.tencent.com/document/api/362/16310)
* [TerminateDisks](https://cloud.tencent.com/document/api/362/16321)

New data structures:

* [Disk](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Disk)
* [DiskChargePrepaid](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#DiskChargePrepaid)
* [DiskConfig](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#DiskConfig)
* [Filter](https://cloud.tencent.com/document/api/362/15669#Filter)
* [Placement](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Placement)
* [Price](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Price)
* [Snapshot](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/362/15669#Snapshot)

