## 소개

본 문서는 객체 태그에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 객체 태그 설정 | 업로드한 객체의 태그 설정       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 객체 태그 조회 | 지정한 객체의 기존 태그 조회 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 객체 태그 삭제 | 지정 객체의 기존 객체 태그 삭제 |


## SDK API 참조

모든 SDK 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)를 참조하십시오.

## 객체 태그 설정

### 업로드 시 태그 추가

#### 기능 설명

객체 업로드 시 요청에 특정 Header를 추가하여 객체에 태그를 달 수 있습니다. 예를 들어 x-cos-tagging의 값을 Key1=Value1&Key2=Value2로 설정할 경우, 태그 집합의 Key와 Value는 반드시 사전에 URL을 인코딩해야 합니다.

#### 예시 코드

```
String bucket = "examplebucket-1250000000"; //버킷. 포맷: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); //로컬 파일의 절대 경로
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
try {
    // 객체 태그를 설정합니다. 태그 집합의 Key와 Value는 반드시 사전에 URL을 인코딩해야 합니다.
    putObjectRequest.setRequestHeaders("x-cos-tagging", "Key1=Value&Key2=Value2", false);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}
// 멀티파트 업로드를 초기화한 UploadId가 존재하는 경우 해당 uploadId 값을 대입하여 이어서 전송합니다. 존재하지 않는 경우 null을 대입합니다.
String uploadId = null;
// 파일 업로드
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);
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

### 기존 객체에 태그 추가

#### 기능 설명

COS는 기존 객체의 태그 설정을 지원합니다. 객체에 키 값 쌍으로 객체 태그를 추가하면 기존 객체 리소스의 그룹화 관리에 도움이 됩니다.

#### 예시 코드

```
String bucket = "examplebucket-1250000000"; //버킷. 포맷: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
PutObjectTaggingRequest putObjectTaggingRequest = new PutObjectTaggingRequest(TestConst.PERSIST_BUCKET, TestConst.PERSIST_BUCKET_SMALL_OBJECT_PATH);
putObjectTaggingRequest.addTag("Key1", "Value1");
putObjectTaggingRequest.addTag("Key2", "안녕하세요");
try {
    PutObjectTaggingResult result = cosXmlService.putObjectTagging(putObjectTaggingRequest);
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
}
```

## 객체 태그 조회

#### 기능 설명

지정한 객체에 존재하는 객체 태그를 조회합니다.

#### 예시 코드

```
String bucket = "examplebucket-1250000000"; //버킷. 포맷: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
GetObjectTaggingRequest getObjectTaggingRequest = new GetObjectTaggingRequest(bucket, cosPath);  
try {
    GetObjectTaggingResult getObjectTaggingResult = cosXmlService.getObjectTagging(getObjectTaggingRequest);
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
}
```

## 객체 태그 삭제

#### 기능 설명

지정한 객체에 존재하는 객체 태그를 삭제합니다.

#### 예시 코드

```
String bucket = "examplebucket-1250000000"; //버킷. 포맷: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
DeleteObjectTaggingRequest deleteObjectTaggingRequest = new DeleteObjectTaggingRequest(bucket, cosPath);
try {
    DeleteObjectTaggingResult deleteObjectTaggingResult = cosXmlService.deleteObjectTagging(deleteObjectTaggingRequest);
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
}
```
