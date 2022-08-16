Data Lake Compute allows you to create and bind a metadata acceleration bucket to accelerate query and analysis. For more information, see [Metadata Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/43305).

## Binding a metadata acceleration bucket
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region.
2. Select **Data Explore** on the left sidebar, click the settings icon, and select **Modify configuration**.
![]()
3. Select a metadata acceleration bucket and bind it to or unbind it from a running cluster. One bucket can be bound to multiple running clusters. To create a bucket, go to the COS console.
![]()
Go to [COS > Bucket List](https://console.cloud.tencent.com/cos/bucket), create a bucket, and enable the metadata acceleration feature. For detailed permissions and restraints, see [Metadata Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/43305).
![]()
![]()
4. You can also bind a metadata acceleration bucket by clicking **Edit** in the **Operation** column of the **Data catalog** tab in the **Data management** module.
![]()




