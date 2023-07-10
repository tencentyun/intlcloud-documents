## 배경

본 문서에서는 Tencent Cloud COS 서비스를 모바일에서 사용할 경우, 약한 네트워크 환경에서 업로드되는 멀티파트의 크기를 유연하게 조절하여 업로드 성공률을 높이는 방법을 소개합니다.

> ! 본 기능은 현재 A/B테스트 단계이며, 본 기능의 사용을 원하실 경우, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 화이트리스트 활성화를 신청하십시오.

## 사용 시 유의사항

1. COS가 지원하는 멀티파트의 최소 크기는 100KB입니다.
2. 멀티파트가 작을수록 요청 수가 증가합니다. 현재 테스트 통계에 따르면 100KB 크기 멀티파트의 요청 시간은 1MB 멀티파트보다 약 2배 더 소요됩니다.
3. 정상 네트워크에서 요청을 보낸다면 멀티파트 크기를 1MB 이상으로 설정하길 권장합니다.
4. 네트워크 신호가 약한 환경에서는 객체 업로드에 실패하기 쉬우니, 멀티파트 크기를 100KB로 설정하여 재업로드해 볼 수 있습니다.
5. 멀티파트 크기 설정이 작을수록 파일 다운로드 속도가 느려질 수 있습니다.

## 예시

#### Android SDK

다음은 약한 네트워크 환경에서 객체를 멀티파트 업로드할 때의 예시 코드입니다.

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
    String bucket = "examplebucket-1250000000"; //버킷, 형식은 BucketName-APPID, 본인의 bucket으로 대체
    String region = Region.AP_Guangzhou.getRegion(); //버킷 소재 리전, 본인의 bucket 소재 리전 입력
    private CosXmlService cosXmlService;

    private Handler mainHandler;
    private boolean isTriedOnce = false; //무제한 재업로드 방지를 위한 재업로드 여부 확인
    private final int MESSAGE_RETRY = 1;

    public ResumeHelper(Context context){
        this.context = context;
        this.mainHandler = new Handler(context.getMainLooper()){
            @Override
            public void handleMessage(Message msg) {
                super.handleMessage(msg);
                switch (msg.what){
                    case MESSAGE_RETRY:
                        /** 재업로드함 */
                        if(isTriedOnce)return;
                        isTriedOnce = true;
                        Parameter parameter = (Parameter) msg.obj;
                        /** 재업로드 */
                        upload(parameter.srcPath, parameter.cosPath, parameter.uploadId, parameter.sliceSize);
                        break;
                }
            }
        };
        initCosXml();
    }

    /**
     * CosXmlService 초기화
     */
    private void initCosXml(){
        /** CosXmlServiceConfig 초기화 */
        CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
                .setDebuggable(true)
                .isHttps(true)
                .setRegion(region)
                .builder();

        //예시에서는 테스트 편의를 위해 영구 키를 사용하나 실제 적용에서는 임시 키 사용을 권장
        String secretId = "COS_SECRETID"; //Tencent Cloud API 키의 SecretId 입력
        String secretKey = "COS_SECRETKEY"; //Tencent Cloud API 키의 SecretKey 입력
        /** 키 정보 초기화 */
        QCloudCredentialProvider qCloudCredentialProvider = new ShortTimeCredentialProvider(secretId, secretKey, 6000);

        /** CosXmlService 초기화 */
        cosXmlService = new CosXmlService(context, cosXmlServiceConfig, qCloudCredentialProvider);
    }

    /**
     * 업로드
     * @param srcPath 로컬 파일 경로
     * @param cosPath COS에 저장된 경로
     * @param uploadId 업로드 재개 여부, 아닐 경우, null 
     * @param sliceSize 멀티파트 업로드 시 파트 크기 설정
     */
    public void upload(final String srcPath, final String cosPath, final String uploadId, long sliceSize){

        /** 멀티파트 업로드 설정 시 파트의 크기 */
        TransferConfig transferConfig = new TransferConfig.Builder()
                .setSliceSizeForUpload(sliceSize)
                .build();
        /** TransferManager 초기화 */
        TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
        /** 업로드 시작: uploadId != null이면 업로드 재개 */
        final COSXMLUploadTask uploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
        /** 작업 상태 정보 표시 */
        uploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d(TAG, "upload task state: " + state.name());
            }
        });
        /** 작업 업로드 진행 표시 */
        uploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                Log.d(TAG, "upload task progress: " + complete + "/" + target);
            }
        });
        /** 작업 업로드 결과 표시 */
        uploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            /** 작업 업로드 성공 */
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                COSXMLUploadTask.COSXMLUploadTaskResult uploadTaskResult = (COSXMLUploadTask.COSXMLUploadTaskResult) result;
                Log.d(TAG, "upload task success: " + uploadTaskResult.printResult());
            }

            /** 작업 업로드 실패 */
            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d(TAG, "upload task failed: " + (exception == null ? serviceException.getMessage() :
                        (exception.errorCode + "," + exception.getMessage())));
                if(exception != null){
                    /** 네트워크 원인으로 실패한 경우, 멀티파트 크기를 100KB로 설정해 재업로드 실행*/
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

#### iOS SDK

다음은 약한 네트워크 환경에서 객체를 멀티파트 업로드할 때의 예시 코드입니다.

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
         1. 네트워크 속도가 느릴 경우 요청 시간이 초과할 수 있습니다. error에서 업로드 재개와 관련한 정보 resumeData를 얻습니다(QCloudUploadResumeDataKey 필드에 저장).
         2. QCloudCOSXMLUploadObjectRequest의 requestWithRequestData를 호출하여 resumeData를 입력한 뒤 request를 다시 생성합니다.
         2. 필요에 따라 QCloudCOSXMLUploadObjectRequest의 sliceSize를 이용해 멀티파트 크기를 재설정합니다.
         3. 업로드를 시작합니다.
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
