## Background
&nbsp;&nbsp;&nbsp;&nbsp;In the era of mobile Internet, Apps, as the infrastructure of mobile Internet services, often need to upload and download a large amount of data, therefore the security and reliability of data are particularly important. By entrusting data storage task to [Tencent Cloud COS Service](https://cloud.tencent.com/product/cos), developers can only focus on the business logic of their Apps, thus reducing work load and improving development efficiency. This document mainly describes how to quickly build a COS-based App transfer service to upload and download App data on Tencent Cloud COS. All you need to do is deploy your businesses, and generate and manage temporary keys on your server.

## Preparations

-  For more information on how to set up temporary key service, see [Temporary Key Generation and Usage Guide](https://cloud.tencent.com/document/product/436/14048).
-  A mobile phone with Android 4.0 (API level 15) or above.

>?We recommend that you use the temporary key service for authorization. If you are unable to set up the service, you can use our Demo with a permanent key.


## Downloading and Installing App


You can download the Demo directly by scanning the QR code with your Android phone:

![](https://main.qcloudimg.com/raw/2687b91ad1d02d335a9f264411275318.png)
 
Download complete code from [GitHub >>](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice).

