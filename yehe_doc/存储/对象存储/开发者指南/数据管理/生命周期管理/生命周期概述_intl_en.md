## Overview

COS supports object-based lifecycle configuration. You can use lifecycle rules to define operations to perform on applicable objects.

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
You need to configure the following elements to create a lifecycle rule:

### Objects
The data to be hit during lifecycle execution. You can customize the lifecycle's scope and data types covered within the scope. During lifecycle execution, the specified scope will be scanned, and the operation will be performed on the configured data types within the scope. You can specify the scope according to the following rules:
- Specify by prefix: Data can be matched by directory name or filename prefix.
- Specify by tag: Data can be filtered by tag.

The following data types can be configured:
- Files on the current version: Files on the latest version in the bucket.
- Files on historical versions: Objects on historical versions stored after versioning is enabled. For more information on versioning, see [Overview](https://www.tencentcloud.com/document/product/436/19883).
- Delete marker: Marker indicating that the object has been deleted. The lifecycle feature can remove the marker automatically after all historical versions are deleted. For more information on the delete marker, see [Delete Markers](https://www.tencentcloud.com/document/product/436/36716).
- Incomplete multipart uploads: Fragments generated due to incomplete multipart uploads.


### Operations
The operation to be performed when the object is hit:
- Data transition: transitions objects to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE after a specified period.
- Expiration: Deletes objects after their specified expiration time.


### Time
The time condition for triggering the above operations:
- Based on the number of days: You can specify when to perform the defined operation on an object based on the last-modified date of the object.

## Notes

>?For how to use the lifecycle, see [Configuring Lifecycle](https://www.tencentcloud.com/document/product/436/17031).

### Data transition

- #### Available regions
Data transition is supported in public cloud regions. Finance Cloud regions support only data transition to the STANDARD_IA storage class.

- #### One-way transition
Data transition is one-way (STANDARD > STANDARD_IA > ARCHIVE, or STANDARD > ARCHIVE) and cannot be done reversely. You can only call [PUT Object - Copy](https://www.tencentcloud.com/document/product/436/10881) (for non-ARCHIVE/DEEP ARCHIVE only) or [POST Object restore ](https://www.tencentcloud.com/document/product/436/12633) (for ARCHIVE and DEEP ARCHIVE only) to restore data from a colder storage class to a hotter one.

- #### Eventual consistency
If multiple rules are configured for the same set of objects and conflict with each other (excluding the configuration for deletion upon expiration), COS will execute the rule that **transitions the objects to the coldest storage class**.

For example, if rules A and B are configured to **transition the objects to STANDARD_IA and ARCHIVE** 90 days after file modification respectively and both hit the same object `test.txt`, rule B will be executed.

| Rule | Resource | Operation | Time Condition | Execution |
|----|----|----|----|----|
| Rule A | test.txt | Transition the object to the STANDARD_IA class. | 90 days after file modification | Execution fails due to a rule conflict. |
| Rule B | test.txt | Transition the object to the ARCHIVE class. | 90 days after file modification | Execution succeeds. |

>! 
>- We strongly recommend that you not configure conflicting lifecycle rules for the same set of objects in COS, because this may result in different fees.
>- Transitioning an object won't change the time the object was uploaded or modified.
>

### Deletion upon expiration

- #### How it works
When an object matches the specified lifecycle rule of deletion upon expiration, Tencent Cloud will add the object to the asynchronous deletion queue. There may be a certain delay in actual deletion. You can get the current status of the object by performing GET or HEAD Object operation.

- #### Eventual consistency
If multiple conflicting rules are configured for the same set of objects, the rule that will expire first will be performed first. **Deletion upon expiration will be performed before the transition**.

For example, if rules C and D are configured to **transition the objects to STANDARD_IA and delete the objects** 180 days after file modification respectively and both hit the same object `test.txt`, rule D will be executed.

| Rule | Resource | Operation | Time Condition | Execution |
|----|----|----|----|----|
| Rule C | test.txt | Transition the object to the STANDARD_IA class. | 180 days after file modification | Execution fails due to a rule conflict. |
| Rule D | test.txt | Delete the object. | 180 days after file modification | Execution succeeds. |


>! It is strongly recommended that you do not configure conflicting lifecycle rules for the same set of objects in COS, because this may result in different fees.
>

### Time
Lifecycle supports triggering rule execution based on the object modification time. Only file write operations such as [PUT Object](https://www.tencentcloud.com/document/product/436/7749), [PUT Object - Copy](https://www.tencentcloud.com/document/product/436/10881), [POST Object](https://www.tencentcloud.com/document/product/436/14690), and [Complete Multipart Upload](https://www.tencentcloud.com/document/product/436/7742) APIs will update the object modification time. The modification time of objects transitioned based on the lifecycle won't be updated.


### Cost considerations

- #### Execution
 - When the lifecycle feature performs a deletion operation, a backend deletion request will be generated. When it performs a transition operation, backend deletion and write requests will be generated. The requests generated by the above operations will be included in the request bill. For example, transitioning the file `test.txt` in STANDARD storage class to STANDARD_IA through the lifecycle will generate two requests, one used to delete the data in STANDARD and the other to write the data in STANDARD_IA.

 - Once triggered, actions configured at any time will always be executed at 00:00 the next day local time on Tencent Cloud COS. Objects are added to an asynchronous queue before execution. For objects that match the rules after the configuration time, actions are performed before 24:00 the next day.

 - For example, you configured a lifecycle rule at 15:00 on the 1st day of the month to delete files one day or longer after they are modified. Then, at 00:00 on the 2nd day, the lifecycle task scans for files that were modified over one day ago and deletes them. Files uploaded on the 1st day will not be deleted at 00:00 on the 2nd day, as the time elapsed since their modification is less than one day. Instead, these files will be deleted at 00:00 on the 3rd day.

 - When an accident occurs or there are too many objects in the bucket, lifecycle execution may fail. For failures due to other reasons, perform the GET or HEAD Object operation to get the current object status.

 - Tencent Cloud cannot provide an accurate bill unless the lifecycle execution is completed.

- #### Time insensitivity

 - Note that the minimum storage duration is 30 days, 90 days, and 180 days for the STANDARD_IA/INTELLIGENT TIERING, ARCHIVE, and DEEP ARCHIVE storage classes, respectively. No additional storage fees will be incurred for the transition or deletion operation itself. COS will ignore lifecycle configurations less than 30/90/180 days, and perform only correct configurations upon your request.

 - For example, if an object in STANDARD_IA is transitioned before 30 days, it will start incurring ARCHIVE storage fees on the transition day and continue incurring STANDARD_IA storage fees until the 30th day. Another example is that if an archived object is deleted upon expiration before it is stored for 90 days, it will continue incurring ARCHIVE storage fees until the 90th day. It works the same way with DEEP ARCHIVE.

- #### Size limits
There is a minimum size limit for objects in the STANDARD_IA, ARCHIVE, and DEEP ARCHIVE storage classes. For example, if an object smaller than 64 KB is uploaded to the STANDARD_IA storage class, it will be calculated as 64 KB. To reduce user costs, lifecycle execution does not transition the storage classes of objects that are smaller than 64 KB. 

>? Lifecycle execution does not transition the storage classes of objects that are smaller than 64 KB.
