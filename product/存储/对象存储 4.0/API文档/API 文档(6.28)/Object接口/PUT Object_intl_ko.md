## 기능 설명
PUT Object API 요청은 로컬 개체(Object)를 지정 버킷에 업로드할 수 있습니다. 해당 작업은 요청자가 버킷에 대해 쓰기 권한이 있어야 합니다.

### 버전

버킷에 버전 제어를 활성화하면, COS는 추가해야 할 개체에 자동으로 유일한 버전 ID를 생성합니다. COS는 x-cos-version-id 응답 헤더를 사용하여 응답에서 이 ID를 반환합니다.
버킷의 버전 제어를 일시 정지해야 할 경우, COS는 줄곧 해당 null을 버킷에 저장한 개체의 버전 ID로 사용합니다.

### 세부 분석
1. Bucket의 쓰기 권한이 필요합니다.
2. 요청 헤더의 Content-Length 값이 실제 요청 본문에서 전송한 데이터 길이보다 작아도 COS는 성공적으로 파일을 생성합니다. 단, Object 크기는 Content-Length에서 정의한 크기만 하며, 다른 데이터는 폐기됩니다.
3. 추가를 시도한 Object의 같은 이름의 파일이 이미 존재할 경우, 새로 업로드한 파일은 기존 파일을 덮어쓰며 성공 시, 200 OK를 반환합니다.

## 요청
### 요청 예제

```shell
PUT /<ObjectName> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.).

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더
해당 작업은 다음 요청 헤더를 사용하여 구현할 수도 있습니다.

이름|설명|유형|필수 여부
---|---|---|---
Content-Disposition|RFC 2616에서 정의한 파일 이름이며, Object 메타데이터로 저장합니다.|string|아니요
Content-Encoding|RFC 2616에서 정의한 인코딩 형식이며, Object 메타데이터로 저장합니다.|string|아니요
Expect|Expect: 100-continue를 사용할 때, 서버의 확인을 받아야 요청 내용을 발송합니다.|string|아니요
Expires|RFC 2616에서 정의한 캐시 정책이며, Object 메타데이터로 저장합니다.|string|아니요
x-cos-meta-\*|사용자 지정 헤더 접미사와 사용자 지정 헤더 정보를 포함하고, Object 메타데이터 반환으로 사용하며, 크기는 2KB로 제한합니다.<br>**주의: **사용자 지정 헤버 정보는 밑줄을 지원하지만, 사용자 지정 헤더 접미사는 밑줄을 지원하지 않습니다.|string|아니요
x-cos-storage-class|Object의 스토리지 클래스를 설정합니다. 열거값: STANDARD, STANDARD_IA, 기본값: STANDARD|string|아니요
x-cos-acl|Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read, default, 기본값: default(Bucket 권한 승계). 주의: 현재 접근 정책 항목은 1000개로 제한됩니다. Object ACL 제어를 진행할 필요가 없다면, default를 입력하거나 이 항목을 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.|string|아니요
x-cos-grant-read |권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id="[OwnerUin]" | String |  아니요
x-cos-grant-write| 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id="[OwnerUin]" |String |  아니요
x-cos-grant-full-control | 권한을 부여받은 자에게 모든 권한을 부여합니다. 형식: x-cos-grant-full-control: id="[OwnerUin]" | String| 아니요

#### 서버 암호화 관련 헤더

해당 요청 작업은 Tencent Cloud COS가 데이터를 저장할 때, 응용하는 데이터 암호화 보호 정책을 지정합니다. Tencent Cloud COS는 데이터를 데이터 센터에 입력할 때 자동 암호화하고 해당 데이터를 사용할 때 자동 암호화 해제하도록 도와줍니다. 현재는 Tencent Cloud COS 기본 키를 사용하여 데이터에 AES-256 암호화를 지원합니다. 데이터에 대해 서버 암호화를 활성화해야 할 경우, 다음 헤더를 전달해야 합니다.

| 이름        | 설명    | 유형     | 필수 여부     |
| --------- | --------- | ------ | ------ |
| x-cos-server-side-encryption | 개체에 서버 암호화를 활성화하는 방식을 지정합니다. <br/>COS 기본 키를 사용하여 암호화할 때, AES256을 입력합니다. | String | 암호화가 필요할 경우, 예 |

### 요청체
해당 요청의 요청체는 Object 파일 내용입니다.

## 응답
### 응답 헤더

#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.

#### 고유의 응답 헤더

해당 요청 작업의 응답 헤더의 구체적인 데이터는 다음과 같습니다.

|이름|유형|설명|
|---|---|---|
|ETag|string|파일 내용의 MD5값 업로드|
|x-cos-version-id|string|객체 버전 반환|
|x-cos-server-side​-encryption|string|COS 관리 서버 암호화를 통해 개체를 저장한 경우, 응답은 이 헤더와 사용한 암호화 알고리즘 값 AES256을 포함합니다. |

### 응답 본문
해당 요청 응답 본문은 비어 있습니다.

### 오류 코드
해당 요청 작업은 특별한 오류 정보가 없습니다. 흔히 볼 수 있는 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례

### 요청

```shell
PUT /picture.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2015 20:32:00 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484639384;32557535384&q-key-time=1484639384;32557535384&q-header-list=host&q-url-param-list=&q-signature=5c07b7c67d56497d9aacb1adc19963135b7d00dc
Content-Length: 64

[Object]
```

### 응답

```shell
HTTP/1.1200 OK
Content-Type: application/xml
Content-Length: 0
Date: Wed,16 Aug 2017 11: 59: 33 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDMzYTRfMjQ4OGY3Xzc3NGRfMWY=
```
