Tencent Push Notification Service (TPNS) provides a stable and fast application push service that features high delivery rate. Boasting industry-leading technical advantages, stable and reliable message push channels, and proprietary dual service architecture for session keep-alive, it is convenient and fast to access for effective improvement of the message delivery rate. It can push 18 million messages per minute and deliver them in a matter of seconds (sustaining in-app pushes for Tencent applications such as the Honor of Kings). In addition, it can precisely tag users for efficient lean operation of applications.

TPNS operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------|------|------------------------|
| Adding vendor channel     | tpns | AddChannelInfo         |
| Canceling scheduled push task   | tpns | CancelPush             |
| Creating application       | tpns | CreateApp              |
| Creating product       | tpns | CreateProduct          |
| Pushing message       | tpns | CreatePush             |
| Creating push plan     | tpns | CreatePushPlan         |
| Deleting application       | tpns | DeleteAppInfo          |
| Deleting product       | tpns | DeleteProductInfo      |
| Querying account bound to device | tpns | DescribeAccountByToken |
| Querying application information    | tpns | DescribeAppInfo        |
| Querying vendor channel information   | tpns | DescribeChannelInfo    |
| Querying product information     | tpns | DescribeProductInfo    |
| Updating application information     | tpns | ModifyAppInfo          |
| Modifying product information     | tpns | ModifyProductInfo      |
| Uploading certificate       | tpns | UploadCert             |
| Uploading number package      | tpns | UploadPushPackage      |
