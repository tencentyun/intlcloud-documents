## 소개

본 문서는 객체의 다운로드 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬 파일 시스템에 객체 다운로드        |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 고급 인터페이스(권장)

### 객체 다운로드

고급 인터페이스는 다운로드 요청 일시 중지, 복구, 취소를 지원하며, 중단된 지점부터 다운로드 기능을 제공합니다.

#### 예시 코드1: 객체 다운로드

[//]: # (.cssg-snippet-transfer-download-object)
```java
// 고급 다운로드 인터페이스는 중단된 지점부터 이어 올리기를 지원합니다. 따라서 다운로드 전에 HEAD를 요청하여 파일 정보를 획득하시기 바랍니다.
// 임시 키 또는 서브 계정을 사용해 액세스하는 경우 권한 리스트에 HeadObject 권한이 포함되어 있는지 확인하십시오.

// TransferConfig 초기화. 본 예시는 기본 설정을 사용합니다. 사용자 정의할 경우에는 SDK 인터페이스 문서 참고
TransferConfig transferConfig = new TransferConfig.Builder().build();
//TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자, 즉 객체 키
//로컬 디렉터리 경로
String savePathDir = context.getExternalCacheDir().toString();
//로컬에 저장할 파일명. 입력하지 않는 경우(null) COS의 파일명과 동일
String savedFileName = "exampleobject";

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext,
                bucket, cosPath, savePathDir, savedFileName);

//다운로드 진행률 콜백 설정
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
//반환 결과 콜백 설정
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLDownloadTask.COSXMLDownloadTaskResult downloadTaskResult =
                (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
//작업 상태 콜백 설정. 작업 진행 과정 확인 가능
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java)를 참고하십시오.

#### 예시 코드2: 다운로드 일시 중지, 계속, 취소

다운로드 작업은 다음 방식으로 일시 중지 가능:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```java
cosxmlDownloadTask.pause();
```

일시 정지 후 다음 방법으로 업로드 재개 가능:

[//]: # (.cssg-snippet-transfer-download-object-resume)
```java
cosxmlDownloadTask.resume();
```

다음 방법을 통해 다운로드 취소:

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```java
cosxmlDownloadTask.cancel();
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java)를 참고하십시오.

#### 예시 코드3: 체크포인트 재시작 설정

[//]: # (.cssg-snippet-transfer-download-resumable)
```java
// TransferConfig 초기화. 본 예시는 기본 설정을 사용합니다. 사용자 정의할 경우에는 SDK 인터페이스 문서 참고
// TransferManager는 체크포인트 다운로드를 지원하므로 bucket, cosPath, savePathDir, storedFileName만 확인하면 됩니다.
// 매개변수가 동일하면, 마지막으로 다운로드한 위치에서 SDK를 계속 다운로드합니다.
TransferConfig transferConfig = new TransferConfig.Builder().build();
//TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자, 즉 객체 키
//로컬 디렉터리 경로
String savePathDir = context.getExternalCacheDir().toString();
//로컬에 저장할 파일명. 입력하지 않는 경우(null) COS의 파일명과 동일
String savedFileName = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePathDir, savedFileName);

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext, getObjectRequest);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java)를 참고하십시오.

#### 예시 코드4: 일괄 다운로드

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```java
// 버킷 내 객체 위치 식별자, 즉 객체 키
String[] cosPaths = new String[] {
        "exampleobject1",
        "exampleobject2",
        "exampleobject3",
};

for (String cosPath : cosPaths) {

    COSXMLDownloadTask cosxmlDownloadTask =
            transferManager.download(applicationContext,
                    bucket, cosPath, savePathDir, savedFileName);
    // 반환 결과 콜백 설정
    cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
        @Override
        public void onSuccess(CosXmlRequest request, CosXmlResult result) {
            COSXMLDownloadTask.COSXMLDownloadTaskResult cOSXMLDownloadTaskResult =
                    (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
        }

        @Override
        public void onFail(CosXmlRequest request,
                           CosXmlClientException clientException,
                           CosXmlServiceException serviceException) {
            if (clientException != null) {
                clientException.printStackTrace();
            } else {
                serviceException.printStackTrace();
            }
        }
    });
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java)를 참고하십시오.

#### 예시 코드5: 디렉터리 다운로드

[//]: # (.cssg-snippet-transfer-download-directory)
```java
boolean isTruncated = true;
String marker = null;
try {
    while (isTruncated) {
        GetBucketRequest getBucketRequest = new GetBucketRequest(region, bucket, directoryPath);
        // 페이징 정보 설정
        getBucketRequest.setMarker(marker);
        // 하위 디렉터리를 쿼리하지 않도록 설정
        getBucketRequest.setDelimiter("/");
        GetBucketResult getBucketResult = cosXmlService.getBucket(getBucketRequest);
        // 일괄 다운로드
        for (ListBucket.Contents content : getBucketResult.listBucket.contentsList) {
            GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, content.key, savePathDir);
            transferManager.download(context,getObjectRequest);
        }
        isTruncated = getBucketResult.listBucket.isTruncated;
        marker = getBucketResult.listBucket.nextMarker;
    }
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java)를 참고하십시오.

## 간단한 작업

### 객체 다운로드

#### 기능 설명

Object(파일/객체)를 로컬에 다운로드합니다(GET Object).

#### 예시 코드

[//]: # (.cssg-snippet-get-object)
```java
String bucket = "examplebucket-1250000000"; //버킷 이름, 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
String savePath = context.getExternalCacheDir().toString(); //로컬 경로

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath,
        savePath);
getObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

cosXmlService.getObjectAsync(getObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest,
                          CosXmlResult cosXmlResult) {
        GetObjectResult getObjectResult = (GetObjectResult) cosXmlResult;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/GetObject.java)를 참고하십시오.

