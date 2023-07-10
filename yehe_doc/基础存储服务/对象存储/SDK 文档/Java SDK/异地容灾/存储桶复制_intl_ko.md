## 소개

본문은 버킷 복제 관련 API 개요 및 SDK 코드 예시를 제공합니다.

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 버킷 복제 설정 | 버킷 복제 규칙 설정 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | 버킷 복제 쿼리 | 버킷 복제 규칙 쿼리 |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 버킷 복제 삭제 | 버킷 복제 규칙 삭제 |

## 버킷 복제 설정

#### 기능 설명

버킷 복제 규칙(PUT Bucket replication)을 설정합니다.

#### 메소드 프로토타입

```java
public void setBucketReplicationConfiguration(
        SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest)
                throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-put-bucket-replication)
```java
// appid를 포함한 소스 버킷 이름.
String bucketName = "examplebucket-1250000000";

BucketReplicationConfiguration bucketReplicationConfiguration = new BucketReplicationConfiguration();
// 요청자 ID 설정. 형식: qcs::cam::uin/<OwnerUin>:uin/<SubUin>.
bucketReplicationConfiguration.setRoleName("qcs::cam::uin/100000000001:uin/100000000001");

// 타깃 버킷 및 스토리지 유형 설정. QCS 형식: qcs::cos:[region]::[bucketname-AppId].
ReplicationDestinationConfig replicationDestinationConfig = new ReplicationDestinationConfig();
replicationDestinationConfig.setBucketQCS("qcs::cos:ap-beijing::destinationbucket-1250000000");
replicationDestinationConfig.setStorageClass(StorageClass.Standard);

// 규칙 상태 및 접두사 설정.
ReplicationRule replicationRule = new ReplicationRule();
replicationRule.setStatus(ReplicationRuleStatus.Enabled);
replicationRule.setPrefix("");
replicationRule.setDestinationConfig(replicationDestinationConfig);
// 규칙 추가
String ruleId = "replication-to-beijing";
bucketReplicationConfiguration.addRule(replicationRule);

SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest =
        new SetBucketReplicationConfigurationRequest(bucketName, bucketReplicationConfiguration);
cosClient.setBucketReplicationConfiguration(setBucketReplicationConfigurationRequest);
```



#### 매개변수 설명

| 매개변수                                   | 설명                                                     | 유형                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                   |
| setBucketReplicationConfigurationRequest | 버킷 복제 설정                                               | SetBucketReplicationConfigurationRequest |

#### 반환 결과 설명

  - 성공: 반환값 없음.
  - 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


## 버킷 복제 쿼리

#### 기능 설명

버킷 복제 규칙(GET Bucket replication)을 쿼리합니다.

#### 메소드 프로토타입
```java
// 버킷의 버킷 복제 설정 가져오기 방법 1
public BucketReplicationConfiguration getBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// 버킷의 버킷 복제 설정 가져오기 방법 2        
public BucketReplicationConfiguration getBucketReplicationConfiguration(
            GetBucketReplicationConfigurationRequest getBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// 버킷의 버킷 복제 설정 가져오기 방법 1
BucketReplicationConfiguration brcfRet = cosClient.getBucketReplicationConfiguration(bucketName);

// 버킷의 버킷 복제 설정 가져오기 방법 2
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
        new GetBucketReplicationConfigurationRequest(bucketName));
```


#### 매개변수 설명

| 매개변수                                   | 설명                                                     | 유형                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                   |
| getBucketReplicationConfigurationRequest | 버킷 복제 설정 가져오기 요청                                       | GetBucketReplicationConfigurationRequest |

#### 반환 결과 설명
- 성공: 버킷의 버킷 복제 규칙이 반환됨.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


## 버킷 복제 삭제

#### 기능 설명

버킷 복제 규칙(DELETE Bucket replication)을 삭제합니다.

#### 메소드 프로토타입
```java
// 버킷의 버킷 복제 설정 삭제 방법1
public void deleteBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// 버킷의 버킷 복제 설정 삭제 방법2        
public void deleteBucketReplicationConfiguration(
            DeleteBucketReplicationConfigurationRequest deleteBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// 버킷의 버킷 복제 설정 삭제 방법1
cosClient.deleteBucketReplicationConfiguration(bucketName);

// 버킷의 버킷 복제 설정 삭제 방법2
cosClient.deleteBucketReplicationConfiguration(new DeleteBucketReplicationConfigurationRequest(bucketName));
```


#### 매개변수 설명

| 매개변수                                      | 설명                                                     | 유형                                        |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| bucketName                                  | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                      |
| deleteBucketReplicationConfigurationRequest | 버킷 복제 설정 삭제 요청                                       | DeleteBucketReplicationConfigurationRequest |

#### 반환 결과 설명

  - 성공: 반환값 없음.
  - 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참고하십시오.
