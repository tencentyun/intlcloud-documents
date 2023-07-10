The batch restoration feature can be used to restore archived objects in the inventory. This operation supports configuring parameters for `POST Object restore`. The configuration information will affect the restoration time and expiration time of copies. For more information, see [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

Restoration is supported for ARCHIVE and DEEP ARCHIVE storage classes. For more information on these two storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

To create a batch restoration job, you need to specify the following two parameters:

- Restoration mode: Standard retrieval or bulk retrieval. For more information, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- Copy validity period: When an archived object is restored, a temporary copy will be created, which will expire and be deleted automatically after the specified time period. For more information on the copy validity period, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).

## Notes

1. If the batch restoration job includes copies of objects that have already been restored, the validity period of these copies will be updated when the job starts, ensuring that all copies in the job have the same validity period.
2. The batch restoration job only initiates requests to restore objects. After all requests are sent, the **Batch Operation** page will display the job as completed. COS doesn't notify you when the objects have been restored, but you can configure event notifications to receive notifications. For more information, see [Event Notifications](https://intl.cloud.tencent.com/document/product/436/31648).

