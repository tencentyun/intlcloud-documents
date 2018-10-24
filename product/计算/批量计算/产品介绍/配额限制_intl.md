## Limit on Number of Concurrent Cores in Batch
In order to ensure that all users can execute computing jobs during peak hours, Batch uses the total CPU cores held by a user at the same time as the dimension for quota limit. Currently, at most **500 CPU cores** can be held in **one single region** (such as Guangzhou or Shanghai). A ticket can be submitted if more cores are needed.

## Limit on Quota for CVM Instances
Batch may use postpaid CVM instances during job execution. There is a limit on the number of CVM instances that a user can hold at the same time in different **availability zones**. For details, see the "Purchase Limits for Postpaid CVM Instances" section in [Quota for CVM Instances](https://intl.cloud.tencent.com/document/product/213/2664).
