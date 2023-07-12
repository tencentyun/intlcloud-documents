## 소개

본문은 버킷 Referer 에 대한 화이트/블랙리스트의 API 개요 및 SDK 예시 코드를 제공합니다.

>! COS Java SDK v5.6.52 또는 그 이후 버전이 필요합니다.
>

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 버킷 Referer 설정 | 버킷 Referer 화이트 또는 블랙리스트 설정 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 버킷 Referer 쿼리| 버킷 Referer 화이트 또는 블랙리스트 쿼리 |

## 버킷 Referer 설정

#### 기능 설명

버킷의 Referer의 화이트 또는 블랙리스트를 설정합니다(PUT Bucket referer).

#### 메소드 프로토타입

```java
public void setBucketRefererConfiguration(String bucketName, BucketRefererConfiguration configuration) throws CosClientException, CosServiceException;

public void setBucketRefererConfiguration(SetBucketRefererConfigurationRequest setBucketRefererConfigurationRequest) throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// 소스 버킷 이름. appid를 포함해야 함
String bucketName = "examplebucket-1250000000";

BucketRefererConfiguration configuration = new BucketRefererConfiguration();

// 링크 도용 방지 활성화
configuration.setStatus(BucketRefererConfiguration.DISABLED);
// 링크 도용 방지 유형을 화이트리스트로 설정
//configuration.setRefererType(BucketRefererConfiguration.WHITELIST);
// 링크 도용 방지 유형을 블랙리스트로 설정(화이트리스트와 둘 중 하나 선택)
configuration.setRefererType(BucketRefererConfiguration.BLACKLIST);

// 설정할 도메인 입력
configuration.addDomain("test.com");
configuration.addDomain("test.1.com");

//(옵션)빈 링크 도용 방지 액세스 허용 여부. 기본값: DENY.
configuration.setEmptyReferConfiguration(BucketRefererConfiguration.DENY);
// configuration.setEmptyReferConfiguration(BucketRefererConfiguration.ALLOW);

cosClient.setBucketRefererConfiguration(bucketName, configuration);
```

#### 매개변수 설명

| 매개변수 이름                                   | 매개변수 설명                                                     | 유형                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                   |
| configuration | 버킷 Referer 설정                                               | BucketRerfererConfiguration |

BucketReferreConfiguration 설명:

| 매개변수 이름          | 매개변수 설명                                         | 유형    | 필수 여부 | 메소드      |
| -------------- | ----------------------------------------------- | ------ | ---- | -------- |
| Status         | 링크 도용 방지 활성화 여부, 열거 값: Enabled、Disabled           | String | 필수   | setStatus |
| RefererType    | 링크 도용 방지 유형 열거 값: Black-List, White-List          | String | 필수   | setRefererType |
| Domain         | 유효 도메인. 포트, IP 및 와일드카드 지원\*. 다중 지원.        | String | 필수   | addDomain |
| EmptyReferConfiguration | 빈 Refer 액세스 허용 여부, 열거 값: Allow、Deny | String | 옵션  | setEmptyReferConfiguration |

#### 반환 결과 설명

  - 성공: 반환값 없음.
  - 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

## 버킷 Referer 쿼리

#### 기능 설명

버킷의 Referer의 화이트 또는 블랙리스트를 쿼리합니다(PUT Bucket referer).

#### 메소드 프로토타입

```java
public BucketRefererConfiguration getBucketRefererConfiguration(String bucketName) throws CosClientException, CosServiceException
```

#### 요청 예시

```java
// 소스 버킷 이름. appid를 포함해야 함
String bucketName = "examplebucket-1250000000";

BucketRefererConfiguration configuration = cosClient.getBucketRefererConfiguration(bucketName);

if (configuration == null) {
    System.out.printf("bucket %s does not have referer configuration\n", bucketName);
    return;
}

System.out.printf("status: %s\n", configuration.getStatus());
System.out.printf("referer type: %s\n", configuration.getRefererType());
System.out.printf("empty referer config: %s\n", configuration.getEmptyReferConfiguration());

for (String domain : configuration.getDomainList()) {
    System.out.printf("domain: %s\n", domain);
}
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명  | 유형  |
| ----------- | -------- | ---- |
| bucketName  | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                   |

#### 반환 결과 설명

- 성공: 버킷의 Referer의 화이트 또는 블랙리스트 반환.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.
