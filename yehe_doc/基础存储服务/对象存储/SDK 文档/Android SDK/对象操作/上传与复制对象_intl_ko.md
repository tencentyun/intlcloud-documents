## 소개

본 문서는 객체의 업로드, 복사 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 간편 업로드       | 하나의 객체를 버킷에 업로드    |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 폼을 사용한 객체 업로드   | 폼을 사용한 객체 업로드 요청                     |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정(객체 속성 수정)   | 파일을 타깃 경로에 복사                       |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 멀티파트 업로드       | 객체 멀티파트 업로드                        |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 고급 인터페이스(권장)

### 객체 업로드

고급 인터페이스는 간편 업로드, 멀티파트 업로드 인터페이스를 캡슐화합니다. 파일 크기에 따라 스마트하게 업로드 방식을 선택하며, 업로드 재개 기능을 지원합니다.

#### 예시 코드1: 로컬 파일 업로드

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// TransferConfig 초기화. 본 예시는 기본 설정을 사용합니다. 사용자 정의할 경우에는 SDK 인터페이스 문서를 참고하십시오.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); //로컬 파일의 절대 경로
//멀티파트 업로드를 초기화한 UploadId가 존재하는 경우 해당하는 uploadId 값을 대입하여 계속 전달합니다. 존재하지 않는 경우 null을 대입합니다.
String uploadId = null;
PutObjectRequest putObjectRequest= new PutObjectRequest(bucket, cosPath, srcPath);
// 업로드 시 파일 스토리지 유형 설정
putObjectRequest.setStroageClass(COSStorageClass.STANDARD);
// 파일 업로드
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);

//업로드 진행률 콜백 설정
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
//반환 결과 콜백 설정
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
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
//작업 상태 콜백 설정. 작업 진행 과정을 확인할 수 있습니다.
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java)를 참고하시기 바랍니다.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명된 링크 생성** 문서를 참고하시기 바랍니다. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

#### 예시 코드2: 바이너리 데이터 업로드

[//]: # (.cssg-snippet-transfer-upload-bytes)
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키

// 바이트 배열 업로드
byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        bytes);

//반환 결과 콜백 설정
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
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
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java)를 참고하시기 바랍니다.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명된 링크 생성** 문서를 참고하시기 바랍니다. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

#### 예시 코드3: 스트림 방식 업로드

[//]: # (.cssg-snippet-transfer-upload-stream)
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키

// 스트림 방식 업로드
InputStream inputStream =
        new ByteArrayInputStream("this is a test".getBytes(Charset.forName(
                "UTF-8")));
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        inputStream);

//반환 결과 콜백 설정
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
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
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java)를 참고하시기 바랍니다.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명된 링크 생성** 문서를 참고하시기 바랍니다. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

#### 예시 코드4: URI를 통한 업로드

[//]: # (.cssg-snippet-transfer-upload-uri)
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키

// 파일의 Uri
Uri uri = Uri.parse("exampleObject");
// 멀티파트 업로드를 초기화한 UploadId가 존재하는 경우 해당하는 uploadId 값을 대입하여 계속 전달합니다. 존재하지 않는 경우 null을 대입합니다.
String uploadId = null;
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        uri, uploadId);

//반환 결과 콜백 설정
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
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
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java)를 참고하시기 바랍니다.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명된 링크 생성** 문서를 참고하시기 바랍니다. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

#### 예시 코드5: 스마트 멀티파트 임계값 설정

`TransferManager`는 2M보다 크거나 같은 파일을 자동으로 멀티파트 업로드 하도록 기본 설정 되어있습니다. 다음 코드를 통해 멀티파트 임계값을 수정할 수 있습니다.

```
TransferConfig transferConfig = new TransferConfig.Builder()
	.setDivisionForUpload(2 * 1024 * 1024) // 2M보다 크거나 같은 파일을 자동으로 멀티파트 업로드하도록 설정 
	.build();
	
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);	
```


#### 예시 코드6: 업로드 일시 중지, 계속 및 취소

업로드 작업은 다음 방법으로 일시 정지할 수 있습니다.

[//]: # (.cssg-snippet-transfer-upload-pause)
```java
// 업로드 중 마지막 Complete Multipart Upload 요청을 전송한 경우 일시 중지에 실패합니다.
boolean pauseSuccess = cosxmlUploadTask.pauseSafely();
```

일시 정지 후 다음 방법으로 업로드를 재개할 수 있습니다.

[//]: # (.cssg-snippet-transfer-upload-resume)
```java
// 일시 중지 성공 시 업로드 재개 가능
if (pauseSuccess) {
    cosxmlUploadTask.resume();
}
```

다음 방법으로 업로드를 취소할 수 있습니다.

[//]: # (.cssg-snippet-transfer-upload-cancel)
```java
cosxmlUploadTask.cancel();
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java)를 참고하시기 바랍니다.

#### 예시 코드7: 일괄 업로드

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```java
//로컬 파일의 절대 경로
File[] files = new File(context.getCacheDir(), "exampleDirectory").listFiles();

// 일괄 업로드 시작
for (File file : files) {
    //멀티파트 업로드를 초기화한 UploadId가 존재하는 경우 해당하는 uploadId 값을 대입하여 계속 전달합니다. 존재하지 않는 경우 null을 대입합니다.
    String uploadId = null;

    // 파일 업로드
    COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
            file.getAbsolutePath(), uploadId);

    //반환 결과 콜백 설정
    cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
        @Override
        public void onSuccess(CosXmlRequest request, CosXmlResult result) {
            COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                    (COSXMLUploadTask.COSXMLUploadTaskResult) result;
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

#### 예시 코드8: 디렉터리 생성

[//]: # (.cssg-snippet-create-directory)
```java
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
// 버킷 내 폴더 위치 식별자. 즉, 객체 키이며 반드시 ’/’로 끝나야 합니다.
String cosPath = "exampleobject/";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, new byte[0]);
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutObjectResult putObjectResult =
                (PutObjectResult) result;
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
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java)를 참고하시기 바랍니다.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명된 링크 생성** 문서를 참고하시기 바랍니다. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

### 우선순위가 낮은 작업 설정

setPriorityLow()를 호출하면 해당 작업은 우선순위가 낮은 작업(예: 백그라운드 로그 업로드)이 되며, 스레드 점유로 인해 다른 업로드 작업이 정체되는 현상을 방지합니다.


```
PutObjectRequest putObjectRequest= new PutObjectRequest(bucket, key, filePath);
putObjectRequest.setPriorityLow(); // 우선순위가 낮은 업로드 작업으로 설정
final COSXMLUploadTask uploadTask = transferManager.upload(putObjectRequest, null);
uploadTask.setCosXmlResultListener(new CosXmlResultListener() {
      @Override
      public void onSuccess(CosXmlRequest request, CosXmlResult result) {}
			

     @Override
      public void onFail(CosXmlRequest request, CosXmlClientException clientException, CosXmlServiceException serviceException) {}
});
```


### 대기 타임아웃 시간 설정

startTimeoutTimer() 방법은 타이머를 활성화합니다. 지정 시간을 초과했는데도 작업이 실행되지 않았다면 해당 작업을 취소하고 onFailed 방법을 콜백합니다.


```
PutObjectRequest putObjectRequest= new PutObjectRequest(bucket, key, filePath);
final COSXMLUploadTask uploadTask = transferManager.upload(putObjectRequest, null);
uploadTask.startTimeoutTimer(1000); // 1s 대기 타임아웃 시간
uploadTask.setCosXmlResultListener(new CosXmlResultListener() {
      @Override
      public void onSuccess(CosXmlRequest request, CosXmlResult result) {}
			

     @Override
      public void onFail(CosXmlRequest request, CosXmlClientException clientException, CosXmlServiceException serviceException) {}
});
```



### 객체 복사

고급 인터페이스는 간편 복사 및 멀티파트 복사 인터페이스의 비동기화 요청을 캡슐화합니다. 복사 요청 일시 정지, 복구 및 취소를 지원합니다.

#### 예시 코드

[//]: # (.cssg-snippet-transfer-copy-object)
```java
// TransferConfig 초기화. 본 예시는 기본 설정을 사용합니다. 사용자 정의할 경우에는 SDK 인터페이스 문서를 참고하십시오.
TransferConfig transferConfig = new TransferConfig.Builder().build();
//TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String sourceAppid = "1250000000"; //계정 APPID
String sourceBucket = "sourcebucket-1250000000"; //원본 객체가 있는 버킷
String sourceRegion = "COS_REGION"; //원본 객체 버킷이 있는 리전
String sourceCosPath = "sourceObject"; //원본 객체의 객체 키
//원본 객체 속성 구성
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
                sourceAppid, sourceBucket, sourceRegion, sourceCosPath);
//타깃 버킷
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
//타깃 객체
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키

//객체 복사
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath,
        copySourceStruct);

//반환 결과 콜백 설정
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLCopyTask.COSXMLCopyTaskResult cOSXMLCopyTaskResult =
                (COSXMLCopyTask.COSXMLCopyTaskResult) result;
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
//작업 상태 콜백 설정. 작업 진행 과정을 확인할 수 있습니다.
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferCopyObject.java)를 참고하시기 바랍니다.

## 간단한 작업

### 객체 간편 업로드

#### 기능 설명

PUT Object 인터페이스는 객체를 지정된 버킷에 업로드할 수 있습니다. 이 작업은 요청자가 버킷에 대한 WRITE 권한을 가지고 있어야 합니다. 최대 5GB 이하인 객체의 업로드를 지원합니다. 5GB 이상의 객체는 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 혹은 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) 업로드를 사용하십시오.

> !
> 1. Key(파일명)는 `/`로 끝날 수 없습니다. 그렇지 않으면 폴더로 인식될 수 있습니다.
> 2. 루트 계정(동일한 APPID)당 버킷의 ACL 규칙 수량은 최대 1000개이며, 객체 ACL 규칙 수량은 제한이 없습니다. 객체 ACL 제어가 필요하지 않을 경우 업로드 시 설정하지 마십시오. 기본 버킷 권한이 상속됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-object)
```java
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키.
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString();//"로컬 파일의 절대 경로";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath,
        srcPath);

putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        PutObjectResult putObjectResult = (PutObjectResult) result;
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

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PutObject.java)를 참고하시기 바랍니다.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명된 링크 생성** 문서를 참고하시기 바랍니다. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

### 입력 폼 객체 업로드

#### 기능 설명

폼을 사용해 객체 업로드를 요청합니다.

#### 예시 코드

[//]: # (.cssg-snippet-post-object)
```java
String bucket = "examplebucket-1250000000"; //버킷 이름, 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키.
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString();//"로컬 파일의 절대 경로";

PostObjectRequest postObjectRequest = new PostObjectRequest(bucket, cosPath,
        srcPath);

postObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
cosXmlService.postObjectAsync(postObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        PutObjectResult putObjectResult = (PutObjectResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PostObject.java)를 참고하시기 바랍니다.

### 객체 복사(속성 수정)

타깃 경로에 파일을 복사합니다(PUT Object-Copy).

#### 예시 코드1: 객체 복사 시 객체 속성 유지

[//]: # (.cssg-snippet-copy-object)
```java
String sourceAppid = "1250000000"; //계정 APPID
String sourceBucket = "sourcebucket-1250000000"; //원본 객체가 있는 버킷
String sourceRegion = "COS_REGION"; //원본 객체 버킷이 있는 리전
String sourceCosPath = "sourceObject"; //원본 객체 키
// 원본 객체 속성 구성
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CopyObject.java)를 참고하시기 바랍니다.

#### 예시 코드2: 객체 복사 시 객체 속성 변경

[//]: # (.cssg-snippet-copy-object-replaced)
```java
String sourceAppid = "1250000000"; //계정 APPID
String sourceBucket = "sourcebucket-1250000000"; //원본 객체가 있는 버킷
String sourceRegion = "COS_REGION"; //원본 객체 버킷이 있는 리전
String sourceCosPath = "sourceObject"; //원본 객체 키
// 원본 객체 속성 구성
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
copyObjectRequest.setCopyMetaDataDirective(MetaDataDirective.REPLACED);
copyObjectRequest.setXCOSMeta("x-cos-metadata-oldKey", "newValue");

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CopyObject.java)를 참고하시기 바랍니다.

#### 예시 코드3: 객체 메타데이터 수정

[//]: # (.cssg-snippet-modify-object-metadata)
```java
String appId = "1250000000"; //계정 APPID
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String region = "COS_REGION"; //원본 객체 버킷이 있는 리전
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
// 원본 객체 속성 구성
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
copyObjectRequest.setCopyMetaDataDirective(MetaDataDirective.REPLACED);
// 메타데이터를 새로운 값으로 수정
copyObjectRequest.setXCOSMeta("x-cos-metadata-oldKey", "newValue");

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ModifyObjectProperty.java)를 참고하시기 바랍니다.

#### 예시 코드4: 객체 스토리지 유형 수정

[//]: # (.cssg-snippet-modify-object-storage-class)
```java
String appId = "1250000000"; //계정 APPID
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String region = "COS_REGION"; //원본 객체 버킷이 있는 리전
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
// 원본 객체 속성 구성
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
// 표준IA 스토리지로 변경
copyObjectRequest.setCosStorageClass(COSStorageClass.STANDARD_IA);

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ModifyObjectProperty.java)를 참고하시기 바랍니다.

## 멀티파트 작업

여기서는 멀티파트 업로드 프로세스를 설명합니다.

#### 멀티파트 업로드와 복사 프로세스

1. 멀티파트 업로드를 초기화(Initiate Multipart Upload)하고 UploadId를 획득합니다.
2. UploadId를 사용해 멀티파트를 업로드(Upload Part)하거나 멀티파트를 복사(Upload Part Copy)합니다.
3. 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 멀티파트 업로드 재개와 복사 프로세스

1. UploadId를 기록하지 않은 경우 멀티파트 업로드 작업을 조회(List Multipart Uploads)하여 해당 파일의 UploadId를 획득합니다.
2. UploadId를 사용해 업로드된 멀티파트를 나열합니다(List Parts).
2. UploadId를 사용해 남은 멀티파트를 업로드(Upload Part)하거나 남은 멀티파트를 복사(Upload Part Copy)합니다.
3. 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 멀티파트 업로드 및 복사 중지 프로세스

1. UploadId를 기록하지 않은 경우 멀티파트 업로드 작업을 조회(List Multipart Uploads)하여 해당 파일의 UploadId를 획득합니다.
2. 멀티파트 업로드를 중지하고 업로드된 멀티파트를 삭제합니다(Abort Multipart Upload).

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회합니다(List Multipart Uploads).

#### 예시 코드

[//]: # (.cssg-snippet-list-multi-upload)
```java
String bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
ListMultiUploadsRequest listMultiUploadsRequest =
        new ListMultiUploadsRequest(bucket);
cosXmlService.listMultiUploadsAsync(listMultiUploadsRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        ListMultiUploadsResult listMultiUploadsResult =
                (ListMultiUploadsResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java)를 참고하시기 바랍니다.

### 멀티파트 업로드 초기화

#### 기능 설명

Multipart Upload 업로드 작업을 초기화하고 해당하는 uploadId를 가져옵니다(Initiate Multipart Upload).

#### 예시 코드
g
[//]: # (.cssg-snippet-init-multi-upload)
```java
String bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키.

InitMultipartUploadRequest initMultipartUploadRequest =
        new InitMultipartUploadRequest(bucket, cosPath);
cosXmlService.initMultipartUploadAsync(initMultipartUploadRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        // 멀티파트 업로드의 uploadId
        uploadId = ((InitMultipartUploadResult) result)
                .initMultipartUpload.uploadId;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java)를 참고하시기 바랍니다.

### 멀티파트 업로드

객체를 멀티파트 업로드합니다(Upload Part).

#### 예시 코드

[//]: # (.cssg-snippet-upload-part)
```java
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
UploadPartRequest uploadPartRequest = new UploadPartRequest(bucket, cosPath,
        partNumber, srcFile.getPath(), offset, PART_SIZE, uploadId);

uploadPartRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

cosXmlService.uploadPartAsync(uploadPartRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        String eTag = ((UploadPartResult) result).eTag;
        eTags.put(partNumber, eTag);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java)를 참고하시기 바랍니다.

### 멀티파트 복사

#### 기능 설명

다른 객체를 한 파트로 복사합니다(Upload Part-Copy).

#### 예시 코드

[//]: # (.cssg-snippet-upload-part-copy)
```java
String sourceAppid = "1250000000"; //계정 APPID
String sourceBucket = "sourcebucket-1250000000"; //원본 객체가 있는 버킷
String sourceRegion = "COS_REGION"; //원본 객체 버킷이 있는 리전
String sourceCosPath = "sourceObject"; //원본 객체 키
// 원본 객체 속성 구성
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키

String uploadId = "exampleUploadId";
int partNumber = 1; //멀티파트 번호
long start = 0; //원본 객체의 시작 위치 복사
long end = 1023; //원본 객체의 종료 위치 복사

UploadPartCopyRequest uploadPartCopyRequest =
        new UploadPartCopyRequest(bucket, cosPath,
        partNumber, uploadId, copySourceStruct, start, end);
cosXmlService.copyObjectAsync(uploadPartCopyRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        UploadPartCopyResult uploadPartCopyResult =
                (UploadPartCopyResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsCopyObject.java)를 참고하시기 바랍니다.

### 업로드된 멀티파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 예시 코드

[//]: # (.cssg-snippet-list-parts)
```java
String bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키.

ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, cosPath,
        uploadId);
cosXmlService.listPartsAsync(listPartsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        ListParts listParts = ((ListPartsResult) result).listParts;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java)를 참고하시기 바랍니다.

### 멀티파트 업로드 완료

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 예시 코드
[//]: # (.cssg-snippet-complete-multi-upload)
```java
String bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키.

CompleteMultiUploadRequest completeMultiUploadRequest =
        new CompleteMultiUploadRequest(bucket,
        cosPath, uploadId, eTags);
cosXmlService.completeMultiUploadAsync(completeMultiUploadRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        CompleteMultiUploadResult completeMultiUploadResult =
                (CompleteMultiUploadResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java)를 참고하시기 바랍니다.

### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 예시 코드

[//]: # (.cssg-snippet-abort-multi-upload)
```java
String bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키.

AbortMultiUploadRequest abortMultiUploadRequest =
        new AbortMultiUploadRequest(bucket,
        cosPath, uploadId);
cosXmlService.abortMultiUploadAsync(abortMultiUploadRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        AbortMultiUploadResult abortMultiUploadResult =
                (AbortMultiUploadResult) result;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/AbortMultiPartsUpload.java)를 참고하시기 바랍니다.

