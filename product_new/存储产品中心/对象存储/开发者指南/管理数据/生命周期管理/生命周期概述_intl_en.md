COS supports object-based lifecycle configuration. By sending specific description language to a bucket, COS can automatically perform predefined actions on objects to which a rule is applied. 

> A lifecycle can be set to as long as 3,650 days.

## Use Cases

### Log Record

With corresponding lifecycle configuration, log data stored in COS can be automatically archived after 30 days or deleted after 2 years.

### Data Transition

Hot data is frequently accessed in a short period of time after the upload, but then is less or not accessed at all after some time. Therefore, you may set the lifecycle rules to store the data uploaded 30 days ago in Standard_IA storage class and store the data uploaded 60 days ago in Archive storage class. This process is called data transition.

### Archive Management

When you use COS for file archive management, you need to save all historical versions of files for a long time in accordance with compliance requirements in financial, medical, and other industries. In this case, you can configure the lifecycle to transition and store the historical versions of files in Archive storage class.

## Support Descriptions

### Supported Actions

- Data transition: transitions existing objects to the STANDARD_IA, ARCHIVE or DEEP ARCHIVE storage class after a specified time period.
- Deletion after expiration: automatically delete objects after their specified expiration time.

### Supported Resources

- Specified based on prefixes: objects with different prefixes are processed according to applicable rules.
- Versioning-enabled objects: you can manage the current and historical versions of objects separately as needed.
- Objects with delete markers: when all old versions of objects are cleared, you can specify to remove their delete markers.
- Incomplete multipart uploads: process incomplete multipart upload tasks.

### Supported Time Conditions

- Based on the number of days: specify in how many days after an object is last modified the corresponding action will be performed.
- Based on a specific date: specify a date when the corresponding action will be performed.

## Notes

### Data Transition

#### Supported Regions

This operation is supported for public cloud regions.

#### One-way Transition

From the hottest to the coldest, COS storage classes are STANDARD > STANDARD_IA > ARCHIVE > DEEP ARCHIVE. Objects can be transitioned only from a hotter storage class to a colder one, such as from STANDARD to ARCHIVE, but not vice versa. To restore your data from a colder storage class to a hotter one, you can only call  [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) (for other storage classes than ARCHIVE and DEEP ARCHIVE), or [POST Object restore ](https://intl.cloud.tencent.com/document/product/436/12633) (only for ARCHIVE and DEEP ARCHIVE).

#### Eventual Consistency

If multiple conflicting rules (excluding deletion after expiration) are configured for the same set of objects, these rules will be performed in a chronological order. The objects will be transitioned to the coldest storage class according to the rules.
> It is strongly recommended that you do not configure conflicting lifecycle rules for the same set of objects in COS, because this may result in additional fees.

### Deletion after Expiration

#### How it Works

When an object matches the specified lifecycle rule of deletion after expiration, COS will add it to the async deletion queue. There will be a delay in the actual deletion. You can get the current status of the object by performing a GET or HEAD Object operation.

#### Eventual Consistency

If multiple conflicting rules are configured for the same set of objects, these rules will be performed in chronological order in accordance with expiration time. **Deletion after expiration takes precedence over before transition from one storage class to another**.
> It is strongly recommended that you do not configure conflicting lifecycle rules for the same set of objects in COS, because this may result in additional fees.

### Cost Considerations

#### Execution Instructions

Once triggered, actions configured at any time will always be executed at 00:00 Beijing time (GMT+8) the next day in COS. As objects need to be added to an async queue before execution, for objects uploaded after the configuration time that are matched by a rule, actions will be performed on them before 00:00 the next day.

When any accident occurs or there are too many objects in the bucket, lifecycle execution may fail. For failures due to other reasons, execute GET or HEAD Object to get the current object status.

Tencent Cloud cannot provide an accurate bill unless the lifecycle execution is completed.

#### Time-insensitivity

Please note that the minimum storage duration is 30 days, 90 days, and 180 days for STANDARD_IA, ARCHIVE and DEEP ARCHIVE storage classes, respectively. No additional storage fees will be incurred for the transition or delete action itself. COS will ignore lifecycle configurations less than 30/60 days, and perform only correct configurations upon your request.

For example, if an object in STANDARD_IA storage class is transitioned before 30 days, it will start incurring ARCHIVE storage fees on the transition day and continue incurring STANDARD_IA storage fees until the 30th day. Another example is that if an archived object is deleted upon expiration before it is stored for 90 days, it will continue incurring ARCHIVE storage fees until the 90th day. It works the same way with DEEP ARCHIVE.

#### Size-insensitivity

There is a minimum allowed object size in the STANDARD_IA, ARCHIVE, and DEEP ARCHIVE storage classes. For example, if an object below 64 KB is uploaded to the STANDARD_IA storage class, it will be calculated as 64 KB. COS will not check the file size; instead, it will transition objects only according to the specified rule.
