## 소개

본문은 인벤토리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명             |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | 인벤토리 작업 설정 | 버킷의 인벤토리 작업 설정 |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | 인벤토리 작업 조회 | 버킷 인벤토리 작업 조회 |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | 인벤토리 작업 삭제 | 버킷의 인벤토리 작업 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 인벤토리 작업 설정

#### 기능 설명

PUT Bucket inventory는 버킷에 인벤토리 작업을 생성하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-inventory)
```cs
try
{
  string inventoryId = "aInventoryId";
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  PutBucketInventoryRequest putRequest = new PutBucketInventoryRequest(bucket, inventoryId);
  putRequest.SetDestination("CSV", "100000000001", "examplebucket-1250000000", "ap-guangzhou","list1");
  putRequest.IsEnable(true);
  putRequest.SetScheduleFrequency("Daily");
  //실행 요청
  PutBucketInventoryResult putResult = cosXml.PutBucketInventory(putRequest); 
  
  //요청 완료
  Console.WriteLine(putResult.GetResultInfo());
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketInventory.cs)를 참고하십시오.


#### 오류 코드 설명

이 요청에서 발생할 수 있는 몇 가지 특수 오류는 다음과 같습니다.

| 오류 코드                | 설명                                         | 상태 코드               |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument       | 잘못된 매개변수 값                               | HTTP 400 Bad Request |
| TooManyConfigurations | 인벤토리 수가 최댓값인 1,000개에 도달                 | HTTP 400 Bad Request |
| AccessDenied          | 승인되지 않은 액세스. 버킷에 액세스할 수 있는 권한이 없습니다. | HTTP 403 Forbidden   |

## 인벤토리 작업 조회

#### 기능 설명

GET Bucket inventory는 버킷에 있는 사용자의 인벤토리 작업 정보를 조회하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-inventory)
```cs
try
{
  string inventoryId = "aInventoryId";
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketInventoryRequest getRequest = new GetBucketInventoryRequest(bucket);
  getRequest.SetInventoryId(inventoryId);
  
  GetBucketInventoryResult getResult = cosXml.GetBucketInventory(getRequest);
  
  InventoryConfiguration configuration = getResult.inventoryConfiguration;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs)를 참고하십시오.

## 인벤토리 작업 삭제

#### 기능 설명

DELETE Bucket inventory는 버킷에서 지정된 인벤토리 작업을 삭제하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-delete-bucket-inventory)
```cs
try
{
  string inventoryId = "aInventoryId";
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  DeleteBucketInventoryRequest deleteRequest = new DeleteBucketInventoryRequest(bucket);
  deleteRequest.SetInventoryId(inventoryId);
  DeleteBucketInventoryResult deleteResult = cosXml.DeleteBucketInventory(deleteRequest);
  
  //요청 완료
  Console.WriteLine(deleteResult.GetResultInfo());
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs)를 참고하십시오.

