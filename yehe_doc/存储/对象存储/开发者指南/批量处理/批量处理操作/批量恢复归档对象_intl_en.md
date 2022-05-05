Batch restoring archived objects can be used to restore archived objects in the inventory. This operation supports configuring parameters for POST Object restore. The configuration information will affect the restoration and expiration time of the replicas. For more information on POST Object restore, see [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

To create a job for batch restoring archived objects, you need to specify the following two parameters:

- Restoration mode: Standard or bulk mode. For more information on restoration mode, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- Replica validity period: When an archived object is restored, a temporary replica is created, which will expire and be deleted automatically after a specified time period. For more information on the validity period of a replica, see [Restoring Archive Objects](https://intl.cloud.tencent.com/document/product/436/30961).

## Notes

1. If the job to batch restore archived objects includes replicas of objects that have already been restored, the validity period of these objects will be updated when the job starts, ensuring that all object replicas in the job have the same validity period.
2. The batch restore job only initiates requests to restore objects. After all requests are sent, the Batch Operation page will report the job as complete. COS doesn’t notify you when the objects have been restored. However, you can configure event notifications to receive notifications. For more information, see [Event Notifications](https://intl.cloud.tencent.com/document/product/436/31648).

