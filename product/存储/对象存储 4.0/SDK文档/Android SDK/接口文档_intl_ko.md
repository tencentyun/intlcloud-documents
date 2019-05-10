COS 서비스 XML Android SDK 작업에 성공하면 API별 해당 유형을 반환하게 되고, 실패하면 CosXmlClientException과 CosXmlServiceException을 throw합니다. 그 중 CosXmlClientException은 클라이언트 이상, 매개변수가 비어 있으면 네트워크 연결 실패 등입니다. 존재하지 않는 파일 접근이나 파일 접근 권한이 없음 등 CosXmlServiceException이란 서버가 요구 조건에 부합하지 않는 클라이언트 요청을 처리할 때 반환하는 오류를 가리킵니다. 자세한 내용은 [SDK 이상 정보 설명](#sdk_exception)을 참조하십시오.

SDK에는 API 요청별로 동기화와 비동기 두 가지 요청 방식을 제공하였습니다.

## Bucket API 설명

## Put Bucket

이 API를 호출하면 지정 계정에서 버킷 1개를 생성하게 됩니다. 구체적인 절차는 다음과 같습니다.

1. **PutBucketRequest(String)** 생성자 함수를 호출하여 PutBucketRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putBucket 방식을 호출하고 PutBucketRequest를 전달하며 PutBucketResult 객체를 반환합니다.
   (또는 putBucketAsync 방식을 호출하고, PutBucketRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다)

```c
PutBucketResult putBucket(PutBucketRequest request) throws CosXmlClientException, CosXmlServiceException;
void putBucketAsync(PutBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

PutBucketResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```
String bucket = "bucket";
PutBucketRequest putBucketRequest = new PutBucketRequest(bucket);

//Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read, 기본값: private
putBucketRequest.setXCOSACL("private");

//권한 부여받은 자에게 읽기 권한 부여
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(readACLS);

//권한 부여받은 자에게 쓰기 권한 부여
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(writeACLS);

//권한 부여받은 자에게 읽기/쓰기 권한 부여
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(writeandReadACLS);

//동기화 방법 사용
try {
    PutBucketResult putBucketResult = cosXmlService.putBucket(putBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.putBucketAsync(putBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putBucketRequst.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Delete Bucket 

이 API를 호출하면 지정 계정에서 버킷을 삭제할 수 있으며, 삭제 전에는 버킷 내용이 비어 있어야 합니다. 버킷 내부 모든 객체를 삭제해야만 버킷 자체를 삭제할 수 있습니다. 구체적인 절차는 다음과 같습니다.

1. **DeleteBucketRequest(String)** 생성자 함수를 호출하여 DeleteBucketRequest 객체를 인스턴스화합니다.
2. CosXmlService의 deleteBucket 방식을 호출하고 DeleteBucketRequest를 전달해 DeleteBucketResult 객체를 반환합니다.
   (또는 deleteBucketAsync 방식을 호출하고 DeleteBucketRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다)

```java
DeleteBucketResult deleteBucket(DeleteBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketAsync(DeleteBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

DeleteBucketResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
DeleteBucketRequest deleteBucketRequest = new DeleteBucketRequest(bucket);

// 동기화 방법 사용
try {
    DeleteBucketResult deleteBucketResult = cosXmlService.deleteBucket(deleteBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.deleteBucketAsync(deleteBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `deleteBucketRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Head Bucket

이 API를 호출하면 지정 버킷 존재 여부를 확인하게 됩니다. 구체적인 절차는 다음과 같습니다.

1. HeadBucketRequest(String) 생성자 함수를 호출하여 HeadBucketRequest 객체를 인스턴스화합니다.
2. CosXmlService의 headBucket 방식을 호출하고 HeadBucketRequest 전달하며 HeadBucketResult 객체를 반환합니다.
   (또는 headBucketAsync 방식을 호출하고, HeadBucketRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다)

```java
HeadBucketResult headBucket(HeadBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void headBucketAsync(HeadBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

PutBucketResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
HeadBucketRequest headBucketRequest = new HeadBucketRequest(bucket);

//동기화 방법 사용
try {
    HeadBucketResult headBucketResult = cosXmlService.headBucket(headBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.headBucketAsync(headBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Head Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `headBucketRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Get Bucket Location

이 API는 버킷 소재 지역 정보 획득에 사용됩니다. 구체적인 절차는 다음과 같습니다.

1. **GetBucketLocationRequest(String)** 생성자 함수를 호출하여 GetBucketLocationRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getBucketLocation 방식을 호출하고 GetBucketLocationRequest를 전달하며 GetBucketLocationResult 객체를 반환합니다.
   (또는 getBucketLocationAsync 방식을 호출하고 GetBucketLocationRequestd와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다)

```java
GetBucketLocationResult getBucketLocation(GetBucketLocationRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLocationAsync(GetBucketLocationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

GetBucketLocationResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름       | 변수 설명                              | 유형               |
| ------------------ | ------------------------------------- | ------------------ |
| locationConstraint | 버킷 소재 지역                       | LocationConstraint |
| httpCode           | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int                |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
GetBucketLocationRequest getBucketLocationRequest = new GetBucketLocationRequest(bucket);

//동기화 방법 사용
try {
    GetBucketLocationResult getBucketLocationResult = cosXmlService.getBucketLocation(getBucketLocationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.getBucketLocationAsync(getBucketLocationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket Location
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Location failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketLocationRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Get Bucket(모든 Objects 열거)

이 API를 호출하면 해당 버킷의 일부 또는 전체 Object를 열거하게 됩니다. 구체적인 절차는 다음과 같습니다.

1. **GetBucketRequest(String)** 생성자 함수를 호출하여 GetBucketRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getBucket 방식을 호출하고 GetBucketRequest를 전달하며 GetBucketResult 객체를 반환합니다.
   (또는 getBucketAsync 방식을 호출하고 GetBucketRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다)

```java
GetBucketResult getBucket(GetBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketAsync(GetBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

GetBucketResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형       |
| ------------ | ------------------------------------- | ---------- |
| listBucket   | Get Bucket 요청 결과의 모든 정보 저장    | ListBucket |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int        |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";  
GetBucketRequest getBucketRequest = new GetBucketRequest(bucket);

//접두사 매칭, 반환된 파일 접두사 주소를 규정하는 데 사용됩니다
getBucketRequest.setPrefix("prefix");

//1회 최대 반환 항목 수량, 기본값은 1000
getBucketRequest.setMaxKeys(100);

//구분자는 하나의 문자이며, Prefix가 있을 경우,
//Prefix부터 delimiter까지의 동일 경로를 하나의 유형으로 분류하고 Common Prefix라 정의합니다.
//그런 다음 모든 Common Prefix를 나열합니다. Prefix가 없으면 경로 기점에서 시작합니다.
getBucketRequest.setDelimiter('/');

// 동기화 방법 사용
try {
    GetBucketResult getBucketResult = cosXmlService.getBucket(getBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Put Bucket ACL

이 API를 호출하면 버킷의 접근 제어 권한을 지정할 수 있습니다. 구체적인 절차는 다음과 같습니다.

1. **PutBucketACLRequest(String)** 생성자 함수를 호출하여 PutBucketACLRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putBucketACL 방식을 호출하고 PutBucketACLRequest를 전달해 PutBucketACLResult 객체를 반환합니다.
   (또는 putBucketACLAsync 방식을 호출하고 PutBucketACLRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
PutBucketACLResult putBucketACL(PutBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketACLAsync(PutBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| xcosACL                   | 버킷 접근 권한을 설정합니다. 유효값: private, public-read-write, public-read. 기본값: private | String               | 아니요   |
| xcosGrantRead             | 권한 부여받은 자에게 읽기 권한 부여                                         | ACLAccount           | 아니요   |
| xcosGrantWrite            | 권한 부여받은 자에게 기 권한 부여                                         | ACLAccount           | 아니요   |
| xcosGrantRead             | 권한 부여받은 자에게 읽기/쓰기 권한 부여                                       | ACLAccount           | 아니요   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

PutBucketACLResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
PutBucketACLRequest putBucketACLRequest = new PutBucketACLRequest(bucket);

//버킷 접근 권한 설정
putBucketACLRequest.setXCOSACL("public-read");

//권한 부여받은 자에게 읽기 권한 부여
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(readACLS);

//권한 부여받은 자에게 쓰기 권한 부여
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(writeACLS);

//권한 부여받은 자에게 읽기/쓰기 권한 부여
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(writeandReadACLS);

// 동기화 방법 사용
try {
    PutBucketACLResult putBucketACLResult = cosXmlService.putBucketACL(putBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 콜백으로 요청 콜백
cosXmlService.putBucketACLAsync(putBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putBucketACLRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.

## Get Bucket ACL

이 API는 버킷의 ACL 획득에 사용됩니다. 구체적인 절차는 다음과 같습니다.

1. **GetBucketACLRequest(String)** 생성자 함수를 호출하여 GetBucketACLRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getBucketACL 방식을 호출하고 GetBucketACLRequest를 전달해 GetBucketACLResult 객체를 반환합니다.
   (또는 getBucketACLAsync 방식을 호출하고 GetBucketACLRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
GetBucketACLResult getBucketACL(GetBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketACLAsync(GetBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

GetBucketACLResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름        | 변수 설명                                                     | 유형                |
| ------------------- | ------------------------------------------------------------ | ------------------- |
| accessControlPolicy | [권한 부여받은 자 정보와 권한 정보](https://cloud.tencent.com/document/product/436/7733) | AccessControlPolicy |
| httpCode            | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패                        | Int                 |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
GetBucketACLRequest getBucketACLRequest = new GetBucketACLRequest(bucket);

// 동기화 방법 사용
try {
    GetBucketACLResult getBucketACLResult = cosXmlService.getBucketACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 콜백으로 요청 콜백
cosXmlService.getBucketACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketACLRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


### Put Bucket CORS

이 API를 호출하면 지정 버킷에서 CORS 구성 정보가 설정됩니다. 구체적인 절차는 다음과 같습니다.

1. **PutBucketCORSRequest(String)** 생성자 함수를 호출하여 PutBucketCORSRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putBucketCORS 방식을 호출하고 PutBucketCORSRequest를 전달해 PutBucketCORSResult 객체를 반환합니다.
   (또는 putBucketCORSAsync 방식을 호출하고 PutBucketCORSRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
 PutBucketCORSResult putBucketCORS(PutBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketCORSAsync(PutBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                       | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 bucket 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String                     | 예   |
| cORSRule                  | CORS 구성 정보                                             | CORSConfiguration.CORSRule | 예   |
| signDuration              | 서명의 유효 기간, 단위는 초입니다.                                       | Long                       | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>             | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>             | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

PutBucketCORSResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
PutBucketCORSRequest putBucketCORSRequest = new PutBucketCORSRequest(bucket);
    
/**
 * CORSConfiguration.cORSRule: CORS 구성 정보
 * corsRule.id: 규칙의 ID 구성
 * corsRule.allowedOrigin: 허가된 접근 출처, 와일드카드 *를 지원하며 형식은 프로토콜://도메인 이름[:포트]입니다. 예: http://www.qq.com
 * corsRule.maxAgeSeconds: OPTIONS 요청의 얻은 결과의 유효 기간을 설정합니다.
 * corsRule.allowedMethod: 허가된 HTTP 작업. 예: GET, PUT, HEAD, POST, DELETE
 * corsRule.allowedHeader: OPTIONS 요청을 발송할 때 서버에 다음 요청은 어느 사용자 지정의 HTTP 요청 헤더를 사용할 수 있는지 알립니다. 와일드카드 *를 지원합니다.
 * corsRule.exposeHeader: 웹 브라우저가 수신할 수 있는 서버 출처의 사용자 지정 헤더 정보를 설정합니다.
 */
CORSConfiguration.CORSRule corsRule = new CORSConfiguration.CORSRule();

corsRule.id = "123";
corsRule.allowedOrigin = "https://cloud.tencent.com";
corsRule.maxAgeSeconds = 5000;

List<String> methods = new LinkedList<>();
methods.add("PUT");
methods.add("POST");
methods.add("GET");
corsRule.allowedMethod = methods;

List<String> headers = new LinkedList<>();
headers.add("host");
headers.add("content-type");
corsRule.allowedHeader = headers;

List<String> exposeHeaders = new LinkedList<>();
headers.add("x-cos-metha-1");
corsRule.exposeHeader = headers;

//CORS 구성 정보 설정
putBucketCORSRequest.addCORSRule(corsRule);

// 동기화 방법 사용
try {
    PutBucketCORSResult putBucketCORSResult = cosXmlService.putBucketCORS(putBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.putBucketCORSAsync(putBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket CORS success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putBucketCORSRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


### Get Bucket CORS

이 API를 호출하면 지정 버킷에서 CORS 구성 정보를 획득하게 됩니다. 구체적인 절차는 다음과 같습니다.

1. **GetBucketCORSRequest(String)** 생성자 함수를 호출하여 GetBucketCORSRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getBucketCORS 방식을 호출하고 GetBucketCORSRequest를 전달해 GetBucketCORSResult 객체를 반환합니다.
   (또는 getBucketCORSAsync 방식을 호출하고 GetBucketCORSRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
GetBucketCORSResult getBucketCORS(GetBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketCORSAsync(GetBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

GetBucketCORSResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름      | 유형                                                         | 변수 설명          |
| ----------------- | ------------------------------------------------------------ | ----------------- |
| cORSConfiguration | [CORS 구성의 모든 정보](https://cloud.tencent.com/document/product/436/8274) | CORSConfiguration |
| httpCode          | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패                        | Int               |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
GetBucketCORSRequest getBucketCORSRequest = new GetBucketCORSRequest(bucket);

//동기화 방법 사용
try {
    GetBucketCORSResult getBucketCORSResult = cosXmlService.getBucketCORS(getBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.getBucketCORSAsync(getBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket CORS success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketCORSRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Delete Bucket CORS

이 API를 호출하면 지정 버킷에서 CORS 구성 정보가 삭제됩니다. 구체적인 절차는 다음과 같습니다.

1. **DeleteBucketCORSRequest(String)** 생성자 함수를 호출하여 DeleteBucketCORSRequest 객체를 인스턴스화합니다.
2. CosXmlService의 deleteBucketCORS 방식을 호출하고 DeleteBucketCORSRequest를 전달해 DeleteBucketCORSResult 객체를 반환합니다. 
   (또는 deleteBucketCORSAsync 방식을 호출하고 DeleteBucketCORSRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
DeleteBucketCORSResult deleteBucketCORS(DeleteBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketCORSAsync(DeleteBucketCORSRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

DeleteBucketCORSResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
DeleteBucketCORSRequest deleteBucketCORSRequest = new DeleteBucketCORSRequest(bucket);

// 동기화 방법 사용
try {
    DeleteBucketCORSResult deleteBucketCORSResult = cosXmlService.deleteBucketCORS(deleteBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.deleteBucketCORSAsync(deleteBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket CORS success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `deleteBucketCORSRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Put Bucket Versioning

이 API는 버킷의 다중 버전 관리 기능을 설정하는 데 사용됩니다. 구체적인 절차는 다음과 같습니다.
1. PutBucketVersioningRequest 생성자 함수를 호출하여 PutBucketVersioningRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putBucketVersioning(PutBucketVersioningRequest) 동기화 방식을 호출해 PutBucketVersioningRequest를 전달하고 PutBucketVersioningResult 객체를 반환합니다(또는 putBucketVersionAsync 방식을 호출하고 PutBucketVersioningRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
PutBucketVersioningResult putBucketVersioning(PutBucketVersioningRequest request)throws CosXmlClientException, CosXmlServiceException;

void putBucketVersionAsync(PutBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| isEnable                  | 다중 버전 관리 기능 활성화 여부. true는 활성화, 그렇지 않으면 false입니다.              | boolean              | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

PutBucketVersioningResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
PutBucketVersioningRequest putBucketVersioningRequest = new PutBucketVersioningRequest(bucket);
request.setEnableVersion(true);//활성화

// 동기화 요청 사용
try {
    PutBucketVersioningResult putBucketVersioningResult = cosXmlService.putBucketVersioning(putBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.putBucketVersionAsync(putBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Object success
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putBucketVersioningRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Get Bucket Versioning

이 API를 호출하면 지정 버킷의 다중 버전 구성 정보를 획득하게 됩니다. 구체적인 절차는 다음과 같습니다.

1. GetBucketVersioningRequest 생성자 함수를 호출하여 GetBucketVersioningRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getBucketVersioning(GetBucketVersioningRequest) 동기화 방식을 호출해 GetBucketVersioningRequest를 전달하고 GetBucketVersioningResult 객체를 반환합니다(또는 getBucketVersioningAsync 방식을 호출하고 GetBucketVersioningRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
GetBucketVersioningResult getBucketVersioning(GetBucketVersioningRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketVersioningAsync(GetBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

GetBucketVersioningResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름            | 변수 설명                              | 유형                    |
| ----------------------- | ------------------------------------- | ----------------------- |
| versioningConfiguration | 멀티 버전 구성 정보                        | VersioningConfiguration |
| httpCode                | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int                     |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
GetBucketVersioningRequest getBucketVersioningRequest = new GetBucketVersioningRequest(bucket);
    
// 동기화 요청 사용
try {
    GetBucketVersioningResult getBucketVersioningResult = cosXmlService.getBucketVersioning(getBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 콜백으로 요청 콜백
cosXmlService.getBucketVersioningAsync(getBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Bucket Versioning success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketVersioningRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


#### Put Bucket Replication

이 API를 호출하면 다른 지역의 버킷 사이에 비동기 복사 기능이 구성됩니다. 구체적인 절차는 다음과 같습니다.

1. PutBucketReplicationRequest 생성자 함수를 호출하여 PutBucketReplicationRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putBucketReplication(PutBucketReplicationRequest) 동기화 방식을 호출해 PutBucketReplicationRequest를 전달하고 PutBucketReplicationResult 객체를 반환합니다(또는 putBucketReplicationAsync 방식을 호출하고 PutBucketReplicationRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
PutBucketReplicationResult putBucketReplication(PutBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;

void putBucketReplicationAsync(PutBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| ownerUin                  | replication의 개시자 신분 ID Owner Uin 설정                   | String               | 예   |
| subUin                    | replication의 개시자 신분 ID sub Uin 설정                     | String               | 예   |
| ruleStruct                | 지역 간 구성 정보, 최대 1000개까지 지원할 수 있으며, 모든 정책은 1개의 대상 버킷만 지향할 수 있습니다. | RuleStruct           | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

PutBucketReplicationResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
PutBucketReplicationRequest putBucketReplicationRequest = new PutBucketReplicationRequest(bucket);
PutBucketReplicationRequest.RuleStruct ruleStruct = new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_id";
ruleStruct.isEnable = true;
ruleStruct.appid = "1253960454";
ruleStruct.bucket = "replicationtest";
ruleStruct.region = "ap-beijing";
putBucketReplicationRequest.setReplicationConfigurationWithRule(ruleStruct);
putBucketReplicationRequest.setReplicationConfigurationWithRole("ownerUin", "subUin");

// 동기화 요청 사용    
try {
    PutBucketReplicationResult result = cosXmlService.putBucketReplication(putBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 요청 사용    
cosXmlService.putBucketReplicationAsync(putBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Put Bucket Replication success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket Replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putBucketReplicationRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Get Bucket Replication

이 API를 호출하면 지정 버킷의 지역 간 구성 정보를 획득하게 됩니다. 구체적인 절차는 다음과 같습니다.

1. GetBucketReplicationRequest생성자 함수를 호출하여 GetBucketReplicationRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getBucketReplication(GetBucketReplicationRequest) 동기화 방식을 호출해 GetBucketReplicationRequest를 전달하고 GetBucketReplicationResult 객체를 반환합니다(또는 getBucketReplicationAsync 방식을 호출하고 GetBucketReplicationRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
GetBucketReplicationResult getBucketReplication(GetBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;

void getBucketReplicationAsync(GetBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

GetBucketReplicationResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름             | 변수 설명                              | 유형                     |
| ------------------------ | ------------------------------------- | ------------------------ |
| replicationConfiguration | 지역 간 구성 정보                        | ReplicationConfiguration |
| httpCode                 | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int                      |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
GetBucketReplicationRequest getBucketReplicationRequest = new GetBucketReplicationRequest(bucket);

// 동기화 요청 사용    
try {
    GetBucketReplicationResult getBucketReplicationResult = cosXmlService.getBucketReplication(getBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 요청 사용    
cosXmlService.getBucketReplicationAsync(getBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Bucket Replication success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketReplicationRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다. 


## Delete Bucket Replication

이 API를 호출하면 지정 버킷의 지역 간 구성 정보가 삭제됩니다. 구체적인 절차는 다음과 같습니다.

1. DeleteBucketReplicationRequest 생성자 함수를 호출하여 DeleteBucketReplicationRequest 객체를 인스턴스화합니다.
2. CosXmlService의 deleteBucketReplication(DeleteBucketReplicationRequest) 동기화 방식을 호출해 DeleteBucketReplicationRequest를 전달하고 DeleteBucketReplicationResult 객체를 반환합니다(또는 deleteBucketReplicationAsync 방식을 호출하고 DeleteBucketReplicationRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
DeleteBucketReplicationResult deleteBucketReplication(DeleteBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;

void deleteBucketReplicationAsync(DeleteBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

DeleteBucketReplicationResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
DeleteBucketReplicationRequest deleteBucketReplicationRequest = new DeleteBucketReplicationRequest(bucket);
    
// 동기화 요청 사용
try {
    DeleteBucketReplicationResult result = cosXmlService.deleteBucketReplication(deleteBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 요청 사용
cosXmlService.deleteBucketReplicationAsync(deleteBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Delete Bucket Replication success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket Replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `deleteBucketReplicationRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Put Bucket Lifecycle

이 API는 버킷의 수명 주기 정보 설정에 사용됩니다. 구체적인 절차는 다음과 같습니다.

1. `PutBucketLifecycleRequest(String)` 생성자 함수를 호출하여 PutBucketLifecycleRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putBucketLifecycle 방식을 호출하고 PutBucketLifecycleRequest를 전달해 PutBucketLifecycleResult 객체를 반환합니다.
   (또는 putBucketLifecycleAsync 방식을 호출하고 PutBucketLifecycleRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
PutBucketLifecycleResult putBucketLifecycle(PutBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketLifecycleAsync(PutBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                        | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 bucket 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String                      | 예   |
| rule                      | 수명 주기 구성 규칙                                             | LifecycleConfiguration.Rule | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초입니다                                       | Long                        | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>              | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>              | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener        | 아니요   |

#### 반환 결과 설명

PutBucketLifecycleResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
PutBucketLifecycleRequest putBucketLifecycleRequest = new PutBucketLifecycleRequest(bucket);

// 주기 구성 규칙 정보 선언
LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
rule.id = "Lifecycle ID";
LifecycleConfiguration.Filter filter = new LifecycleConfiguration.Filter();
filter.prefix = "prefix/";
rule.filter = filter;
rule.status = "Enabled or Disabled";
LifecycleConfiguration.Transition transition = new LifecycleConfiguration.Transition();
transition.days = 100;
transition.storageClass = COSStorageClass.STANDARD.getStorageClass();
putBucketLifecycleRequest.setRuleList(rule);

// 동기화 방법 사용
try {
    PutBucketLifecycleResult putBucketLifecycleResult = cosXmlService.putBucketLifecycle(putBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.putBucketLifecycleAsync(putBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket Lifecycle success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putBucketLifecycleRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Get Bucket Lifecycle

이 API는 버킷의 수명 주기 정보 획득에 사용됩니다. 구체적인 절차는 다음과 같습니다.

1. **GetBucketLifecycleRequest(String)** 생성자 함수를 호출하여 GetBucketLifecycleRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getBucketLifecycle 방식을 호출하고 GetBucketLifecycleRequest를 전달해 GetBucketLifecycleResult 객체를 반환합니다.
   (또는 getBucketLifecycleAsync 방식을 호출하고 GetBucketLifecycleRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
GetBucketLifecycleResult getBucketLifecycle(GetBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLifecycleAsync(GetBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

getBucketLifecycle 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름           | 변수 설명                              | 유형                   |
| ---------------------- | ------------------------------------- | ---------------------- |
| lifecycleConfiguration | 수명 주기 구성 정보                      | LifecycleConfiguration |
| httpCode               | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int                    |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
GetBucketLifecycleRequest getBucketLifecycleRequest = new GetBucketLifecycleRequest(bucket);

// 동기화 방법 사용
try {
    GetBucketLifecycleResult getBucketLifecycleResult = cosXmlService.getBucketLifecycle(getBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.getBucketLifecycleAsync(getBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket Lifecycle success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketLifecycleRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Delete Bucket Lifecycle

이 API는 버킷의 수명 주기 정보 삭제에 사용됩니다. 구체적인 절차는 다음과 같습니다.

1. **DeleteBucketLifecycleRequest(String)** 생성자 함수를 호출하여 DeleteBucketLifecycleRequest 객체를 인스턴스화합니다.
2. CosXmlService의 deleteBucketLifecycle 방식을 호출하고 DeleteBucketLifecycleRequest를 전달해 DeleteBucketLifecycleResult 객체를 반환합니다.
   (또는 deleteBucketLifecycleAsync 방식을 호출하고 DeleteBucketLifecycleRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
DeleteBucketLifecycleResult deleteBucketLifecycle(DeleteBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketLifecycleAsync(DeleteBucketLifecycleRequest request,CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

DeleteBucketLifecycleResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
DeleteBucketLifecycleRequest deleteBucketLifecycleRequest = new DeleteBucketLifecycleRequest(bucket);

//동기화 방법 사용
try {
    DeleteBucketLifecycleResult deleteBucketCORSResult = cosXmlService.deleteBucketLifecycle(deleteBucketLifecycleRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.deleteBucketLifecycleAsync(deleteBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket Lifecycle success
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `deleteBucketLifecycleRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## List Multipart Uploads

이 API는 버킷에서 진행 중인 멀티파트 업로드 획득에 사용됩니다. 1회 요청 작업은 최대 1000개의 진행 중인 멀티파트 업로드를 열거할 수 있습니다. 구체적인 절차는 다음과 같습니다.

1. **ListMultiUploadsRequest(String)** 생성자 함수를 호출하여 ListMultiUploadsRequest 객체를 인스턴스화합니다.
2. CosXmlService의 listMultiUploads 방식을 호출하고 ListMultiUploadsRequest를 전달해 ListMultiUploadsResult 객체를 반환합니다.
   (또는 listMultiUploadsAsync 방식을 호출하고 ListMultiUploadsRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
ListMultiUploadsResult listMultiUploads(ListMultiUploadsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listMultiUploadsAsync(ListMultiUploadsRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

ListMultiUploadsResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름         | 변수 설명                              | 유형                 |
| -------------------- | ------------------------------------- | -------------------- |
| listMultipartUploads | 모든 멀티파트 업로드의 정보                    | ListMultipartUploads |
| httpCode             | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int                  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";   
ListMultiUploadsRequest listMultiUploadsRequest = new ListMultiUploadsRequest(bucket);

// 동기화 방법 사용
try {
    ListMultiUploadsResult listMultiUploadsResult = cosXmlService.listMultiUploads(listMultiUploadsRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 방법 사용
cosXmlService.listMultiUploadsAsync(listMultiUploadsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo List Multi Uploads success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo List Multi Uploads failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `listMultiUploadsRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Object API 설명

## Put Object

로컬 파일을 COS에 업로드합니다. 이미지 유형의 작은 파일(20M 이하) 업로드에 적용되며 최대 5GB(5GB 포함)까지 지원하며, 5GB 이상은 반드시 [COSXMLUploadTask 업로드](#upload_task) 또는 멀티파트 업로드를 사용해야 합니다. COS에 이미 객체가 존재하면 덮어쓰기됩니다. 간편 업로드 API는 업로드 일시 정지와 다시 시작을 할 수 없으며, 업로드 과정 중 이상 상황이 발생하여 실패하면 다시 업로드해야 합니다.
구체적인 절차는 다음과 같습니다.

1. `(String, String, String)` 생성자 함수를 호출하여 PutObjectRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putObject 방식을 호출하고 PutObjectRequest를 전달해 PutObjectResult 객체를 반환합니다.
   (또는 putObjectAsync 방식을 호출하고 PutObjectRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
PutObjectResult putObject(PutObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectAsync(PutObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                   | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 bucket 형식은  `<BucketName-APPID>`, 예: examplebucket-1250000000) | String                 | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS에 저장되는 파일의 절대 경로입니다. | String                 | 예   |
| srcPath                   | 로컬 파일의 절대 경로                                           | String                 | 예   ||
| signDuration              | 서명의 유효 기간으. 단위는 초입니다                                       | Long                   | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>         | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>         | 아니요   |
| qCloudProgressListener    | 업로드 진행률 콜백                                                 | CosXmlProgressListener | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener   | 아니요   |

#### 반환 결과 설명

PutObjectResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형   |
| ------------ | ------------------------------------- | ------ |
| accessUrl    | 요청 성공 시, 파일의 접근 주소를 반환합니다        | String |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int    |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = “버킷 이름”  // COS XML API의 bucket 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000
String cosPath = "객체 키”  //COS에 저장되는 파일의 절대 경로"  //형식 예: cosPath = "test.txt";
String srcPath = "로컬 파일의 절대 경로". // 예: srcPath = Environment.getExternalStorageDirectory().getPath() + "/test.txt".

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath).

putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

// 동기화 방법을 사용하여 업로드
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백을 사용하여 업로드
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener( ) {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Put object success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put object failed because of CosXmlClientException or CosXmlServiceException...
    }
});


//바이트 배열 업로드
String bucket = “버킷 이름”  // COS XML API의 bucket 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000
String cosPath = "객체 키”  //COS에 저장되는 파일의 절대 경로"  //형식 예: cosPath = "test.txt";
byte[] data = "this is a test".getBytes(Charset.forName("UTF-8"));
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}


//바이트 스트림 업로드
String bucket = “버킷 이름”  // COS XML API의 bucket 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000
String cosPath = "객체 키”  //COS에 저장되는 파일의 절대 경로"  //형식 예: cosPath = "test.txt";
InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, inputStream);
putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putObjectRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## 멀티파트 업로드

### <span id = "InitMultipartUploadRequest">Initiate Multipart Upload</span>

이 API를 호출하면 멀티파트 업로드를 초기화할 수 있습니다. 이 요청을 성공적으로 실행하면 후속 Upload Part 요청에 사용되는 UploadId를 반환하게 됩니다. 구체적인 절차는 다음과 같습니다.

1. **InitMultipartUploadRequest(String, String)**생성자 함수를 호출하여 InitMultipartUploadRequest 객체를 인스턴스화합니다.
2. CosXmlService의 initMultipartUpload 방식을 호출하고 InitMultipartUploadRequest를 전달해 InitMultipartUploadResult 객체를 반환합니다.
   (또는 initMultipartUploadAsync 방식을 호출하고 InitMultipartUploadRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
InitMultipartUploadResult initMultipartUpload(InitMultipartUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void initMultipartUploadAsync(InitMultipartUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS로 저장되는 파일의 절대 경로입니다. | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

InitMultipartUploadResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름        | 변수 설명                                                     | 유형                |
| ------------------- | ------------------------------------------------------------ | ------------------- |
| initMultipartUpload | [성공한 요청의 반환 결과](https://cloud.tencent.com/document/product/436/7746) | InitMultipartUpload |
| httpCode            | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패                        | Int                 |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";

InitMultipartUploadRequest initMultipartUploadRequest = new InitMultipartUploadRequest(bucket, cosPath);

// 동기화 방법으로 요청
try {
    InitMultipartUploadResult initMultipartUploadResult = cosXmlService.initMultipartUpload(initMultipartUploadRequest);
    String uploadId =initMultipartUploadResult.initMultipartUpload.uploadId;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 방법으로 요청
cosXmlService.initMultipartUploadAsync(initMultipartUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        String uploadId = ((InitMultipartUploadResult)cosXmlResult).initMultipartUpload.uploadId;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Init Multipart Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `initMultipartUploadRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


### Upload Part

이 API를 호출하면 멀티파트 업로드를 구현할 수 있습니다. 지원하는 파트 수는 1부터 10000까지이며 크기는 1MB부터 5GB까지입니다. 구체적인 절차는 다음과 같습니다.

1. **UploadPartRequest(String, String, int, String, String)** 생성자 함수를 호출하여 UploadPartRequest 객체를 인스턴스화합니다.
2. CosXmlService의 uploadPart 방식을 호출하고 UploadPartRequest를 전달해 UploadPartResult 객체를 반환합니다.
   (또는 uploadPartAsync 방식을 호출하고 UploadPartRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
UploadPartResult uploadPart(UploadPartRequest request) throws CosXmlClientException, CosXmlServiceException;

void uploadPartAsync(UploadPartRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                   | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 bucket 형식은  `<BucketName-APPID>`, 예: examplebucket-1250000000) | String                 | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS에 저장되는 파일의 절대 경로입니다. | String                 | 예   |
| uploadId                  | 멀티파트 업로드 초기화 시 반환한 uploadId                              | String                 | 예   |
| partNumber                | 파트의 번호, 1부터 시작합니다.                                    | Int                    | 예   |
| srcPath                   | 로컬 파일의 절대 경로                                           | String                 | 예   |
| fileOffset                | 해당 파트는 파일의 시작 위치                                     | Long                   | 아니요   |
| contentLength             | 해당 파트의 내용 크기                                             | Long                   | 아니요   |
| signDuration              | 서명의 유효 기간. 단위는 초입니다                                       | Long                   | 아니요   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>         | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>         | 아니요   |
| qCloudProgressListener    | 업로드 진행률 콜백                                                 | CosXmlProgressListener | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener   | 아니요   |

#### 반환 결과 설명

UploadPartResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 유형                                              | 변수 설명 |
| ------------ | ------------------------------------------------- | -------- |
| eTag         | 요청 성공, 멀티파트 파일의 MD5 값을 반환하며 마지막 파트 완성에 사용됩니다 | String   |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패             | Int      |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "멀티파트 초기화 시 반환한 uploadId";
int partNumber = 1;//이번에 업로드한 멀티파트 번호로 1부터 시작합니다.
String srcPath = "로컬 파일의 절대 경로";

UploadPartRequest uploadPartRequest = new UploadPartRequest(bucket, cosPath, partNumber, srcPath, uploadId);

uploadPartRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        float result = (float) (progress * 100.0/max);
        Log.w("TEST","progress =" + (long)result + "%");
    }
});

//동기화 방법을 사용하여 업로드
try {
    UploadPartResult uploadPartResult = cosXmlService.uploadPart(uploadPartRequest);
    String eTag = uploadPartResult.eTag; // 멀티파트 파일의 eTag 획득
    
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

    
// 비동기 콜백으로 요청 콜백
cosXmlService.uploadPartAsync(uploadPartRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        String eTag =((UploadPartResult)cosXmlResult).eTag;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Upload Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `uploadPartRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


### <span id = "CompleteMultiUploadRequest">Complete Multipart Upload</span>

모든 멀티파트 업로드 후에는 이 API를 호출하여 전체 멀티파트 업로드를 구현하는 데 사용해야 합니다. 구체적인 절차는 다음과 같습니다.

1. **CompleteMultiUploadRequest(String, String, String, Map<Integer, String>)** 생성자 함수를 호출하여 CompleteMultiUploadRequest 객체를 인스턴스화합니다.
2. CosXmlService의 completeMultiUpload 방식을 호출하고 CompleteMultiUploadRequest를 전달해 CompleteMultiUploadResult 객체를 반환합니다.
   (또는 completeMultiUploadAsync 방식을 호출하고 CompleteMultiUploadRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
CompleteMultiUploadResult completeMultiUpload(CompleteMultiUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void completeMultiUploadAsync(CompleteMultiUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                   | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 bucket 형식은  `<BucketName-APPID>`, 예: examplebucket-1250000000) | String                 | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS에 저장되는 파일의 절대 경로입니다. | String                 | 예   |
| uploadId                  | 멀티파트 업로드 초기화 시 반환한 uploadId                              | String                 | 예   |
| partNumberAndETag         | 멀티파트 번호와 해당 멀티파트 MD5 값                                 | Map&lt;Integer,String> | 예   |
| signDuration              | 서명의 유효 기간으. 단위는 초입니다                                       | Long                   | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>         | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>         | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener   | 아니요   |

#### 반환 결과 설명

CompleteMultiUploadResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름            | 변수 설명                                                     | 유형                    |
| ----------------------- | ------------------------------------------------------------ | ----------------------- |
| completeMultipartUpload | [성공한 요청의 반환 결과](https://cloud.tencent.com/document/product/436/7742) | CompleteMultipartResult |
| accessUrl               | 요청 성공 시, 접근 파일의 주소를 반환합니다                               | String                  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "멀티파트 초기화 시 반환한 uploadId";
int partNumber = 1;
String etag = "번호는 partNumber로 멀티파트 업로드 종료 후 반환한 etag와 대응합니다 ";
Map<Integer, String> partNumberAndETag = new HashMap<>();
partNumberAndETag.put(partNumber, etag);

CompleteMultiUploadRequest completeMultiUploadRequest = new CompleteMultiUploadRequest(bucket, cosPath, uploadId, partNumberAndETag);

// 동기화 방법으로 요청
try {
    CompleteMultiUploadResult completeMultiUploadResult = cosXmlService.completeMultiUpload(completeMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.completeMultiUploadAsync(completeMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Complete Multi Upload success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Complete Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `completeMultiUploadRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


### List Parts

이 API는 특정 멀티파트 업로드 중 이미 업로드한 멀티파트를 조회하는 데 사용됩니다. 즉, 지정 UploadId가 속한 모든 성공적으로 업로드한 멀티파트를 나열합니다.

1. **ListPartsRequest(String, String, String)** 생성자 함수를 호출하여 ListPartsRequest 객체를 인스턴스화합니다.
2. CosXmlService의 listParts 방식을 호출하고 ListPartsRequest를 전달해 ListPartsResult 객체를 반환합니다.
   (또는 listPartsAsync 방식을 호출하고 ListPartsRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
ListPartsResult listParts(ListPartsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listPartsAsync(ListPartsRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS로 저장되는 파일의 절대 경로입니다. | String               | 예   |
| uploadId                  | 멀티파트 업로드 초기화 시 반환한 uploadId                              | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

ListPartsResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                                                     | 유형      |
| ------------ | ------------------------------------------------------------ | --------- |
| listParts    | [성공한 요청의 반환 결과](https://cloud.tencent.com/document/product/436/7747) | ListParts |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패                        | Int       |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "멀티파트 초기화 시 반환한 uploadId";

ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, cosPath, uploadId);

// 동기화 방법으로 요청
try {
    ListPartsResult listPartsResult = cosXmlService.listParts(listPartsRequest);
    ListParts listParts = listPartsResult.listParts;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백 
cosXmlService.listPartsAsync(listPartsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        ListParts listParts = ((ListPartsResult)cosXmlResult).listParts;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo List Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `listPartsRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


### Abort Multipart Upload

이 API는 하나의 멀티파트 업로드를 중단하고 이미 업로드된 파트를 삭제하는 데 사용됩니다.

1. **AbortMultiUploadRequest(String, String, String)** 생성자 함수를 호출하여 AbortMultiUploadRequest 객체를 인스턴스화합니다.
2. CosXmlService의 abortMultiUpload 방식을 호출하고 AbortMultiUploadRequest를 전달해 AbortMultiUploadResult 객체를 반환합니다.
   (또는 abortMultiUploadAsync 방식을 호출하고 AbortMultiUploadRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
AbortMultiUploadResult abortMultiUpload(AbortMultiUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void abortMultiUploadAsync(AbortMultiUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름 (COS XML API의 bucket 형식은  `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS로 저장되는 파일의 절대 경로입니다. | String               | 예   |
| uploadId                  | 멀티파트 업로드 초기화 시 반환한 uploadId                              | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

AbortMultiUploadResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 본문의 [SDK 이상 설명](#sdk_exception)을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "멀티파트 초기화 시 반환한 uploadId";

AbortMultiUploadRequest abortMultiUploadRequest = new AbortMultiUploadRequest(bucket, cosPath, uploadId);

// 동기화 방법으로 요청
try {
    AbortMultiUploadResult abortMultiUploadResult = cosXmlService.abortMultiUpload(abortMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 콜백으로 요청 콜백
cosXmlService.abortMultiUploadAsync(abortMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Abort Multi Upload success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Abort Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `abortMultiUploadRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## 파일 삭제

### Delete Object

이 API를 호출하면 지정한 버킷에서 파일 1개를 삭제할 수 있습니다. 구체적인 절차는 다음과 같습니다.

1. **DeleteObjectRequest(String, String)** 생성자 함수를 호출하여 DeleteObjectRequest 객체를 인스턴스화합니다.
2. CosXmlService의 completeMultiUpload 방식을 호출하고 DeleteObjectRequest를 전달해 DeleteObjectResult 객체를 반환합니다.
   (또는 deleteObjectAsync 방식을 호출하고 DeleteObjectRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
DeleteObjectResult deleteObject(DeleteObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteObjectAsync(DeleteObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS로 저장되는 파일의 절대 경로입니다. | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

DeleteObjectResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, cosPath);

// 동기화 방법을 사용하여 삭제
try {
    DeleteObjectResult deleteObjectResult = cosXmlService.deleteObject(deleteObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백 
cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Delete Object success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `deleteObjectRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


### Delete Multi Objects

이 API를 호출하면 지정 버킷에서 파일을 배치 삭제할 수 있습니다. 요청은 1회 최대 1000개 파일을 배치 삭제할 수 있습니다. 구체적인 절차는 다음과 같습니다.

1. DeleteMultiObjectRequest(String, List&lt;String>) 생성자 함수를 호출하여 DeleteMultiObjectRequest 객체를 인스턴스화합니다.
2. CosXmlService의 deleteMultiObject 방식을 호출하고 DeleteMultiObjectRequest를 전달해 DeleteMultiObjectResult 객체를 반환합니다.
   (또는 deleteMultiObjectAsync 방식을 호출하고 DeleteMultiObjectRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
DeleteMultiObjectResult deleteMultiObject(DeleteMultiObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteMultiObjectAsync(DeleteMultiObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| quiet                     | true: 삭제 오류 파일 정보만 반환합니다. false: 모든 파일의 삭제 결과를 반환합니다 | Boolean              | 예   |
| objectList                | 삭제해야 할 [객체 키](https://cloud.tencent.com/document/product/436/13324) 리스트 | List&lt;String>      | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

DeleteMultiObjectResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
List<String> objectList = new ArrayList<String>();
objectList.add("/2/test.txt");

DeleteMultiObjectRequest deleteMultiObjectRequest = new DeleteMultiObjectRequest(bucket, objectList);
deleteMultiObjectRequest.setQuiet(true);

// 동기화 방법을 사용하여 삭제
try {
    DeleteMultiObjectResult deleteMultiObjectResult =cosXmlService.deleteMultiObject(deleteMultiObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.deleteMultiObjectAsync(deleteMultiObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // Delete Multi Object success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        //  Delete Multi Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `deleteMultiObjectRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다. 


## Get Object

이 API를 호출하면 지정 버킷의 파일 1개가 로컬에 다운로드됩니다. 구체적인 절차는 다음과 같습니다.

1. **GetObjectRequest(String, String, String)** 생성자 함수를 호출하여 GetObjectRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getObject 방식을 호출하고 GetObjectRequest를 전달해 GetObjectResult 객체를 반환합니다.
   (또는 getObjectAsync 방식을 호출하고 GetObjectRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
GetObjectResult getObject(GetObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectAsync(GetObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                   | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 bucket 형식은  `<BucketName-APPID>`, 예: examplebucket-1250000000) | String                 | 예   |
| cosPath                   | [객체 키](https://cloud.tencent.com/document/product/436/13324), COS에 저장되는 파일의 절대 경로입니다. | String                 | 예   |
| savaPath                  | 로컬 폴더에 다운로드된 파일의 절대 경로                               | String                 | 예   |
| start                     | 요청 파일의 시작 위치                                           | Long                   | 아니요   |
| end                       | 요청 파일의 종료 위치                                           | Long                   | 아니요   |
| signDuration              | 서명의 유효 기간으. 단위는 초입니다                                       | Long                   | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>         | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>         | 아니요   |
| qCloudProgressListener    | 다운로드 진행률 콜백                                                 | CosXmlProgressListener | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener   | 아니요   |

#### 반환 결과 설명

GetObjectResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
String savePath = "savePath";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePath);
getObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

//동기화 방법을 사용하여 다운로드
try {
    GetObjectResult getObjectResult =cosXmlService.getObject(getObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.getObjectAsync(getObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Object success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getObjectRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다. 


## 객체 복사

### Copy Object

이 API를 호출하면 파일 1개를 리소스 경로에서 대상 경로로 복사합니다. 권장 파일 크기는 1M부터 5G까지입니다. 5G를 초과하는 파일은 멀티파트 업로드 Upload - Copy를 사용하길 권장합니다. 구체적인 절차는 다음과 같습니다.

1. **CopyObjectRequest(String, String, CopySourceStruct)** 생성자 함수를 호출하여 CopyObjectRequest 객체를 인스턴스화합니다.
2. CosXmlService의 copyObject 방식을 호출하고 CopyObjectRequest를 전달해 CopyObjectResult 객체를 반환합니다.
   (또는 copyObjectAsync 방식을 호출하고 CopyObjectRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
CopyObjectResult copyObject(CopyObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(CopyObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | 대상 [객체 키](https://cloud.tencent.com/document/product/436/13324), COS로 저장되는 파일의 절대 경로입니다. | String               | 예   |
| copySourceStruct          | 소스 경로 구조                                                 | CopySourceStruct     | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

CopyObjectResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형       |
| ------------ | ------------------------------------- | ---------- |
| copyObject   | 복사 결과 정보 반환                      | CopyObject |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int        |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct("소스 파일의 appid",
        "소스 파일의 bucket", "소스 파일의 region", "소스 파일의 cosPath");

CopyObjectRequest copyObjectRequest = null;
try {
    copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}

// 동기화 방법 사용
try {
    CopyObjectResult copyObjectResult = cosXmlService.copyObject(copyObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Copy Object success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `copyObjectRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다. 


### 멀티파트 복사

구체적인 절차는 다음과 같습니다.

1. cosXmlService.initMultipartUpload(InitMultipartUploadRequest)를 호출하여 멀티파트를 초기화합니다. [InitMultipartUploadRequest 멀티파트 초기화](#InitMultipartUploadRequest)를 참조하십시오.
2. cosXmlService.copyObject(UploadPartCopyRequest)를 호출하여 멀티파트 복사를 완료합니다.
3. cosXmlService.completeMultiUpload(CompleteMultiUploadRequest)를 호출하여 멀티파트 복사를 완료합니다. [CompleteMultiUploadRequest 멀티파트 복사 완료](#CompleteMultiUploadRequest)를 참조하십시오.

### UploadPartCopyRequest 설명

```java
UploadPartCopyResult copyObject(UploadPartCopyRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(UploadPartCopyRequest request,final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                   | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 bucket 형식은  `<BucketName-APPID>`, 예: examplebucket-1250000000) | String                 | 예   |
| cosPath                   | 객체 키, COS로 저장되는 파일의 절대 경로                            | String                 | 예   |
| uploadId                  | 멀티파트 업로드 초기화 시 반환한 uploadId                              | String                 | 예   |
| partNumber                | 멀티파트의 번호, 1부터 시작합니다                                      | Int                    | 예   |
| copySourceStruct          | 소스 경로 구조                                                 | CopySourceStruct       | 예   |
| start                     | 해당 멀티파트의 소스 파일 내의 시작 위치                                   | Long                   | 아니요   |
| end                       | 해당 멀티파트의 소스 파일 내의 종료 위치                                   | Long                   | 아니요   |
| signDuration              | 서명의 유효 기간. 단위는 초입니다                                       | Long                   | 아니요   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set<String>            | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set<String>            | 아니요   |
| qCloudProgressListener    | 업로드 진행률 콜백                                                 | CosXmlProgressListener | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener   | 아니요   |

#### 반환 결과 설명

CopyObjectResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형       |
| ------------ | ------------------------------------- | ---------- |
| copyObject   | 복사 결과 정보 반환                      | CopyObject |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int        |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct("소스 파일의 appid",
        "소스 파일의 bucket", "소스 파일의 region", "소스 파일의 cosPath");
String uploadId = "멀티파트의 uploadId 초기화";
int partNumber = 1; //멀티파트 번호
long start = 0;//소스 파일의 시작 위치 복사
long end = 100; //소스 파일의 종료 위치 복사
UploadPartCopyRequest uploadPartCopyRequest = null;
try {
    uploadPartCopyRequest = new UploadPartCopyRequest(bucket, cosPath, partNumber,  uploadId, copySourceStruct， start, end);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}

// 동기화 방법 사용
try {
    UploadPartCopyResult uploadPartCopyResult = cosXmlService.copyObject(uploadPartCopyRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.copyObjectAsync(uploadPartCopyRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Copy Object success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `uploadPartCopyRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다. 


## Head Object

이 API를 호출하면 지정 버킷 중 객체 존재 여부를 확인합니다. 구체적인 절차는 다음과 같습니다.

1. HeadObjectRequest(String, string) 생성자 함수를 호출하여 HeadObjectRequest 객체를 인스턴스화합니다.
2. CosXmlService의 headObject 방식을 호출하고 HeadObjectRequest를 전달해 HeadObjectResult 객체를 반환합니다.
   (또는 headObjectAsync 방식을 호출하고 HeadObjectRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
HeadObjectResult headObject(HeadObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void headObjectAsync(HeadObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | 객체 키, COS로 저장되는 파일의 절대 경로                            | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

HeadObjectResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath"
HeadObjectRequest headObjectRequest = new HeadObjectRequest(bucket, cosPath);

//동기화 방법 사용
try {
    HeadObjectResult headObjectResult = cosXmlService.headObject(headObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 비동기 콜백으로 요청 콜백
cosXmlService.headObjectAsync(headObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Head Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `headObjectRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다. 


## Put Object ACL

이 API를 호출하면 버킷 중 객체의 접근 제어 권한을 지정할 수 있습니다. 구체적인 절차는 다음과 같습니다.

1. **PutObjectACLRequest(String, string)** 생성자 함수를 호출하여 PutObjectACLRequest 객체를 인스턴스화합니다.
2. CosXmlService의 putObjectACL 방식을 호출하고 PutObjectACLRequest를 전달해 PutObjectACLResult 객체를 반환합니다.
   (또는 putObjectACLAsync 방식을 호출하고 PutObjectACLRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
PutObjectACLResult putObjectACL(PutObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectACLAsync(PutObjectACLRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | 객체 키, COS로 저장되는 파일의 절대 경로                            | String               | 예   |
| xcosACL                   | 버킷 접근 권한을 설정합니다. 유효값: private, public-read-write, public-read. 기본값: private | String               | 아니요   |
| xcosGrantRead             | 권한 부여받은 자에게 읽기 권한 부여                                         | ACLAccount           | 아니요   |
| xcosGrantWrite            | 권한 부여받은 자에게 기 권한 부여                                         | ACLAccount           | 아니요   |
| xcosGrantRead             | 권한 부여받은 자에게 읽기/쓰기 권한 부여                                       | ACLAccount           | 아니요   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

PutObjectACLResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름 | 변수 설명                              | 유형 |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패 | Int  |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
PutObjectACLRequest putObjectACLRequest = new PutObjectACLRequest(bucket, cosPath);

//버킷 접근 권한 설정
putObjectACLRequest.setXCOSACL("public-read");

//권한 부여받은 자에게 읽기 권한 부여
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putObjectACLRequest.setXCOSGrantRead(readACLS);

//권한 부여받은 자에게 쓰기 권한 부여
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putObjectACLRequest.setXCOSGrantRead(writeACLS);

//권한 부여받은 자에게 읽기/쓰기 권한 부여
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putObjectACLRequest.setXCOSGrantRead(writeandReadACLS);

// 동기화 방법 사용
try {
    PutObjectACLResult putObjectACLResult = cosXmlService.putObjectACL(putObjectACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 콜백으로 요청 콜백
cosXmlService.putObjectACLAsync(putObjectACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `putObjectACLRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## Get Object ACL

이 API는 버킷 중 지정 객체의 ACL을 획득하는 데 사용됩니다. 구체적인 절차는 다음과 같습니다.

1. **GetObjectACLRequest(String, string)** 생성자 함수를 호출하여 GetObjectACLRequest 객체를 인스턴스화합니다.
2. CosXmlService의 getObjectACL 방식을 호출하고 GetObjectACLRequest를 전달해 GetObjectACLResult 객체를 반환합니다.
   (또는 getObjectACLAsync 방식을 호출하고 GetObjectACLRequest와 CosXmlResultListener를 전달해 비동기 콜백 작업을 진행합니다).

```java
GetObjectACLResult getObjectACL(GetObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectACLAsync(GetObjectACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | 버킷 이름(COS XML API의 버킷 형식은 `<BucketName-APPID>`, 예: examplebucket-1250000000) | String               | 예   |
| cosPath                   | 객체 키, COS로 저장되는 파일의 절대 경로                            | String               | 예   |
| signDuration              | 서명의 유효 기간. 단위는 초                                       | Long                 | 예   |
| checkHeaderListForSign    | 서명에서 인증해야 할 요청 헤더                                       | Set&lt;String>       | 아니요   |
| checkParameterListForSing | 서명에서 인증해야 할 요청 매개변수                                     | Set&lt;String>       | 아니요   |
| cosXmlResultListener      | 업로드 결과 콜백                                                 | CosXmlResultListener | 아니요   |

#### 반환 결과 설명

GetObjectACLResult 객체의 멤버 변수를 통해 요청 결과를 반환합니다.

| 멤버 변수 이름        | 변수 설명                                                     | 유형                |
| ------------------- | ------------------------------------------------------------ | ------------------- |
| accessControlPolicy | [권한 부여받은 자 정보와 권한 정보](https://cloud.tencent.com/document/product/436/7733) | AccessControlPolicy |
| httpCode            | [200, 300) 사이라면 요청 성공, 그렇지 않으면 요청 실패                        | Int                 |

> ?이상 CosClientException 또는 CosServiceException을 throw할 경우, 구체적인 내용은 매개변수 본문 [SDK 이상 정보 설명](#sdk_exception) 장을 참조하십시오.

#### 예시

```java
String bucket = "bucket";
String cosPath = "cosPath";
GetObjectACLRequest getBucketACLRequest = new GetObjectACLRequest(bucket, cosPath);

// 동기화 방법 사용
try {
    GetObjectACLResult getObjectACLResult = cosXmlService.getObjectACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 비동기 콜백으로 요청 콜백
cosXmlService.getObjectACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?요청 시, 이미 계산한 서명 문자열을 바로 설정해야 하려면 `getBucketACLRequest.setSign(‘이미 계산한 서명 문자열’)`을 호출하여 설정할 수 있습니다. 기본으로 sdk에서 서명 문자열을 계산합니다.


## 고급 API 설명

## <span id = "upload_task">고급 API 파일 업로드(추천)</span>

**TransferManager**, **COSXMLUploadTask**는 간편 업로드, 멀티파트 업로드 API의 비동기 요청을 캡슐화하였으며, 업로드 요청 일시 정지, 복구 및 취소를 지원함과 동시에 전송 재개 기능을 지원합니다. 이러한 방식을 사용하여 파일을 업로드하길 추천합니다. 예제 코드는 다음과 같습니다.

```java
// TransferConfig 초기화
TransferConfig transferConfig = new TransferConfig.Builder().build();

/*특별 요구 사항이 있을 경우, 다음과 같이 초기화를 사용자 지정할 수 있습니다. 예를 들어, 해당 파일이 >= 2M일 때, 멀티파트 업로드를 사용하며 파트 크기는 1M이며, 소스 파일이 5M보다 클 때 멀티파트 복사를 사용하며, 파트의 크기는 5M임을 설정할 수 있습니다.*/
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // 멀티파트 복사 사용 여부를 판단하기 위한 파일 최소 크기
        .setSliceSizeForCopy(5 * 1024 * 1024) //멀티파트 복사 시 파트 크기
        .setDivisionForUpload(2 * 1024 * 1024) // 멀티파트 업로드 사용 여부를 판단하기 위한 파일 최소 크기
        .setSliceSizeForCopy(1024 * 1024) //멀티파트 업로드 시 파트 크기
        .build();


//TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "버킷 이름";
String cosPath = "객체 키"; //COS로 저장되는 파일의 절대 경로". //형식 예: cosPath = "test.txt".
String srcPath = "로컬 파일의 절대 경로"; // 예: srcPath=Environment.getExternalStorageDirectory().getPath() + "/test.txt".
String uploadId = null; //멀티파트 업로드를 초기화한 UploadId가 존재할 경우, 해당 uploadId 값을 배정하여 전송을 재개하고, 그렇지 않을 경우 null을 배정합니다.
//파일 업로드
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
* 바이트 배열을 업로드할 경우, TransferManager의 upload(string, string, byte[]) 방법을 호출하여 구현할 수 있습니다.
* byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
*/

/**
* 바이트 스트림을 업로드할 경우, TransferManager의 upload(String, String, InputStream) 방법을 호출하여 구현할 수 있습니다.
* InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
*/

//업로드 진행률 콜백 설정
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//반환 결과 콜백 설정
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//태스크 상태 콜백 설정, 태스크 과정을 조회할 수 있습니다.
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
특별 요구 사항이 있을 경우, 다음 작업을 할 수 있습니다.
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); //버킷 소재 지역 설정
 putObjectRequest.setNeedMD5(true); //Md5 검사 사용 여부
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

//업로드 취소
cosxmlUploadTask.cancel();


//업로드 일시 정지
cosxmlUploadTask.pause();

//업로드 복구
cosxmlUploadTask.resume();

```

## <span id = "download_task">고급 API 파일 다운로드(추천)</span>

**TransferManager**, **COSXMLDownloadTask**는 다운로드 API의 비동기 요청을 캡슐화하였으며, 다운로드 요청 일시 정지, 복구 및 취소를 지원함과 동시에 전송 재개 기능을 지원합니다. 예제 코드는 다음과 같습니다.

```java
Context applicationContext = "application 콘텍스트"； //
String bucket = "버킷 이름"; //파일 소재 버킷
String cosPath = "객체 키"; //COS로 저장되는 파일의 절대 경로". //형식은 cosPath = "test.txt"와 같습니다.
String savedDirPath = "로컬로 다운로드된 파일의 폴더 경로"；
String savedFileName = "로컬로 다운로드된 파일의 파일 이름"；//입력하지 않을 경우(null), cos의 파일 이름과 같습니다.
//파일 다운로드
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savedDirPath, savedFileName);
//다운로드 진행률 콜백 설정
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//반환 결과 콜백 설정
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//태스크 상태 콜백 설정, 태스크 과정을 조회할 수 있습니다.
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
특별 요구 사항이 있을 경우, 다음 작업을 할 수 있습니다.
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
getObjectRequest.setRegion(region); //버킷 소재 지역 설정
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
*/

//다운로드 취소
cosxmlDownloadTask.cancel();

//다운로드 일시 정지
cosxmlDownloadTask.pause();

//다운로드 복구
cosxmlDownloadTask.resume();

```

## <span id = "copy_task">고급 API 파일 복사(추천)</span>

**TransferManager**, **COSXMLCopyTask**는 간편 복사, 멀티파트 복사 API의 비동기 요청을 캡슐화하였으며, 복사 요청 일시 정지, 복구 및 취소를 지원합니다. 예제 코드는 다음과 같습니다.

```java
String bucket = "버킷 이름"; //대상 파일의 버킷
String cosPath = "객체 키"; //COS로 저장되는 대상 파일의 절대 경로". //형식은 cosPath = "test.txt"와 같습니다.
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(
                "소스 파일 버킷 소재의 appid", "소스 파일 버킷", "소스 파일 버킷 소재의 지역", "소스 파일의 객체 키");// 소스 파일 소재 cos의 위치 설명
//파일 복사
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath, copySourceStruct);
//반환 결과 콜백 설정
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//태스크 상태 콜백 설정, 태스크 과정을 조회할 수 있습니다.
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });
/**
특별 요구 사항이 있을 경우, 다음 작업을 할 수 있습니다.
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
copyObjectRequest.setRegion(region); //버킷 소재 지역 설정
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(copyObjectRequest);
*/

//복사 취소
cosxmlCopyTask.cancel();


//복사 일시 정지
cosxmlCopyTask.pause();

//복사 복구
cosxmlCopyTask.resume();
```

## 사전 서명 링크 생성

CosXmlService의 getPresignedURL(CosXmlRequest) 방법을 호출하여 해당 요청의 사전 서명 링크를 획득합니다.

String getPresignedURL(CosXmlRequest cosXmlRequest) throws CosXmlClientException

```java
try{
String urlWithSign = cosXml.getPresignedURL(putObjectRequest);
}catch(Exception ex){
Log.d("TEST", ex.getMessage());
}
```

## <span id = "sdk_exception">SDK 이상 정보 설명</span>

SDK에서 API를 호출하여 COS 객체에 대한 작업에 실패하면 CosXmlClientException 이상 또는 CosXmlServiceException 이상을 throw합니다.

### CosXmlClientException

클라이언트 이상. 클라이언트의 원인으로 서버와 상호 작용을 정상적으로 완료할 수 없어 초래된 실패를 가리킵니다. 예를 들어 클라이언트가 서버에 연결할 수 없거나 서버가 반환한 데이터를 해석할 수 없거나 로컬 파일 읽기에 IO 이상이 발생하는 등 현상과 같습니다. CosXmlClientException은 Exception으로부터 통합되며, 사용 방법은 Exception과 동일하고 다음과 같이 별도 멤버 errorCode를 추가합니다.

| 멤버      | 설명                                  | 유형 |
| --------- | ------------------------------------- | ---- |
| errorCode | 클라이언트 오류 코드. 예를 들어 10000은 매개변수 검사 실패를 의미합니다. | int  |

### CosXmlServiceException

CosXmlServiceException 서비스 이상. 상호 작용이 정상 완료되었지만 작업이 실패한 시나리오를 가리킵니다. 예를 들어 클라이언트가 존재하지 않는 버킷에 접근하거나 존재하지 않는 파일을 삭제하거나 어느 작업을 할 권한이 없거나 서버 고장 등과 같습니다. CosXmlServiceException은 서버가 반환한 상태 코드, requestid, 오류 명세 등을 포함합니다. 이상 현상을 캡처한 뒤, 전체 이상 현상을 프린트하길 권장합니다. 이상 현상은 해결이 필요한 요소를 포함합니다. 다음은 이상 멤버 변수에 대한 설명입니다.

| 멤버         | 설명                                                         | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| requestId    | 요청 ID. 요청을 표시하는 데 사용되며 문제 해결에 있어 아주 중요한 부분입니다.            | String |
| statusCode   | 응답의 상태 코드. 4xx란 요청이 클라이언트로 인해 실패하고, 5xx는 서비스 이상으로 인해 실패한 경우를 의미합니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. | String |
| errorCode    | 요청 실패 시 본문이 반환한 오류 코드입니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. | String |
| errorMessage | 요청 실패 시 본문이 반환한 오류 코드입니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. | String |

