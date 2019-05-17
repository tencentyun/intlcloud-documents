## Background
&nbsp;&nbsp;&nbsp;&nbsp;Apps are the mobile Internet’s building blocks in the mobile Internet era, and they often require massive data uploads and downloads. Therefore, data security and reliability are crucial. Developers can let  [Tencent Cloud COS Service] (https://cloud.tencent.com/product/cos) handle data storage, and can focus on their Apps business logics to reduce workload and improve development efficiency. This document mainly describes how to quickly build a COS-based App transfer service to upload and download App data on Tencent Cloud COS. All you need to do is deploy your businesses and generate and manage temporary keys on your server.

## Preparations

-  For more information on how to set up temporary key service, see [Temporary Key Generation and Usage Guide](https://cloud.tencent.com/document/product/436/14048).
-  A mobile phone with Android 4.0 (API level 15) or above.

>?We recommend that you use the temporary key service for authorization. If you are unable to set up the service, you can use our Demo with a permanent key.


## Downloading and Installing App


You can download the Demo directly by scanning the QR code with your Android phone:

![](https://main.qcloudimg.com/raw/2687b91ad1d02d335a9f264411275318.png)
 
Download complete code from [GitHub >>](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice).

