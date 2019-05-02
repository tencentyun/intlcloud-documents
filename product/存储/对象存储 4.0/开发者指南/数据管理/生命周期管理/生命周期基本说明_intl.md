On COS, you can configure the lifecycle based on object. By sending specific description language to a bucket, COS automatically performs predefined actions on objects to which a rule applies.

>?A lifecycle can be set to as long as 3,650 days.

## Use Cases

### Log record

With lifecycle configure, log data stored on COS can be automatically archived after 30 days or deleted after 2 years.

### Stratified data storage

Hot data is frequently accessed in a short period of time after being uploaded, and then less accessed or no longer accessed after a while. You can set the lifecycle rules to this: store the data uploaded 30 days ago to COS Infrequent Access, and store the data uploaded 60 days ago to Archive Storage.

### Archive management

When you use COS for file archive management, you need to save all historical versions of files for a long time in compliance with financial, medical, and other requirements. In this case, you can configure the lifecycle to store the historical versions of files to Archive Storage.

## Support for Server-side Encryption

### Supported actions

- Transition: Transition objects to STANDARD_IA storage or ARCHIVE storage after a specified time of period.
- Expiration: Automatically delete objects after they reach the specified expiration time.

### Supported resources

- Prefixes: Objects with certain prefixes are processed according to relevant rules.
- Versions: Objects other than the current version are processed according to relevant rules.
- Deletion markers: When the old versions of objects are cleared, you can specify to remove the deletion markers.
- Incomplete multipart upload tasks: Process incomplete multipart upload tasks.

### Supported time conditions

- Based on number of days: Specify after how many days since an object was last modified that an action will occur.
- Based on a specific date: Specify at a specific date that an action will occur.

## Notes

### Transition from one storage class to another

#### Supported zones

You can transition objects to Archive Storage only in the following zones:
Beijing (ap-beijing), Shanghai (ap-shanghai), Guangzhou (ap-guangzhou), Chengdu (ap-chengdu), Chongqing (ap-chongqing)

#### One-way transition

Objects can only be transitioned in one-way, i.e., from STANDARD storage to STANDARD_IA storage and then to ARCHIVE storage, or from STANDARD storage to ARCHIVE storage. Reverse transition is not allowed. To transition objects from cold storage to hot storage, you need to call [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) (for non-ARCHIVE class) or [POST Object restore ](https://cloud.tencent.com/document/product/436/12633) (for ARCHIVE class).

#### Eventual consistency

If multiple conflicting rules (excluding deletion after expiration) are configured for the same set of objects, these rules will be performed in chronological order. The objects will be tiered down to the coldest storage according to the rules.
>!Tencent Cloud COS recommend you not configure conflicting lifecycle rules for the same set of objects, because this may result in different cost performance.

### Deletion after expiration

#### How it works

When an object matches the specified lifecycle rule of deletion after expiration, Tencent Cloud will add the object to the asynchronous deletion queue. This will cause certain delay in actual deletion. You can get the current status of the object by performing GET or HEAD Object action.

#### Eventual consistency

If multiple conflicting rules are configured for the same set of objects, these rules will be performed in chronological order in accordance with expiration time. **Always perform deletion after expiration before transition from one storage class to another**.
>!Tencent Cloud COS recommend you not configure conflicting lifecycle rules for the same set of objects, because this may result in different cost performance.

### Cost considerations

#### Execution instructions

Once triggered, actions configured at any time will always be executed at 00:00 the next day Beijing time (GMT+8) on Tencent Cloud COS. As objects need to be added to an asynchronous queue before execution, for those who match the rules after the configuration time, actions are performed before 24:00 the next day.

When any accident occurs or there are too many objects in the bucket, lifecycle execution may fail. For failures due to other reasons, execute GET or HEAD Object to get the current object status.

Tencent Cloud cannot provide an accurate bill unless the lifecycle execution is completed.

#### Time-insensitive

We will not charge additional storage fees for object storage transition and deletion unless the object is stored in STANDARD_IA storage or ARCHIVE storage for at least 30 days and 60 days, respectively. Tencent Cloud will not check lifecycle configurations less than 30/60 days. We will execute correct configurations according to your requirements.

For example, if you transition an object stored in STANDARD_IA storage (for less than 30 days) to ARCHIVE storage, in addition to the new ARCHIVE storage fee, you also need to pay the STANDARD_IA storage fee till the 30-day STANDARD_IA storage period ends.

For example, if you delete an expired object stored in STANDARD_IA storage for less than 60 days, you need to pay the ARCHIVE storage fee till the 60-day ARCHIVE storage period ends.

#### Size-insensitive

A lower size limit is defined for files to be uploaded to STANDARD_IA storage and ARCHIVE storage. For example, a file smaller than 64 KB is counted as 64 KB when uploaded to STANDARD_IA storage. Tencent Cloud will not check your file size. We will perform object transition action according to specific rules. 

