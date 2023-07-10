## 소개

본 문서는 객체 이동에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명                       | 작업 설명               |
| ------------------------------------------------------------ | ---------------------------- | ---------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정(객체 속성 수정) | 파일을 타깃 경로에 복사     |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제                 | 버킷에서 지정 객체 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 이동

객체 이동에는 타깃 위치로 원본 객체 복사 및 원본 객체 삭제의 두 가지 주요 작업이 포함되어 있습니다.

COS는 버킷 이름(Bucket)과 객체 키(ObjectKey)로 객체를 식별하므로 객체를 이동하는 경우 해당 객체의 식별자를 수정해야 합니다. 현재 COS Java SDK는 객체의 고유 식별자를 수정할 수 있는 인터페이스를 제공하지 않습니다. 하지만 **객체 복사**와 **객체 삭제**를 함께 사용하는 기본 작업으로 객체 식별자를 수정하고 객체를 이동할 수 있습니다.

예시로 mybucket-1250000000이라는 버킷의 picture.jpg 객체를 동일 버킷의 doc 경로로 이동하려면 먼저 picture.jpg 객체를 버킷의 doc 경로로 복사합니다. 즉, 객체 키를 doc/picture.jpg로 설정합니다. 복사 완료 후 picture.jpg 객체를 삭제하여 ‘이동’한 효과를 구현합니다.

마찬가지로 mybucket-1250000000 버킷의 picture.jpg 객체를 myanothorbucket-1250000000으로 이동하려면 먼저 객체를 myanothorbucket-1250000000 버킷에 복사하고 원본 객체를 삭제합니다.



#### 예시 코드

[//]: #	".cssg-snippet-move-object"

```cs
string sourceAppid = "1250000000"; //계정 appid
string sourceBucket = "sourcebucket-1250000000"; //"원본 객체 소재 버킷
string sourceRegion = "COS_REGION"; //원본 객체의 버킷 소재 리전
string sourceKey = "sourceObject"; //원본 객체 키
//원본 객체 속성 구성
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
string key = "exampleobject"; //타깃 객체의 객체 키

COSXMLCopyTask copyTask = new COSXMLCopyTask(bucket, key, copySource);

try {
  // 객체 복사
  COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
    transferManager.CopyAsync(copyTask);
  Console.WriteLine(result.GetResultInfo());

  // 객체 삭제
  DeleteObjectRequest request = new DeleteObjectRequest(sourceBucket, sourceKey);
  DeleteObjectResult deleteResult = cosXml.DeleteObject(request);
  // 결과 출력
  Console.WriteLine(deleteResult.GetResultInfo());
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MoveObject.cs)을 참고하십시오.
