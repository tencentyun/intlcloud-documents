### If multiple VOD cold storage policies are set, will cold storage be triggered for a media file that meets the requirements of one policy?
When a media file meets the requirements of multiple VOD cold storage policies, cold storage will be implemented for the file in the priority of DEEP ARCHIVE > ARCHIVE > STANDARD_IA.
When a policy contains multiple requirements, cold storage will be triggered for a media file only when the file meets all the requirements.


### How is the cold storage of VOD media files charged?
Changing the storage class of a media file from STANDARD to another one will not be charged. After that, the [file storage](https://intl.cloud.tencent.com/document/product/266/14666) and [data retrieval](https://intl.cloud.tencent.com/document/product/266/14666) will be billed.

### After a media file of cold storage is deleted before it is stored for the minimum required storage days, will it be charged any fees?
Its storage will be charged by the minimum [storage](https://intl.cloud.tencent.com/document/product/266/14666) days, even when its storage duration is shorter.
Minimum storage duration for STANDARD_IA files: 30 days.
Minimum storage duration for ARCHIVE files: 90 days.
Minimum storage duration for DEEP ARCHIVE files: 180 days.

### Will the storage class of a cold storage media file turn back to STANDARD automatically?
If a media file meets the requirements of a cold storage policy, the file will be stored in the policy defined class. The class will not default back to STANDARD automatically, yet you can modify the class manually. After manual modification, the storage class will turn to a policy defined one if the policy is triggered. All files will be checked for policy execution every day.


### How much will the access efficiency slow down after a media file turns to STANDARD_IA storage?
Modifying storage class will affect watch experience as file retrievals will affect broadcasting of the first frame and stutter rate among other metrics. We recommend you not modify the storage classes of frequently used media files, and use STANDARD for such files. 


### Does VOD provide data retrieval APIs?
Such APIs are under development.


### How long will it take to change the storage class of a file from STANDARD to STANDARD_IA?
The time depends on the video size, and normally it is in seconds.


### How often will a VOD cold storage policy be executed?
An enabled VOD cold storage policy will be executed at 00:00 (UTC+08:00) each day for all stored data under the current application.
