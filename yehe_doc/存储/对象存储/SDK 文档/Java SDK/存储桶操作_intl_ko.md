## 소개


본 문서에서는 버킷의 기본 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | 버킷 리스트 조회     | 특정 계정의 모든 버킷 리스트 조회     |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 버킷 생성         | 지정 계정에서 버킷 생성         |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 버킷 및 해당 권한 인덱스 | 버킷 존재 여부 및 액세스 권한 보유 여부 인덱스 |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 버킷 삭제         | 지정 계정의 빈 버킷 삭제           |



## 버킷 리스트 조회

#### 기능 설명

지정 계정의 모든 버킷 리스트를 조회합니다.

#### 메소드 프로토타입

```java
public List<Bucket> listBuckets() throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-get-service)
```java
// listBuckets 메소드만 호출하면 cosClient 생성 시 region을 new Region("")으로 지정하면 됩니다.
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```


#### 매개변수 설명

없음

#### 반환 결과 설명

- 성공: 모든 Bucket류의 목록을 반환합니다. Bucket류에는 bucket 멤버, location 등 정보가 포함됩니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참고하십시오.


## 버킷 생성

#### 기능 설명

지정된 계정에 버킷을 생성합니다. 동일한 사용자 계정으로 여러 개의 버킷을 생성할 수 있으며, 최대 200개(리전 구분 없음) 생성 가능하며 버킷의 객체 수에는 제한이 없습니다. 버킷 생성은 빈도가 낮은 작업으로 일반적으로 콘솔에서 Bucket을 생성하고 SDK에서 객체 작업을 수행하는 것을 추천합니다.

#### 메소드 프로토타입

```java
public Bucket createBucket(String  bucketName) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-put-bucket)
```java
String bucket = "examplebucket-1250000000"; //버킷 이름, 형식: BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// bucket의 권한을 Private(개인 읽기/쓰기)으로 설정(기타 옵션: 공개 읽기 및 개인 쓰기, 공개 읽기/쓰기)
createBucketRequest.setCannedAcl(CannedAccessControlList.Private);
Bucket bucketResult = cosClient.createBucket(createBucketRequest);
```


#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName   | Bucket의 이름 생성 규칙은 BucketName-APPID이며 세부 사항은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312)를 참고하십시오 | String                  |

#### 반환 결과 설명

- 성공: 버킷에 대한 설명(버킷 이름, 소유자 및 생성 날짜)을 포함한 버킷류.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참고하십시오.


## 버킷 및 해당 권한 인덱스

#### 기능 설명

버킷의 존재 여부 및 액세스 권한 보유 여부를 인덱스합니다.

#### 메소드 프로토타입

```java
public boolean doesBucketExist(String bucketName) 
  throws CosClientException, CosServiceException;
```

#### 요청 샘플

[//]: # (.cssg-snippet-head-bucket)
```java
// bucket의 이름 생성 규칙은 BucketName-APPID입니다. 여기에 입력되는 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
boolean bucketExistFlag = cosClient.doesBucketExist(bucketName);
```


#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName   | Bucket의 이름 생성 규칙은 BucketName-APPID이며 세부 사항은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오 | String                  |

#### 반환 결과 설명

- 성공：존재할 시 true 반환，아닐 시 false。
- 실패: 오류가 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참고하십시오.


## 버킷 삭제

#### 기능 설명

지정 계정의 빈 버킷을 삭제합니다.

#### 메소드 프로토타입

```java
public void deleteBucket(String bucketName) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-bucket)
```java
// bucket의 이름 생성 규칙은 BucketName-APPID입니다. 여기에 입력되는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucket(bucketName);
```



#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName   | Bucket의 이름 생성 규칙은 BucketName-APPID이며 세부 사항은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312)를 참고하십시오. | String                  |

#### 반환 결과 설명

- 성공: 반환값이 없습니다.
- 실패: 오류 발생(실명 인증 실패). CosClientException 혹은 CosServiceException 오류 발생. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참고하십시오.


