## 소개

본 문서는 객체 삭제 관련 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명               |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제 | 버킷에서 지정 객체 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제 | 버킷에서 다수의 객체 일괄 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 단일 객체 삭제

#### 기능 설명

지정 객체를 삭제합니다(DELETE Object).

#### 예시 코드

[//]: #	".cssg-snippet-delete-object"

```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  //실행 요청
  DeleteObjectResult result = cosXml.DeleteObject(request);
  //요청 완료
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs)을 참고하십시오.

## 다수의 객체 삭제

#### 기능 설명

다수의 객체를 일괄 삭제합니다(DELETE Multiple Objects).

#### 예시 코드

[//]: #	".cssg-snippet-delete-multi-object"

```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
  //반환 결과 형식 설정
  request.SetDeleteQuiet(false);
  //객체 key
  string key = "exampleobject"; //객체 키
  List<string> objects = new List<string>();
  objects.Add(key);
  request.SetObjectKeys(objects);
  //실행 요청
  DeleteMultiObjectResult result = cosXml.DeleteMultiObjects(request);
  //요청 완료
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs)을 참고하십시오.

## 지정 접두사 삭제

#### 기능 설명

지정된 접두사 삭제는 디렉터리 삭제와 유사한 기능을 수행할 수 있습니다.

#### 예시 코드

[//]: #	".cssg-snippet-delete-prefix"

```cs
try
{
  String nextMarker = null;

  // 다음 페이지에 데이터가 없을 때까지 반복적으로 요청
  do
  {
    // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
    string bucket = "examplebucket-1250000000";
    string prefix = "folder1/"; //접두사 지정
    GetBucketRequest listRequest = new GetBucketRequest(bucket);
    //folder1/ 아래의 모든 객체와 하위 디렉터리 가져오기
    listRequest.SetPrefix(prefix);
    listRequest.SetMarker(nextMarker);
    //객체 나열 요청 실행
    GetBucketResult listResult = cosXml.GetBucket(listRequest);
    ListBucket info = listResult.listBucket;
    // 객체 리스트
    List<ListBucket.Contents> objects = info.contentsList;
    // 다음 페이지의 nextMarker
    nextMarker = info.nextMarker;
    
    DeleteMultiObjectRequest deleteRequest = new DeleteMultiObjectRequest(bucket);
    //반환 결과 형식 설정
    deleteRequest.SetDeleteQuiet(false);
    //객체 리스트
    List<string> deleteObjects = new List<string>();
    foreach (var content in objects)
    {
      deleteObjects.Add(content.key);
    }
    deleteRequest.SetObjectKeys(deleteObjects);
    //일괄 삭제 요청 실행
    DeleteMultiObjectResult deleteResult = cosXml.DeleteMultiObjects(deleteRequest);
    //요청 결과 출력
    Console.WriteLine(deleteResult.GetResultInfo());
  } while (nextMarker != null);
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs)을 참고하십시오.
