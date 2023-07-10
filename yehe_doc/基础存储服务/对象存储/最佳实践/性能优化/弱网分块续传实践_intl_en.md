## Background

This document describes how to dynamically adjust the part size during a multipart upload to COS to improve the upload success rate on poor network connections on mobile devices.

> ! This feature is currently during beta test. To enable it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## Notes

1. Currently, the minimum part size supported by COS is 100 KB.
2. The smaller the part, the more the requests. Tests show that the time consumed by requests with a part size of 100 KB is about twice that when the part size is 1 MB.
3. If a request is initiated on a normal network connection, it is recommended to set the part size to 1 MB or higher.
4. Uploading an object in environments with weak signals may fail. If this is the case, you can consider setting the part size to 100 KB and retry the upload.
5. The smaller the part, the slower the file download in the future.

## Samples

#### SDK for Android

Below is sample code for uploading an object in multiple parts on a poor network connection:

```java
import android.content.Context;
import android.os.Handler;
import android.os.Message;
import android.util.Log;

import com.tencent.cos.xml.CosXmlService;
import com.tencent.cos.xml.CosXmlServiceConfig;
import com.tencent.cos.xml.common.ClientErrorCode;
import com.tencent.cos.xml.common.Region;
import com.tencent.cos.xml.exception.CosXmlClientException;
import com.tencent.cos.xml.exception.CosXmlServiceException;
import com.tencent.cos.xml.listener.CosXmlProgressListener;
import com.tencent.cos.xml.listener.CosXmlResultListener;
import com.tencent.cos.xml.model.CosXmlRequest;
import com.tencent.cos.xml.model.CosXmlResult;
import com.tencent.cos.xml.transfer.COSXMLUploadTask;
import com.tencent.cos.xml.transfer.TransferConfig;
import com.tencent.cos.xml.transfer.TransferManager;
import com.tencent.cos.xml.transfer.TransferState;
import com.tencent.cos.xml.transfer.TransferStateListener;
import com.tencent.qcloud.core.auth.QCloudCredentialProvider;
import com.tencent.qcloud.core.auth.ShortTimeCredentialProvider;

public class ResumeHelper {
    private final static String TAG = ResumeHelper.class.getSimpleName();

    private Context context;
    String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID, which should be replaced with your real bucket
    String region = Region.AP_Guangzhou.getRegion(); // Region of the bucket. Enter the region where your bucket is located
    private CosXmlService cosXmlService;

    private Handler mainHandler;
    private boolean isTriedOnce = false; // Whether the object has been re-uploaded. This is used to avoid unlimited re-uploads
    private final int MESSAGE_RETRY = 1;

    public ResumeHelper(Context context){
        this.context = context;
        this.mainHandler = new Handler(context.getMainLooper()){
            @Override
            public void handleMessage(Message msg) {
                super.handleMessage(msg);
                switch (msg.what){
                    case MESSAGE_RETRY:
                        /** Re-uploaded */
                        if(isTriedOnce)return;
                        isTriedOnce = true;
                        Parameter parameter = (Parameter) msg.obj;
                        /** Re-upload */
                        upload(parameter.srcPath, parameter.cosPath, parameter.uploadId, parameter.sliceSize);
                        break;
                }
            }
        };
        initCosXml();
    }

    /**
     * Initialize CosXmlService
     */
    private void initCosXml(){
        /** Initialize CosXmlServiceConfig */
        CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
                .setDebuggable(true)
                .isHttps(true)
                .setRegion(region)
                .builder();

        // A permanent key is used here for the convenience of testing. In actual usage, it is recommended to use a temporary key
        String secretId = "COS_SECRETID"; // Enter the SecretId of your TencentCloud API key
        String secretKey = "COS_SECRETKEY"; // Enter the SecretKey of your TencentCloud API key
        /** Initialize key information */
        QCloudCredentialProvider qCloudCredentialProvider = new ShortTimeCredentialProvider(secretId, secretKey, 6000);

        /** Initialize CosXmlService */
        cosXmlService = new CosXmlService(context, cosXmlServiceConfig, qCloudCredentialProvider);
    }

    /**
     * Upload
     * @param srcPath   Local file path
     * @param cosPath   COS path
     * @param uploadId   Whether the upload is resumed. If not, this parameter should be null
     * @param sliceSize   Part size set for multipart upload
     */
    public void upload(final String srcPath, final String cosPath, final String uploadId, long sliceSize){

        /** Set the part size for multipart upload */
        TransferConfig transferConfig = new TransferConfig.Builder()
                .setSliceSizeForUpload(sliceSize)
                .build();
        /** Initialize TransferManager */
        TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
        /** Start uploading: If uploadId != null, interrupted upload can be resumed */
        final COSXMLUploadTask uploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
        /** Display task status information */
        uploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d(TAG, "upload task state: " + state.name());
            }
        });
        /** Display upload progress */
        uploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                Log.d(TAG, "upload task progress: " + complete + "/" + target);
            }
        });
        /** Display upload result */
        uploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            /** Upload succeeded */
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                COSXMLUploadTask.COSXMLUploadTaskResult uploadTaskResult = (COSXMLUploadTask.COSXMLUploadTaskResult) result;
                Log.d(TAG, "upload task success: " + uploadTaskResult.printResult());
            }

            /** Upload failed */
            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d(TAG, "upload task failed: " + (exception == null ? serviceException.getMessage() :
                        (exception.errorCode + "," + exception.getMessage())));
                if(exception != null){
                    /** If the failure is caused by a network reason, try setting the part size to 100 KB and re-run the task */
                    if(exception.errorCode == ClientErrorCode.IO_ERROR.getCode()
                            || exception.errorCode == ClientErrorCode.POOR_NETWORK.getCode()){

                        Log.d(TAG, "upload task try again");
                        Message msg = mainHandler.obtainMessage();
                        msg.what = MESSAGE_RETRY;
                        Parameter parameter = new Parameter();
                        parameter.cosPath = cosPath;
                        parameter.srcPath = srcPath;
                        parameter.uploadId = uploadTask.getUploadId();
                        parameter.sliceSize = 100 * 1024L;
                        msg.obj = parameter;
                        mainHandler.sendMessage(msg);
                    }
                }
            }
        });
    }

    private static class Parameter{
        private String cosPath;
        private String srcPath;
        private String uploadId;
        private long sliceSize;
    }
}
```

#### SDK for iOS

Below is sample code for uploading an object in multiple parts on a poor network connection:

```objective-c
    QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
    NSURL* url = [NSURL fileURLWithPath:@"filePathURL"];
    put.object = @"text.txt";
    put.bucket = self.bucket;
    put.body =  url;
    [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
        NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
    }];
    [put setFinishBlock:^(QCloudUploadObjectResult *result, NSError *error) {
        /**
         1. Request timeout may be caused by a slow network connection. Upload resuming information (resumeData) can be obtained in error (in the QCloudUploadResumeDataKey field).
         2. Call the requestWithRequestData of QCloudCOSXMLUploadObjectRequest to pass in the resumeData and generate a new request.
         3. Reset the part size through the sliceSize of QCloudCOSXMLUploadObjectRequest as needed.
         4. Start uploading
         */
        if (error.code == -1001) {
            NSData *resumeData =error.userInfo[QCloudUploadResumeDataKey];
            if (resumeData) {
                QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest   requestWithRequestData:resumeData];
                request.sliceSize = 100*1024;
                [request setFinishBlock:^(QCloudUploadObjectResult* outputObject, NSError *error) {
                    NSLog(@"result: %@",outputObject);
                }];
                
                [request setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
                    NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
                }];
                [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];
            }
        }
    }];
   [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
    
```
