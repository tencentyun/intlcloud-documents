## 소개

본문은 버킷 복제 관련 API 개요 및 SDK 코드 예시를 제공합니다.

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 버킷 복제 설정 | 버킷 복제 규칙 설정 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | 버킷 복제 쿼리 | 버킷 복제 규칙 쿼리 |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 버킷 복제 삭제 | 버킷 복제 규칙 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 복제 설정

#### 기능 설명

지정된 버킷에 대한 버킷 복제 규칙을 설정합니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-replication)
```cs
// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
string ownerUin = "100000000001"; //요청 발송자 식별: OwnerUin
string subUin = "100000000001"; //요청 발송자 식별: SubUin
PutBucketReplicationRequest request = new PutBucketReplicationRequest(bucket);
//replication 설정
PutBucketReplicationRequest.RuleStruct ruleStruct = 
  new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; //특정 Rule 이름 표시
ruleStruct.isEnable = true; //Rule 적용 여부 식별. true: 적용, false: 미적용
ruleStruct.appid = "1250000000"; //APPID
ruleStruct.region = "ap-beijing"; //타깃 스토리지 리전 정보
ruleStruct.bucket = "destinationbucket-1250000000"; //형식: BucketName-APPID
ruleStruct.prefix = "34"; //접두사 매칭 정책
List<PutBucketReplicationRequest.RuleStruct> ruleStructs = 
  new List<PutBucketReplicationRequest.RuleStruct>();
ruleStructs.Add(ruleStruct);
request.SetReplicationConfiguration(ownerUin, subUin, ruleStructs);

try
{
  PutBucketReplicationResult result = cosXml.PutBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReplication.cs)을 참고하십시오.

## 버킷 복제 쿼리

#### 기능 설명

지정된 버킷의 버킷 복제 규칙을 쿼리합니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-replication)
```cs
// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
GetBucketReplicationRequest request = new GetBucketReplicationRequest(bucket);
try
{
  GetBucketReplicationResult result = cosXml.GetBucketReplication(request);
  // 버킷의 교차 리전 복제 설정
  ReplicationConfiguration conf =  result.replicationConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReplication.cs)을 참고하십시오.

## 버킷 복제 삭제

#### 기능 설명

지정된 버킷에 대한 버킷 복사 규칙을 삭제합니다.

#### 예시 코드

[//]: # (.cssg-snippet-delete-bucket-replication)
```cs
// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
DeleteBucketReplicationRequest request = new DeleteBucketReplicationRequest(bucket);
try
{
  DeleteBucketReplicationResult result = cosXml.DeleteBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReplication.cs)을 참고하십시오.

