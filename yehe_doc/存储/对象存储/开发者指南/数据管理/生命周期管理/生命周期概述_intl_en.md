# Overview

COS supports object-based lifecycle configuration. If you set rules for a bucket, COS can automatically perform predefined operations on objects to which the rule is applied.

>?
>- A lifecycle can be set to as long as 3,650 days.
>- Up to 1,000 lifecycle rules can be added for each bucket.

## Use Cases

### Log record

With lifecycle configured, logs stored on COS can be automatically archived after 30 days or deleted after 2 years.

### Hot/Cold data tiering

Hot data is frequently accessed in a short period of time after the upload, but then is less or not accessed at all after some time. Therefore, you can set the lifecycle rules to store the data uploaded 30 days ago in the STANDARD_IA storage class and data uploaded 60 days ago in ARCHIVE. This process is called data transition.

### Archive management

When you use COS for file archive management, you need to save all historical versions of files for a long time according to the compliance requirements in financial, medical, and other industries. In this case, you can configure the lifecycle to transition and store the historical versions of files in the ARCHIVE storage class.

## Configuration Items

### Operations

- Data transition: transitions objects to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE after a specified period.
- Deletion upon expiration: deletes objects automatically after they expire.

### Objects

- Prefixes: Rules are applied to objects with specified prefixes.
- Versioning: Rules are applied to objects with non-current versions.
- Delete markers: When all historical versions of objects are cleared, you can specify to remove the delete marker.
- Incomplete multipart uploads: processes incomplete multipart upload jobs.

### Time

- Based on the number of days: You can specify in how many days after an object is last modified to perform the corresponding operation.
- Based on a specific date: You can specify a date to perform the corresponding operation.

## Directions

### Data transition

#### Supported regions

Only public cloud regions are supported.

#### One-way transition

Data transition is one-way (STANDARD > STANDARD_IA > ARCHIVE, or STANDARD > ARCHIVE) and cannot be in the reversed way. You can only call [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) (for non-ARCHIVED/DEEP ARCHIVE only) or [POST Object restore ](https://intl.cloud.tencent.com/document/product/436/12633) (for ARCHIVE and DEEP ARCHIVE only) to restore data from a colder storage class to a hotter one.

#### Eventual consistency

If multiple conflicting rules (excluding rules deleted due to expiration) are configured for a set of objects, COS will transition the objects to the coldest storage class first. For example, if a set of objects is configured with both **transition to STANDARD_IA** and **transition to ARCHIVE**, the **transition to ARCHIVE** rule will be performed first.
>!It is strongly recommended that you do not configure conflicting lifecycle rules for the same set of objects in COS, because this may result in different fees.

### Deletion upon expiration

#### How it works

When an object matches the specified lifecycle rule of deletion upon expiration, Tencent Cloud will add the object to the asynchronous deletion queue. There may be a certain delay in actual deletion. You can get the current status of the object by performing GET or HEAD Object operation.

#### Eventual consistency
If multiple conflicting rules are configured for the same set of objects, the rule that will expire first will be performed first. **Deletion upon expiration will be performed before the transition**.

>! It is strongly recommended that you do not configure conflicting lifecycle rules for the same set of objects in COS, because this may result in different fees.
>

### Cost considerations

#### Execution instructions

Once triggered, actions configured at any time will always be executed at 00:00 the next day Beijing time (GMT+8) on Tencent Cloud COS. As objects need to be added to an asynchronous queue before execution, for those who match the rules after the configuration time, actions are performed before 24:00 the next day.

For example, you configured a lifecycle rule at 15:00 on the 1st day of the month to delete files one day or longer after they are modified. Then, at 00:00 on the 2nd day, the lifecycle task scans for files that were modified over one day ago and deletes them. Files uploaded on the 1st day will not be deleted at 00:00 on the 2nd day, as the time elapsed since their modification is less than one day. Instead, these files will be deleted at 00:00 on the 3rd day.

When an accident occurs or there are too many objects in the bucket, lifecycle execution may fail. For failures due to other reasons, perform the GET or HEAD Object operation to get the current object status.

Tencent Cloud cannot provide an accurate bill unless the lifecycle execution is completed.

#### Time-insensitive

Please note that the minimum storage duration is 30 days, 90 days, and 180 days for the STANDARD_IA/INTELLIGENT TIERING, ARCHIVE, and DEEP ARCHIVE storage classes, respectively. No additional storage fees will be incurred for the transition or delete action itself. COS will ignore lifecycle configurations less than 30/90/180 days, and perform only correct configurations upon your request.

For example, if an object in STANDARD_IA is transitioned before 30 days, it will start incurring ARCHIVE storage fees on the transition day and continue incurring STANDARD_IA storage fees until the 30th day. Another example is that if an archived object is deleted upon expiration before it is stored for 90 days, it will continue incurring ARCHIVE storage fees until the 90th day. It works the same way with DEEP ARCHIVE.

#### Size-insensitive

There is a minimum size limit for objects in the STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, and DEEP ARCHIVE storage classes. For example, if an object smaller than 64 KB is uploaded to the STANDARD_IA storage class, it will be calculated as 64 KB. COS will not check the file size and will transition objects according to the specified rule. 

>?Zero-byte objects will not be transitioned.
