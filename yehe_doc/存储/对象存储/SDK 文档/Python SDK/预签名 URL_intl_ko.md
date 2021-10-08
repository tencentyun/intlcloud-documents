## 소개
Python SDK는 서명 획득 및 사전 서명된 URL 요청 획득 인터페이스, 객체 다운로드의 사전 서명된 URL 획득 인터페이스를 제공합니다. 영구 키 또는 임시 키를 사용해 사전 서명된 URL을 획득하는 호출 방법과 동일하며, 임시 키 사용 시에는 header 또는 query_string에 x-cos-security-token을 추가해야 합니다.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 

## 서명 획득

#### 기능 설명
지정 작업의 서명을 획득합니다. 모바일에서의 서명 배포에 주로 사용됩니다.

#### 메소드 프로토타입

```
get_auth(Method, Bucket, Key, Expired=300, Headers={}, Params={})
```

#### 요청 예시 업로드

[//]: # (.cssg-snippet-get-authorization-upload)
```python
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### 요청 예시 다운로드

[//]: # (.cssg-snippet-get-authorization-download)
```python
response = client.get_auth(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### 모든 매개변수 요청 예시

```python
response = client.get_auth(
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=300,
    Headers={
        'Content-Length': 'string',
        'Content-MD5': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    }
)
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 | 
| -------------- | -------------- |---------- | ----------- |
 | Method  |해당 작업의 Method, 옵션값: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'|  String |  예 | 
 | Bucket  |버킷 이름은 BucketName-APPID로 구성 |  String |  예 | 
 | Key  | Bucket 작업에 루트 경로 `/` 입력, object 작업에 파일 경로 입력| String | 예| 
 |Expired| 서명 만료 시간(단위: 초)| Int| 아니요|
 |Headers| 서명을 삽입할 요청 헤더| Dict| 아니요|
 |Params | 서명을 삽입할 요청 매개변수| Dict| 아니요|

#### 반환 결과 설명

해당 방법의 반환값은 해당 작업의 서명 값입니다.

## 사전 서명된 URL 가져오기

#### 기능 설명

사전 서명된 링크를 획득하여 배포에 사용합니다.

#### 요청 예시 업로드

[//]: # (.cssg-snippet-get-presign-upload-url)
```python
response = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### 요청 예시 다운로드

[//]: # (.cssg-snippet-get-presign-download-url)
```python
response = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```


#### 임시 키 요청 예시

[//]: # (.cssg-snippet-get-presign-download-sts-url)
```python
response = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'x-cos-security-token': 'string'
    }
)
```

#### 메소드 프로토타입

```
get_presigned_url(Bucket, Key, Method, Expired=300, Params={}, Headers={})
```

#### 요청 예시

```python
response = client.get_presigned_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD',
    Expired=300,
    Headers={
        'Content-Length': 'string',
        'Content-MD5': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    }
)
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket  |버킷 이름은 BucketName-APPID로 구성 |  String |  예 | 
 |  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String  | 예 | 
 | Method  |해당 작업의 Method, 옵션값: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'|  String |  예 | 
 |Expired| 서명 만료 시간(단위: 초)| Int| 아니요|
 |Params| 서명에 삽입할 요청 매개변수| Dict| 아니요|
 |Headers| 서명에 삽입할 요청 헤더| Dict| 아니요|
 
 
#### 반환 결과 설명

해당 방법의 반환값은 사전 서명된 URL입니다.

## 사전 서명된 다운로드 URL 획득

#### 기능 설명
사전 서명된 다운로드 링크를 획득하여 직접 다운로드에 사용합니다.


#### 임시 키 요청 예시

[//]: # (.cssg-snippet-get-presign-download-sts-url)
```python
response = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'x-cos-security-token': 'string'
    }
)
```


#### 메소드 프로토타입

```
get_presigned_download_url(Bucket, Key, Expired=300, Params={}, Headers={})
```

#### 요청 예시

[//]: # (.cssg-snippet-get-presign-download-url-alias)
```python
response = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=300,
    Headers={
        'Range': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    }
)
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket  |버킷 이름은 BucketName-APPID로 구성 |  String |  예 | 
 |  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String  | 예 | 
 |Expired| 서명 만료 시간(단위: 초)| Int| 아니요|
 |Params| 서명에 삽입할 요청 매개변수| Dict| 아니요|
 |Headers| 서명에 삽입할 요청 헤더| Dict| 아니요|

#### 반환 결과 설명

해당 방법의 반환값은 사전 서명된 다운로드 URL입니다.
