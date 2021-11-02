## 소개

본 문서는 객체 태그에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 객체 태그 설정 | 객체의 태그 설정       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 객체 태그 조회 | 지정한 객체의 기존 태그 조회 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 객체 태그 삭제 | 지정한 객체의 기존 태그 삭제 |


## 객체 태그 설정

#### 기능 설명

객체의 태그를 설정하는 데 사용됩니다.

#### 메소드 프로토타입

```java
public SetObjectTaggingResult setObjectTagging(SetObjectTaggingRequest setObjectTaggingRequest);
```

#### 요청 예시 1: 업로드된 객체의 태그 설정

```java
String bucketName = "examplebucket-1250000000";
String key = "exampletkey";
List<Tag> tags = new LinkedList<>();
tags.add(new Tag("tag1", "value1"));
tags.add(new Tag("tag2", "value2"));
ObjectTagging objectTagging = new ObjectTagging(tags);
SetObjectTaggingRequest setObjectTaggingRequest = new SetObjectTaggingRequest(bucketName, key, objectTagging);
cosclient.setObjectTagging(setObjectTaggingRequest);
```

#### 요청 예시 2: 객체 업로드 시 태그 설정

```java
String bucketName = "examplebucket-1250000000";
String key = "testfiles/testTagging.txt";
InputStream is = new ByteArrayInputStream(new byte[]{’d’, ’a’, ’t’, ’a’});
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setHeader("x-cos-tagging", "tag1=value1&tag2=value2");
cosclient.putObject(bucketName, key, is, objectMetadata);
```

#### 매개변수 설명

| 매개변수 이름                             | 설명               | 유형                                 |
| ------------------------------------ | ------------------ | ------------------------------------ |
| setObjectTaggingRequest | 객체 태그 설정 요청 | SetObjectTaggingRequest |

Request 멤버 설명:

| Request 멤버         | 설정 메소드            | 설명                      | 유형                       |
| -------------------  | ----------------- | ------------------------ | -------------------------- |
| bucketName  | 생성자 또는 set 메소드 | 태그를 설정한 객체의 버킷 이름, 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key | 생성자 또는 set 메소드 | 태그를 설정한 객체 키, 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| objectTagging | 생성자 또는 set 메소드 | 객체 태그 설정 | ObjectTagging |

ObjectTagging 멤버 설명:

| 매개변수 이름 | 설명 | 유형 |
| ------  | ---- | ---- |
| tagSet | 객체의 태그 설정 모음 | List&lt;Tag> |

Tag 멤버 설명:

| 매개변수 이름 | 설명 | 유형 |
| ----- | ---- | ---- |
| key | 태그의 key | String |
| value | 태그의 value | String |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

## 객체 태그 조회

### 기능 설명

지정한 객체의 기존 객체 태그를 조회합니다.

#### 메소드 프로토타입

```java
public GetObjectTaggingResult getObjectTagging(GetObjectTaggingRequest getObjectTaggingRequest);
```

#### 요청 예시

```java
String bucketName = "exampletbucket-1250000000";
String key = "exampletkey";
GetObjectTaggingRequest getObjectTaggingRequest = new GetObjectTaggingRequest(bucketName, key);
GetObjectTaggingResult getObjectTaggingResult = cosclient.getObjectTagging(getObjectTaggingRequest);
List<Tag> resultTagSet = getObjectTaggingResult.getTagSet();
System.out.println(resultTagSet.toString());
```

#### 매개변수 설명

| 매개변수 이름   | 설명        | 유형   |
| ---------- | ---------- | ------ |
| getObjectTaggingRequest | 객체 태그 조회 요청 | GetObjectTaggingRequest |

Request 멤버 설명:

| Request 멤버         | 설정 방법            | 설명                      | 유형                       |
| -------------------- | ----------------- | ------------------------ | ------------------------- |
| bucketName  | 생성자 또는 set 메소드 | 태그를 설정한 객체의 버킷 이름, 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key | 생성자 또는 set 메소드 | 태그를 설정한 객체 키, 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |

#### 반환 결과 설명

- 성공: 객체의 태그 정보를 포함한 GetObjectTaggingResult를 반환.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

## 객체 태그 삭제

#### 기능 설명

지정한 객체의 기존 태그를 삭제하는 데 사용됩니다.

#### 메소드 프로토타입

```java
public DeleteObjectTaggingResult deleteObjectTagging(DeleteObjectTaggingRequest deleteObjectTaggingRequest);
```

#### 요청 예시

```java
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
DeleteObjectTaggingRequest deleteObjectTaggingRequest = new DeleteObjectTaggingRequest(bucketName, key);
cosclient.deleteObjectTagging(deleteObjectTaggingRequest);
```

#### 매개변수 설명

| 매개변수 이름   | 설명        | 유형   |
| --------- | ---------- | ------ |
| deleteObjectTaggingRequest | 객체 태그 삭제 요청 | DeleteObjectTaggingRequest |

Request 멤버 설명:

| Request 멤버         | 설정 메소드            | 설명                      | 유형                       |
| -------------------- | ------------------ | ----------------------- | -------------------------- |
| bucketName  | 생성자 또는 set 메소드 | 태그를 설정한 객체의 버킷 이름, 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key | 생성자 또는 set 메소드 | 태그를 설정한 객체 키, 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.
