## 소개

본 문서는 객체의 사전 서명된 링크 생성에 대한 예시 코드를 제공합니다.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 


## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 사전 서명된 링크 생성

#### 예시 코드1: 사전 서명된 업로드 링크 생성

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
try {
    String bucket = "examplebucket-1250000000"; //버킷 이름
    String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자.
    String method = "PUT"; //HTTP 요청 메소드
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath) {
        @Override
        public RequestBodySerializer getRequestBody()
                throws CosXmlClientException {
            //put과 같이 body를 포함해야 하는 요청의 서명된 URL 계산에 사용됩니다.
            return RequestBodySerializer.string("text/plain",
                    "this is test");
        }
    };
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java)를 참고하십시오.
>

#### 예시 코드2: 사전 서명된 다운로드 링크 생성

[//]: # (.cssg-snippet-get-presign-download-url)
```java
try {
    String bucket = "examplebucket-1250000000"; //버킷 이름
    String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자.
    String method = "GET"; //HTTP 요청 메소드
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath);
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java)를 참고하십시오.
>

