

## 소개

본 문서에서는 버킷 태그에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                       |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 버킷 태그 설정 | 기존 버킷에 대한 태그 설정 |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 버킷 태그 조회 | 지정된 버킷의 기존 버킷 태그 조회 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 버킷 태그 삭제 | 지정된 버킷 태그 삭제 |

버킷 태그 설정

#### 기능 설명

PUT Bucket tagging 기존 버킷의 태그를 설정하는 데 사용됩니다.

#### 메소드 프로토타입

```java
public void setBucketTaggingConfiguration(SetBucketTaggingConfigurationRequest setBucketTaggingConfigurationRequest);
public void setBucketTaggingConfiguration(String bucketName, BucketTaggingConfiguration bucketTaggingConfiguration);
```

#### 요청 예시

[//]: # (.cssg-snippet-put-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
List<TagSet> tagSetList = new LinkedList<TagSet>();
TagSet tagSet = new TagSet();
tagSet.setTag("age", "18");
tagSet.setTag("name", "xiaoming");
tagSetList.add(tagSet);
BucketTaggingConfiguration bucketTaggingConfiguration = new BucketTaggingConfiguration();
bucketTaggingConfiguration.setTagSets(tagSetList);
SetBucketTaggingConfigurationRequest setBucketTaggingConfigurationRequest =
new SetBucketTaggingConfigurationRequest(bucketName, bucketTaggingConfiguration);
cosClient.setBucketTaggingConfiguration(setBucketTaggingConfigurationRequest);
```

#### 매개변수 설명

| 매개변수 이름         | 설명                                                         | 유형             |
| ------------------------------------ | ------------------ | ------------------------------------ |
| setBucketTaggingConfigurationRequest | 버킷 태그 설정 요청 | SetBucketTaggingConfigurationRequest |

Request 멤버 설명:

| Request 멤버    | 설정 방법            | 설명                                                         | 유형                    |
| -------------------- | ------------------- | ------------------------------------------------------------ | -------------------------- |
| bucketName   | 생성자 또는 set 메소드 | 태그 설정 버킷. 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         |
| taggingConfiguration | 생성자 또는 set 메소드 | 버킷의 태그 설정                                             | BucketTaggingConfiguration |

BucketLoggingConfiguration 멤버 설명:

| 매개변수 이름 | 설명                                                         | 유형   |
| -------- | -------------------- | ------------ |
| tagSets  | 버킷의 태그 구성 집합 | List&lt;TagSet&gt; |

TagSet 멤버 설명：

| 매개변수 이름         | 설명                                                         | 유형             |
| -------- | ------------------------------------------------------------ | ------------------- |
| tags     | 태그의 Key 및 Value, 길이는 128바이트를 초과할 수 없습니다. Key 및 Value는 영어, 숫자, 공백, 더하기 기호, 빼기 기호, 언더바, 등호, 마침표, 콜론, 슬래시를 지원합니다. | Map&lt;String, String&gt; |

#### 반환 결과 설명

- 성공: 반환값이 없습니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 혹은 CosServiceException 오류 발생. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537) 참조.

## 버킷 태그 조회

#### 기능 설명

GET Bucket tagging 지정된 버킷의 기존 버킷 태그를 조회하는 데 사용됩니다.

#### 메소드 프로토타입

```java
public BucketTaggingConfiguration getBucketTaggingConfiguration(String bucketName);
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
BucketTaggingConfiguration bucketTaggingConfiguration = cosClient.getBucketTaggingConfiguration(bucketName);
```

#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 태그 조회 버킷. 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |

#### 반환 결과 설명

- 성공：버킷의 태그 설정 정보를 포함한 BucketTaggingConfiguration를 반환.
- 실패: 오류가 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참고하십시오.

## 버킷 태그 삭제

#### 기능 설명

DELETE Bucket tagging 지정된 버킷의 기존 버킷 태그를 삭제하는 데 사용됩니다.

#### 메소드 프로토타입

```java
public void deleteBucketTaggingConfiguration(String bucketName);
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketTaggingConfiguration(bucketName);
```

#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 태그 삭제 버킷. 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String             |

#### 반환 결과 설명

- 성공: 반환값이 없습니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 혹은 CosServiceException 오류 발생. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참고하십시오.
