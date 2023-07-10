## 소개


본 문서는 객체 이동에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명                       | 작업 설명               |
| :----------------------------------------------------------- | :--------------------------- | :--------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정(객체 속성 수정) | 파일을 타깃 경로에 복사     |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제                 | 버킷에서 지정 객체 삭제 |

## 객체 이동

객체 이동에는 타깃 위치로 원본 객체 복사 및 원본 객체 삭제의 두 가지 주요 작업이 포함되어 있습니다.

COS는 버킷 이름(Bucket)과 객체 키(ObjectKey)로 객체를 식별하므로 객체를 이동하는 경우 해당 객체의 식별자를 수정해야 합니다. 현재 COS Java SDK는 객체의 고유 식별자를 수정할 수 있는 인터페이스를 제공하지 않습니다. 하지만 **객체 복사**와 **객체 삭제**를 함께 사용하는 기본 작업으로 객체 식별자를 수정하고 객체를 이동할 수 있습니다.

예시로 mybucket-1250000000이라는 버킷의 picture.jpg 객체를 동일 버킷의 doc 경로로 이동하려면 먼저 picture.jpg 객체를 버킷의 doc 경로로 복사합니다. 즉, 객체 키를 doc/picture.jpg로 설정합니다. 복사 완료 후 picture.jpg 객체를 삭제하여 ‘이동’한 효과를 구현합니다.

마찬가지로 mybucket-1250000000 버킷의 picture.jpg 객체를 myanothorbucket-1250000000으로 이동하려면 먼저 객체를 myanothorbucket-1250000000 버킷에 복사하고 원본 객체를 삭제합니다.

#### 예시 코드

[//]: # (.cssg-snippet-delete-object)
```
final String sourceAppid = "1250000000"; //계정 appid
        final String sourceBucket = "sourcebucket-1250000000"; //"원본 객체가 있는 버킷
        final String sourceRegion = "COS_REGION"; //원본 객체 버킷이 있는 리전
        final String sourceKey = "sourceObject"; //원본 객체 키
        //원본 객체 속성 구성
        CopyObjectRequest.CopySourceStruct copySource = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket,
                sourceRegion, sourceKey);
        String bucket = "examplebucket-1250000000"; //타깃 버킷. 포맷: BucketName-APPID
        String key = "exampleobject"; //타깃 객체의 객체 키
        COSXMLCopyTask copyTask = transferManager.copy(bucket, key, copySource);
        copyTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
               
                // 복사 후 파일 삭제
                DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(sourceBucket, sourceKey);
                cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
                    @Override
                    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
                        // 파일 삭제 완료
                    }

                    @Override
                    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException e, CosXmlServiceException e1) {
                        // 파일 삭제 실패
                    }
                });
            }
            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
            }
        });
```
