## 기능 설명

Upload Part 인터페이스는 블록 단위로 COS에 객체 업로드를 구현합니다. 최대 10,000개의 블록을 지원하며 각 블록의 크기는 1MB - 5GB이고 마지막 블록은 1MB 미만일 수 있습니다.

> ? 
> 1. 먼저 [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)를 통해 초기화합니다. 초기화 후 이 업로드를 고유하게 식별하는 UploadId를 얻습니다.
> 2. Upload Part를 요청할 때마다 partNumber와 uploadId가 필요합니다. partNumber는 파트의 번호로, 비순차 업로드를 지원합니다.
> 3. uploadId와 partNumber가 동일할 때, 나중에 업로드 요청을 시작하는 파트가 이전 파트를 덮어씁니다. uploadId가 존재하지 않을 경우 404 오류인 NoSuchUpload를 반환합니다.
> 

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer 사용 권장
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=UploadPart&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>디버깅 클릭</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 검색 인터페이스 등의 기능을 제공합니다. 각 호출의 요청 내용 및 반환 결과를 확인하고 SDK 호출 예시를 자동으로 생성할 수 있습니다.
            </div>
        </div>
    </div>
</div>

## 요청

#### 요청 예시

```plaintext
PUT /<ObjectKey>?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: Content Type
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Object Part]
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com，이 중 &lt;BucketName-APPID> 는 APPID 확장자를 가진 버킷 이름입니다. 예: examplebucket-1250000000. [버킷 개요 > 기본 정보](https://intl.cloud.tencent.com/document/product/436/38493) 및 [버킷 개요 > 버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312) 문서를 참고하십시오. &lt;Region>은 COS의 가용 리전입니다. [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참고하십시오.
> - Authorization: Auth String(자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참고하십시오).
> 

#### 요청 매개변수 

| 이름      | 설명                                                         | 유형   | 필수 입력 여부 |
| ---------- | ------------------------------------------------------------ | ------- | -------- |
| partNumber | 이 멀티파트 업로드의 번호를 식별합니다. 범위: 1 - 10000.                | integer | Yes       |
| uploadId         | 이번 멀티파트 업로드 ID 표시. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다. | string | Yes   |

#### 요청 헤더

본 인터페이스는 공통 요청 헤더 뿐만 아니라, 아래의 요청 헤더도 지원합니다. 공통 요청 헤더 관련 자세한 내용은 [공통 요청 헤더](https://intl.cloud.tencent.com/document/product/436/7728) 문서를 참고하십시오.

**서버 암호화(SSE) 관련 헤더**

현재 멀티파트 업로드 초기화 시 SSE-C를 사용한 경우, 멀티파트 업로드 시 지정한 암호화 알고리즘과 키 정보를 지정하고 멀티파트 업로드를 초기화해야 합니다. 그렇지 않으면 다음 헤더를 지정할 수 없습니다.

| 이름                                            | 설명                                                         | 유형   | 필수 선택 여부 |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | -------- |
| x-cos-server-side-encryption-customer-algorithm | 서버측 암호화 알고리즘, 현재 AES256만 지원                            | string | Yes       |
| x-cos-server-side-encryption-customer-key       | 서버 암호화 키의 Base64 인코딩<br>예시: `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes       |
| x-cos-server-side-encryption-customer-key-MD5   | Base64 인코딩을 사용하는 서버 암호화 키의 MD5 해시 값<br>예시: `U5L61r7jcwdNvT7frmUG8g==` | string | Yes       |
| x-cos-traffic-limit | 이 멀티파트 업로드에 대한 트래픽 제어 속도 제한 값은 숫자여야 하며 기본 단위는 bit/s입니다. 속도 제한 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s이며, 이 범위를 초과하면 400 오류가 반환됩니다. | integer | No       |

#### 요청 본문

이 인터페이스 요청의 요청 본문은 객체(파일)의 블록 콘텐츠입니다.

## 응답

#### 응답 헤더

본 인터페이스는 공동 응답 헤더를 반환하는 것 외에 다음 응답 헤더도 반환합니다. 공동 응답 헤더에 대한 자세한 내용은 [공동 응답 헤더](https://intl.cloud.tencent.com/document/product/436/7729) 문서를 참고하십시오.

**서버 암호화(SSE) 관련 헤더**

멀티파트 업로드 초기화 시 서버 암호화를 사용한 경우 이 인터페이스는 서버 암호화 전용 헤더를 반환합니다. [서버 암호화 전용 헤더](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8)를 참고하십시오.

#### 응답 본문

해당 요청의 응답 본문은 공란입니다.

#### 오류 코드

이 인터페이스는 통일된 오류 응답 및 오류 코드를 따르며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오.

## 실제 사례

#### 사례 1: 단순 사례

#### 요청

```plaintext
PUT /exampleobject?partNumber=1&uploadId=1585130821cbb7df1d11846c073ad648e8f33b087cec2381df437acdc833cf654b9ecc6361 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 25 Mar 2020 10:07:14 GMT
Content-Type: application/octet-stream
Content-Length: 1048576
Content-MD5: OScKloo1fSQgfpkRFiUH6w==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1585130834;1585138034&q-key-time=1585130834;1585138034&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=partnumber;uploadid&q-signature=a815da18232cfec87e8218f32f31b1e2c5eb****
Connection: close

[Object Part]
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Wed, 25 Mar 2020 10:07:14 GMT
ETag: "39270a968a357d24207e9911162507eb"
Server: tencent-cos
x-cos-hash-crc64ecma: 9973912126177188060
x-cos-request-id: NWU3YjJkNTJfZDBjODJhMDlfMjU4NTZfMjc5MzBh****
```

#### 사례 2: 서버측 암호화 SSE-COS 사용

#### 요청

```plaintext
PUT /exampleobject?partNumber=1&uploadId=1590862540251355295a5c736513d70d42b92bbde4f0fafb5e0ecb314b55aa0018cc9fa76f HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:15:50 GMT
Content-Type: application/octet-stream
Content-Length: 13
Content-MD5: EI9SjrY7Zec08nrjMfX/qg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862550;1590869750&q-key-time=1590862550;1590869750&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=partnumber;uploadid&q-signature=2a0085596de5861410bcc43f3d107dc9dda5****
Connection: close

[Object Part]
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sat, 30 May 2020 18:15:51 GMT
ETag: "108f528eb63b65e734f27ae331f5ffaa"
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEyZDZfYjNjMjJhMDlfMmJlM18zOWI2****
x-cos-server-side-encryption: AES256
```

#### 사례 3: 서버측 암호화 SSE-KMS 사용

#### 요청

```plaintext
PUT /exampleobject?partNumber=1&uploadId=15908625793957d71176fa878282d266a95b79dc2aec159b4a73d1d79c80d4f931cda6ad65 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:16:29 GMT
Content-Type: application/octet-stream
Content-Length: 13
Content-MD5: EI9SjrY7Zec08nrjMfX/qg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862589;1590869789&q-key-time=1590862589;1590869789&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=partnumber;uploadid&q-signature=2d1231c77c72727bd1c2454726813e095a7e****
Connection: close

[Object Part]
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sat, 30 May 2020 18:16:30 GMT
ETag: "1d3e8ae9da423b440341b09f1616f074"
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEyZmRfYTRiOTJhMDlfMTE0ZGRfMmE3OTk4****
x-cos-server-side-encryption: cos/kms
x-cos-server-side-encryption-cos-kms-key-id: 48ba38aa-26c5-11ea-855c-52540085****
```

#### 사례 4: 서버 측 암호화 SSE-C 사용

#### 요청

```plaintext
PUT /exampleobject?partNumber=1&uploadId=1590862610acd643927bad05cd3947bf98b56b04b0b0b2a45a49969f87cc95b7fd5fcc065a HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sat, 30 May 2020 18:17:01 GMT
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key: MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
Content-Type: application/octet-stream
Content-Length: 13
Content-MD5: EI9SjrY7Zec08nrjMfX/qg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1590862621;1590869821&q-key-time=1590862621;1590869821&q-header-list=content-length;content-md5;content-type;date;host;x-cos-server-side-encryption-customer-algorithm;x-cos-server-side-encryption-customer-key;x-cos-server-side-encryption-customer-key-md5&q-url-param-list=partnumber;uploadid&q-signature=6d0914f1db0e03569b6b5d340dc8d71616bf****
Connection: close

[Object Part]
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sat, 30 May 2020 18:17:01 GMT
ETag: "ff14981a35a58eb97bca838b055c573b"
Server: tencent-cos
x-cos-hash-crc64ecma: 4510578591875220731
x-cos-request-id: NWVkMmEzMWRfYjRjOTJhMDlfYWRhXzFhZmYw****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
```
