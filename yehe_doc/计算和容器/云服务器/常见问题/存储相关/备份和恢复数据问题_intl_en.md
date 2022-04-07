## How do I back up data for CVM?

- If your CVM uses a cloud disk, you can back up your business data by creating a system disk custom image and a data disk snapshot. 
  - For more information on how to create a custom image, see [Create Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
  - For more information on how to create a snapshot, please see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755)
- If your CVM uses a local disk, you can back up data on system disk by creating a custom image. For business data in your data disk, you still need to customize the backup policy. 
  You can use FTP to back up data in the server to other places. For specific FTP deployment methods, see: 
  - For Windows: [Build the FTP Service (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)
  - For Linux: [Build the FTP Service (Linux)](https://intl.cloud.tencent.com/document/product/213/10912) 

## What are common data backup and recovery solutions?

The data backup and recovery solutions vary by application scenarios and businesses. The following recommendations can be used based on your actual needs:
- Back up the instance regularly using the [CBS Snapshot](https://intl.cloud.tencent.com/document/product/362/5757) feature.
- Deploy key components of an application across multiple availability zones, and copy the data as needed.
- Use [Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/5733) for domain name mapping to ensure that the service IP can be quickly redirected to another CVM instance when the server is unavailable.
- View the monitoring data regularly and configure corresponding alarms. For more information, please see [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).
- Process emergency requests with auto scaling. For more information, please see [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).
