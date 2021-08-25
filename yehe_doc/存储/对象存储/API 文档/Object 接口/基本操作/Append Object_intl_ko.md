## 기능 설명

APPEND Object 인터페이스 요청은 블록 추가 방식으로 객체를 지정된 버킷에 업로드할 수 있습니다. 최초로 APPEND Object 인터페이스를 사용하여 객체를 업로드할 때, 객체 속성은 자동으로 appendable이 되며, 다른 인터페이스를 사용하여 업로드하면 속성이 자동으로 normal이 되고(해당 객체가 이미 있는 경우 속성이 normal로 덮어쓰기 됩니다), [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) 또는 [HEAD Object](https://intl.cloud.tencent.com/document/ product/436/7745) 인터페이스를 통해 x-cos -object-type 응답 헤더를 가져와 객체 속성을 판단할 수 있습니다. 객체 속성이 appendable인 경우에만 본 인터페이스를 사용하여 추가 업로드할 수 있습니다.

추가로 업로드 객체의 경우, 각 블록의 최대 크기는 기본적으로 5GB이고, 최소 제한은 없으며, 추가 방법으로 생성되는 객체의 크기는 5GB를 초과하지 않아야 합니다. Position 값이 현재 객체의 길이와 같지 않으면 COS는 409 오류를 반환합니다. normal 속성 파일을 추가할 경우, COS는 409 ObjectNotAppendable을 반환합니다.

>! 
>- Appendable 객체는 복제할 수 없고, 버전 관리 및 수명 주기 관리에 참여하지 않으며, 리전 간 복제가 불가능합니다.
>- APPEND 인터페이스를 사용하여 추가 업로드하는 경우, COS는 요청에 포함된 스토리지 유형을 검증하지 않고 현재 객체의 스토리지 유형만을 기준으로 합니다.
>- APPEND 인터페이스는 INTELLIGENT TIERING 유형을 지원하지 않습니다.

## 요청

#### 요청 예시

```sh
POST /ObjectName?append&position=*position* HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: size
Content-Type: ContentType
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com. 이 중 &lt;BucketName-APPID>는 APPID 확장자를 가진 버킷 이름입니다. 예: examplebucket-1250000000, [버킷 개요 > 기본 정보](https://intl.cloud.tencent.com/document/product/436/38493) 및 [버킷 개요 > 버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312) 문서를 참고하십시오. &lt;Region>은 COS의 가용 리전입니다. [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참고하십시오.
> - Authorization: Auth String(자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참고하십시오).
> 

#### 요청 헤더

#### 공통 헤더

이 요청 작업의 구현은 공통 요청 헤더를 사용하며, 공통 요청 헤더에 대한 자세한 내용은 [공통 요청 헤더](https://intl.cloud.tencent.com/document/product/436/7728)문서를 참고하십시오.

#### 비공통 헤더

**필수 헤더**
이 요청 작업의 구현은 다음 필수 헤더를 사용합니다.

| 이름           | 설명                                        | 유형   | 필수 선택 여부 |
| -------------- | ------------------------------------------- | ------ | ---- |
| Content-Length | RFC 2616에서 정의된 HTTP 요청 콘텐츠 길이(바이트) | String | 예   |

**권장 헤더**
이 요청 작업의 구현은 다음 권장 요청 헤더 정보를 사용합니다.

|노드 이름(키워드)  |설명                                                         | 유형   | 필수 선택 여부|
| ------------------- | ------------------------------------------------------------ | ------ | ---- |
| Cache-Control       | RFC 2616에서 정의된 캐시 정책. Object 메타데이터로 반환          | String | 아니요   |
| Content-Disposition | RFC 2616에서 정의된 파일 이름. Object 메타데이터로 반환          | String | 아니요   |
| Content-Encoding    | RFC 2616에서 정의된 인코딩 형식. Object 메타데이터로 반환          | String | 아니요   |
| Content-MD5 | RFC 1864에서 정의된 요청 본문 콘텐츠의 16바이트 2진법 MD5 해시 값의 Base64 인코딩 형식. 무결성 검사에 사용되며, 요청 본문이 전송 과정 중 변경되었는지 확인하며, 최종 값의 길이는 24자이어야 합니다. 코드를 작성할 때 반드시 정확한 메소드와 매개변수를 사용하십시오. 예: `ZzD3iDJdrMAAb00lgLLeig==` | String | 아니요 |
| Content-Type        | RFC 2616에서 정의된 콘텐츠 유형(MIME). Object 메타데이터로 반환  | String | 아니요   |
| Expect                 | Expect: 100-continue 사용 시 서버의 확인을 받아야만 요청 콘텐츠를 발송할 수 있습니다. | String           | 아니요   |
| Expires             | RFC 2616에서 정의된 만료 시간. Object 메타데이터로 반환          | String | 아니요   |
| x-cos-meta- *       | 사용자 정의된 헤더 정보 허용. Object 메타데이터로 반환. 크기는 2K로 제한. | String | 아니요   |

**권한 관련 헤더**
이 요청 작업의 구현은 POST 요청의 x-cos-acl 헤더를 사용하여 파일 액세스 권한을 설정할 수 있습니다. 현재 public-read-write, public-read 및 private의 세 가지 유형의 Object 액세스 권한이 있습니다. 설정하지 않으면 기본값은 private 권한입니다. 사용자에게 읽기, 쓰기 또는 읽기 및 쓰기 권한을 개별적으로 여할 수도 있습니다. 내용은 다음과 같습니다.

>? ACL 요청 관련 자세한 내용은 [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) 문서를 참고하십시오.

| 이름                   | 설명                                                         | 유형   | 필수 입력 여부 |
| ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| x-cos-acl | Object의 ACL 속성 정의, 유효값은 private, public-read-write, public-read<br>기본값은 private | String | 아니요 |
| x-cos-grant-read | 권한 수여자에게 읽기 권한 부여, 형식: `x-cos-grant-read: id=" ",id=" "`<br><li>서브 계정에 권한 부여 시, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한 부여 시, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | 아니요 |
| x-cos-grant-write        | 권한 수여자에게 쓰기 권한 부여, 형식:`x-cos-grant-write: id=" ",id=" "` <br><li>서브 계정에 권한 부여 시, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한 부여 시,`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | 아니요   |
| x-cos-grant-full-control | 권한 수여자에게 읽기/쓰기 권한 부여, 형식:`x-cos-grant-full-control: id=" ",id=" "`<br><li> 서브 계정에 권한 부여 시, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br> <li>루트 계정에 권한 부여 시, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` | String | 아니요   |

#### 요청 매개변수

구체적인 내용은 아래와 같습니다.

| 매개변수 이름    | 설명                                                         | 유형  | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------- | ---- |
| position | 추가 작업의 시작점, 단위: 바이트. 최초 추가는 Position=0으로 설정하고 후속 추가는 Position을 현재 Object의 content-length로 설정 | Int | 예 |

#### 요청 본문

해당 요청의 요청 본문은 공란입니다.

## 응답

#### 응답 헤더

#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 사용하며, 공통 요청 헤더에 대한 자세한 내용은 [공통 응답 헤더](https://intl.cloud.tencent.com/document/product/436/7729) 문서를 참고하십시오.

#### 특수 응답 헤더

해당 요청 작업의 응답 헤더에 대한 구체적인 데이터는 다음과 같습니다.

|노드 이름(키워드)  |설명                                                         | 유형   |
| -------------------------- | ---------------------------------- | ------ |
| x-cos-next-append-position | 다음 추가 작업의 시작점, 단위: 바이트. | String |
| ETag                       | 파일의 유일한 식별자                     | String |


#### 응답 본문

해당 응답 본문은 공란으로 반환됩니다.

#### 오류 분석

1. 비 appendable 파일에 APPEND 작업을 실행하면 409 Confilct가 반환됩니다. 오류 메시지:
The operation is not valid for the current state of the object。
2. 요청에 position 매개변수가 포함되지 않은 경우 400 Bad Request가 반환되고 오류 메시지: InvalidArgument가 반환됩니다.
3. 요청에 Content-Length 헤더가 없으면 411 Length Required가 반환됩니다. 오류 메시지:
You must provide the Content-Length HTTP header。

COS 오류 코드 또는 전체 제품 오류 리스트에 대한 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오.

## 실제 사례

#### 요청

```sh
POST /coss3/app?append&position=0 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 16 Jan 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3M****&q-sign-time=1484208848;32557104848&q-key-time=1484208848;32557104848&q-header-list=host&q-url-param-list=append;position&q-signature=855fe6b833fadf20570f7f650e2120e17ce8****
Content-Length: 4096

[Object]
```

#### 응답

```sh
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Tue, 16 Jan 2016 21:32:00 GMT
ETag: 1ce5b469b7d6600ecc2fd112e570917b
Server: tencent-cos
x-cos-content-sha1: 1ceaf73df40e531df3bfb26b4fb7cd95fb7bff1d
x-cos-next-append-position: 4096
x-cos-request-id: NTg3NzNhZGZfMmM4OGY3X2I2Zl8x****
```
