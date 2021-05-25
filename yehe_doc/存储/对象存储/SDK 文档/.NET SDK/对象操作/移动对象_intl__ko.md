## 소개

본 문서는 객체 이동에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명                       | 작업 설명               |
| ------------------------------------------------------------ | ---------------------------- | ---------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정(객체 속성 수정) | 파일을 타깃 경로에 복사     |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제                 | 버킷에서 지정 객체 삭제 |

## SDK API 참조

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참조하십시오.

## 객체 이동

객체 이동에는 원본 객체를 타깃 위치로 복사, 원본 객체를 삭제하는 두 가지 주요 작업이 포함되어 있습니다.

COS의 객체는 'bucket+key' 이름으로 식별되며, 객체 이동은 해당 객체의 이름을 변경하는 것을 의미합니다. SDK는 현재 객체 이름을 변경하는 전용 인터페이스를 제공하지 않으나 기본 작업을 통해 해당 효과를 얻을 수 있습니다.

예를 들어, 'mybucket'이라는 버킷의 'mykey' 객체를 'mybucket' 버킷의 'prefix/mykey'로 이동할 경우, 'prefix/mykey' 객체를 복사한 후 'mykey' 객체를 삭제합니다.

마찬가지로, 'mykey' 객체를 'myanothorbucket' 버킷으로 이동할 경우, 객체를 새로운 버킷에 복사한 후 기존 객체를 삭제합니다.

#### 예시 코드

[//]: #	".cssg-snippet-move-object"

```cs
string sourceAppid = "1250000000"; //계정 appid
string sourceBucket = "sourcebucket-1250000000"; //"원본 객체가 있는 버킷
string sourceRegion = "COS_REGION"; //원본 객체의 버킷이 있는 리전
string sourceKey = "sourceObject"; //원본 객체 키
//원본 객체 속성 구성
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000"; //타깃 버킷. 포맷: BucketName-APPID
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

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MoveObject.cs)를 참조하십시오.
