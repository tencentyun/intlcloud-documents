## 소개

본 문서는 객체의 고급 인터페이스, 간단한 작업, 멀티파트 작업 관련 API 개요 및 SDK 예시 코드를 제공합니다.
**간단한 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket(List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 쿼리| 버킷의 일부 또는 모든 객체 쿼리|
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 업로드       | 버킷에 객체 업로드    |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 폼을 사용한 객체 업로드   | 폼을 사용한 객체 업로드 요청                     |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 쿼리  | 객체의 메타데이터 쿼리                |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬 파일 시스템에 객체 다운로드        |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | 크로스 도메인 설정 사전 요청 | 사전 요청을 통해 실제 크로스 도메인 요청의 발송 가능 여부 확인 |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사       | 객체를 타깃 경로에 복사(객체 키)             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) |  객체 삭제   | 버킷에서 객체 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 여러 개체 삭제   | 버킷에서 여러 객체 삭제 |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 아카이브 객체 복구 | 아카이브 유형의 객체 검색 및 액세스                      |


**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 작업 초기화                   |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 멀티파트 업로드       | 객체 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회     |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 객체의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지 | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 사용 예시

예시1: 디렉터리 a의 모든 파일을 나열합니다.

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',     /* 필수 */
    Prefix: ’a/’,           /* 옵션 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

반환 값 형식:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "",
    "Marker": "a/",
    "MaxKeys": "1000",
    "Delimiter": "",
    "IsTruncated": "false",
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

예시2: 디렉터리 a의 모든 파일을 열거하고, 깊이 탐색은 하지 않습니다.

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```js
cos.getBucket({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Prefix: ’a/’,              /* 옵션 */
    Delimiter: ’/’,            /* 옵션 */
}, function(err, data) {
    console.log(err || data.CommonPrefixes);
});
```

반환 값 형식:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "a/",
    "Marker": "",
    "MaxKeys": "1000",
    "Delimiter": "/",
    "IsTruncated": "false",
    "CommonPrefixes": [{
        "Prefix": "a/1/"
    }],
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

예시3: 디렉터리의 모든 파일을 나열합니다.

```js
var bucket = ’examplebucket-1250000000’;
var region = ’ap-beijing’;
var prefix = ’examplefolder/’;  /* 삭제할 디렉터리 또는 접두사 */
var listFolder = function(marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function(err, data) {
        if (err) {
            return console.log(’list error:’, err);
        } else {
            console.log(’list result:’, data.Contents);
            if (data.IsTruncated === ’true’) listFolder(data.NextMarker);
            else return console.log(’list complete’);
        }
    });
};
listFolder();
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String | Yes   |
| Region       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String      | Yes   |
| Prefix       | 객체 키의 접두사 매칭. 지정된 접두사를 포함한 객체 키만 한정하여 반환합니다.             | String | No   |
| Delimiter    | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용하며, 보통 `/`로 표시합니다. 모든 객체 키는 Prefix 또는 처음(Prefix 미지정 시)부터 첫 번째 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의하여, 모든 Common Prefix를 열거합니다. | String | No   |
| Marker       | 시작하는 객체 키를 표시. Marker부터 시작되는 MaxKeys 항목을 열거하며, 기본적으로 UTF-8 사전 순서에 따라 열거합니다. | String | No   |
| MaxKeys      | 한 번에 반환하는 최대 항목 수. 기본값은 1000이며, 최대값은 1000입니다.                 | String | No   |
| EncodingType | 규정된 반환 값의 인코딩 방식은 url 선택 가능. 반환 객체 키를 대표하는 것은 URL 인코딩(퍼센트 인코딩)값입니다. 예를 들어, ‘Tencent Cloud’는 `%E8%85%BE%E8%AE%AF%E4%BA%91`로 인코딩되었습니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| data              | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - Name            | 버킷 이름. 형식은 &lt;BucketName-APPID>입니다. 예: examplebucket-1250000000 | String      |
| - Prefix          | 객체 키 접두사 매칭. 해당 표기 다음부터(해당 표기 불포함) UTF-8 사전 순서에 따라 객체 키 항목을 반환합니다. | String      |
| - Marker          | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 Marker부터 시작합니다.  | String      |
| - MaxKeys         | 단일 응답 요청에 반환되는 결과의 최대 항목 수                       | String      |
| - Delimiter       | 구분 문자                                                       | String      |
| - IsTruncated     | 응답 요청 항목이 잘렸는지 여부. 값: ’true’ 또는 ’false’             | String      |
| - NextMarker      | 반환 항목이 잘린 경우 NextMarker를 반환하며, 다음 항목의 시작점을 표시합니다.   | String      |
| - CommonPrefixes  | Prefix부터 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의합니다. | ObjectArray |
| - - Prefix        | 단일 Common Prefix의 접두사                                   | String      |
| - EncodingType    | 반환값의 인코딩 방식. Delimiter, Marker, Prefix, NextMarker, Key에 적용됩니다. | String      |
| - Contents        | 객체 메타데이터 정보 리스트                                           | ObjectArray |
| - - Key           | 객체 키. 즉 객체의 이름                                         | String      |
| - - ETag          | 객체 콘텐츠에 따라 계산된 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`). **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String      |
| - - Size          | 객체의 크기. 단위: Byte                                          | String      |
| - - LastModified  | ISO8601 형식의 객체 마지막 수정 시간. 예: 2019-05-24T10:56:40Z | String      |
| - - Owner         | 객체 소유자 정보                                               | Object      |
| - - - ID          | 객체 소유자의 전체 ID. 형식은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`입니다. 예: `qcs::cam::uin/100000000001:uin/100000000001`, 여기에서 100000000001이 uin입니다. | String      |
| - - - DisplayName | 객체 소유자 이름                                             | String      |
| - - StorageClass  | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오. | String      |

### 객체 간편 업로드

#### 기능 설명

PUT Object 인터페이스는 객체를 지정된 버킷에 업로드할 수 있습니다. 이 작업은 요청자가 버킷에 대한 WRITE 권한을 가지고 있어야 합니다. 최대 5GB 이하인 객체의 업로드를 지원합니다. 5GB 이상의 객체는 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 혹은 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) 업로드를 사용하십시오.

> !
> - Key(파일명)는 `/`로 끝날 수 없습니다. 그렇지 않을 경우 폴더로 인식될 수 있습니다.
> - 루트 계정(동일한 APPID)당 버킷의 ACL 규칙 수량은 최대 1000개이며, 객체 ACL 규칙 수량은 제한이 없습니다. 객체 ACL 제어가 필요하지 않을 경우 업로드 시 설정하지 마십시오. 기본적으로 버킷 권한이 상속됩니다.
> - 업로드 후, 동일한 Key로 사전 서명된 링크를 생성할 수 있습니다. 다운로드 시 method를 GET으로 지정하십시오. 자세한 인터페이스 설명은 아래를 참고하시기 바라며, 다른 단말기로 공유하여 다운로드할 수 있습니다. 주의: 파일이 개인 읽기 권한인 경우 사전 서명된 링크에 유효기간이 있습니다.
> 

#### 사용 예시

간편한 파일 업로드는 용량이 작은 파일을 업로드하는 데 적합합니다.

[//]: # (.cssg-snippet-put-object)
```js
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: fs.createReadStream(filePath), // 파일 객체 업로드
    ContentLength: fs.statSync(filepath).size,  // Body가 파일 스트림인 경우 파일 크기를 전달해야 합니다. 그렇지 않으면 onProgress가 정확한 진행률 정보를 반환할 수 없습니다.
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Buffer를 파일 콘텐츠로 업로드합니다.

[//]: # (.cssg-snippet-put-object-bytes)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    Body: Buffer.from('hello!'), /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

문자열을 파일 콘텐츠로 업로드합니다.

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    Body: ’hello!’,
}, function(err, data) {
    console.log(err || data);
});
```

base64를 파일 콘텐츠로 업로드합니다.

[//]: # (.cssg-snippet-put-object-string)
```js
var base64Url = ’data:image/png;base64,iVBORw0KGgo.....’;
// Buffer로 전환하여 업로드해야 합니다.
var body = Buffer.from(base64Url.split(',')[1] , 'base64');
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject.png’,              /* 필수 */
    Body: body,
}, function(err, data) {
    console.log(err || data);
});
```

디렉터리를 생성합니다.

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'a/',              /* 필수 */
    Body: ’’,
}, function(err, data) {
    console.log(err || data);
});
```

지정 디렉터리에 파일을 업로드합니다.

```js
var folder = ’examplefolder/’;
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: folder + ’exampleobject’,              /* 필수 */
    Body: fileObject, // 파일 객체 업로드
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

객체 업로드(단일 링크 속도 제한)

>?객체 업로드 속도 제한에 대한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하십시오.

[//]: # (.cssg-snippet-put-object-traffic-limit)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: fileObject, // 파일 객체 업로드
    Headers: {
      'x-cos-traffic-limit': 819200, // 속도 제한 설정 범위는 819200 - 838860800, 즉 100KB/s - 100MB/s이며, 이 범위를 초과하면 400 오류가 반환됩니다.
    },
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket                 | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String               | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.| String               | Yes   |
| Key                    | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String               | Yes   |
| Body                   | 파일 콘텐츠 업로드. FileStream, 문자열, Buffer 등이 될 수 있습니다.            | Stream/Buffer/String | Yes   |
| CacheControl           | RFC 2616에 정의된 캐시 정책. 객체의 메타데이터로 저장됩니다.             | String               | No   |
| ContentDisposition     | RFC 2616에 정의된 파일 이름. 객체의 메타데이터로 저장됩니다.             | String               | No   |
| ContentEncoding        | RFC 2616에 정의된 인코딩 형식. 객체의 메타데이터로 저장됩니다.             | String               | No   |
| ContentLength          | RFC 2616에 정의된 HTTP 요청 콘텐츠 길이(바이트)                   | String               | No   |
| ContentType            | RFC 2616에 정의된 콘텐츠 유형(MIME). 객체의 메타데이터로 저장됩니다.     | String               | No   |
| Expires                | RFC 2616에 정의된 만료 기간. 객체의 메타데이터로 저장됩니다. 만료 후에는 유효하지 않은 캐시가 되며, 파일은 삭제되지 않습니다.            | String           | No   |
| Expect                 | Expect: 100-continue 사용 시 서버의 확인을 받아야만 요청 콘텐츠를 발송할 수 있습니다. | String               | No   |
| ACL                    | 객체의 ACL 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참고하십시오. </br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본적인 버킷 권한을 상속하십시오.** | String               | No   |
| GrantRead              | 권한 피부여자에게 객체 읽기 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>예: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul>| String               | No   |
| GrantReadAcp           | 권한 피부여자에게 객체의 ACL을 읽을 수 있는 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>예: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String               | No   |
| GrantWriteAcp          | 권한 피부여자에게 객체의 ACL을 입력할 수 있는 권한을 부여합니다. 형식은id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>예: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul> | String               | No   |
| GrantFullControl       | 권한 피부여자에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code></br>예: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String               | No   |
| StorageClass           | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오. 기본값은 STANDARD입니다. | String               | No   |
| x-cos-meta-\*           | 사용자 정의가 허용된 헤더 정보. 객체의 메타데이터로 저장되며, 크기는 2KB로 제한됩니다. | String               | No   |
| onTaskReady            | 업로드 작업 생성 시의 콜백 함수. taskId 하나를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function             | No   |
| - taskId               | 업로드 작업의 번호                                               | String               | No   |
| onProgress             | 진행률 콜백 함수. 진행률 콜백 응답 객체(progressData)의 속성은 다음과 같습니다.     | Function             | No   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number               | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number               | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number               | No   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다. 예: 업로드 50%를 0.5로 표시       | Number               | No   |


#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - ETag       | 파일의 MD5 알고리즘 검증값 반환. ETag 값은 업로드 과정에서 객체 손상 여부를 검사하는 데 사용할 수 있습니다.<br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 폼을 사용한 객체 업로드

Node.js SDK는 POST Object 인터페이스에 해당하는 방법을 제공하지 않습니다. 해당 인터페이스가 필요한 경우 [Web 다이렉트 업로드 사례](https://intl.cloud.tencent.com/document/product/436/9067)의 '솔루션 B: 폼(Form)을 사용하여 업로드'를 참고하십시오.

### 객체 메타데이터 조회

#### 기능 설명

객체의 메타데이터 정보를 조회합니다.

#### 사용 예시

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,               /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | 버킷의 이름. 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String | Yes   |
| Region          | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key             | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| IfModifiedSince | 지정된 시간 이후에 수정될 경우 해당하는 메타데이터 정보를 반환하고, 그렇지 않을 경우 304를 반환합니다.    | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   |요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                  | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 304 등). 지정 시간이 지난 후 수정되지 않은 경우 304를 반환합니다. | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| - x-cos-object-type   | 객체의 추가 업로드 가능 여부 표시. 열거 값은 normal, appendable이 있으며, 기본값은 normal로 반환에 표시되지 않습니다. | String  |
| - x-cos-storage-class | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE가 있으며, 기본값은 STANDARD로 반환에 표시되지 않습니다. | String  |
| - x-cos-meta-*        | 사용자 정의된 meta                                            | String  |
| - NotModified         | 지정 시간 이후 객체의 수정 여부                                 | Boolean |
| - ETag                | 파일의 MD5 알고리즘 검증값 반환. ETag 값은 업로드 과정에서 객체 손상 여부를 검사하는 데 사용할 수 있습니다.<br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다.** | String  |
| - VersionId           | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String  |

### 객체 다운로드

GET Object 인터페이스 요청으로 버킷 내 지정 객체의 콘텐츠를 가져오거나 로컬에 다운로드할 수 있습니다. 해당 API의 요청자는 타깃 객체에 대한 읽기 권한이 있거나 모든 사람에게 타깃 객체의 읽기 권한이 개방되어 있어야 합니다(공개 읽기).

#### 사용 예시

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Range를 지정하여 파일 콘텐츠를 가져옵니다.

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    Range: ’bytes=1-3’,        /* 옵션 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

지정 경로에 파일을 다운로드합니다.

[//]: # (.cssg-snippet-get-object-path)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    Output: './exampleobject',
}, function(err, data) {
    console.log(err || data);
});
```

지정한 파일 입력 스트림에 파일을 다운로드합니다.

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

객체 다운로드(단일 링크 속도 제한)

>?객체 다운로드 속도 제한에 대한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하십시오.

[//]: # (.cssg-snippet-get-object-traffic-limit)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,              /* 필수 */
    Headers: {
      'x-cos-traffic-limit': 819200, // 속도 제한 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s이며, 이 범위를 초과하면 400 오류가 반환됩니다.
    },
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형               | 필수 입력 여부 |
| -------------------------- | ------------------------------------------------------------ | ------------------ | ---- |
| Bucket                     | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String             | Yes   |
| Region                     | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String             | Yes   |
| Key                        | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String             | Yes   |
| Output                     | 출력하는 파일 경로 또는 입력 스트림. 불러오지 않으면 전체 콘텐츠를 콜백 함수 data로 입력합니다. | String/WriteStream | No   |
| ResponseContentType        | 응답 헤더의 Content-Type 매개변수 설정                           | String             | No   |
| ResponseContentLanguage    | 반환 헤더의 Content-Language 매개변수 설정                       | String             | No   |
| ResponseExpires            | 반환 헤더의 Content-Expires 매개변수 설정                        | String             | No   |
| ResponseCacheControl       | 반환 헤더의 Cache-Control 매개변수 설정                          | String             | No   |
| ResponseContentDisposition | 반환 헤더의 Content-Disposition 매개변수 설정                    | String             | No   |
| ResponseContentEncoding    | 반환 헤더의 Content-Encoding 매개변수 설정                       | String             | No   |
| Range                      | RFC 2616에 정의된 바이트 범위. 범위 값은 반드시 bytes=first-last 형식을 사용해야 합니다. first와 last는 0부터 시작하는 오프셋을 기반으로 합니다. 예를 들어, bytes=0-9는 객체의 첫 10바이트 데이터를 다운로드한다는 의미입니다. 지정하지 않을 경우 객체 전체를 다운로드합니다. | String             | No   |
| IfModifiedSince            | 객체가 지정된 시간 이후에 수정되는 경우 해당 객체의 메타데이터 정보를 반환하며, 그렇지 않을 경우 304(not modified)를 반환합니다. | String             | No   |
| IfUnmodifiedSince          | 객체가 지정된 시간 이후에 수정되지 않을 경우 객체를 반환하며, 그렇지 않을 경우 412(precondition failed)를 반환합니다. | String             | No   |
| IfMatch                    | ETag가 지정된 콘텐츠와 일치해야 객체를 반환하며, 그렇지 않을 경우 412(precondition failed)를 반환합니다. | String             | No   |
| IfNoneMatch                | ETag가 지정된 콘텐츠와 불일치해야 객체를 반환하며, 그렇지 않을 경우 304(not modified)를 반환합니다. | String             | No   |
| VersionId                  | 다운로드할 객체의 버전 ID 지정                                    | String             | No   |
| onProgress                 | 진행률 콜백 함수. 진행률 콜백 응답 객체(progressData)의 속성은 다음과 같습니다.     | Function           | No   |
| - progressData.loaded      | 다운로드한 객체의 일부 크기. 단위: 바이트(Bytes)                | Number             | No   |
| - progressData.total       | 객체의 전체 크기. 단위: 바이트(Bytes)                        | Number             | No   |
| - progressData.speed       | 객체의 다운로드 속도. 단위: 바이트/초(Bytes/s)                   | Number             | No   |
| - progressData.percent     | 객체의 다운로드 백분율. 소수점으로 표시합니다. 예: 다운로드 50%를 0.5로 표시       | Number             | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   |요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                  | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 304, 403, 404 등)             | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| - CacheControl        | RFC 2616에 정의된 캐시 명령어. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - ContentDisposition  | RFC 2616에 정의된 파일 이름. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - ContentEncoding     | RFC 2616에 정의된 인코딩 형식. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - Expires             | RFC 2616에 정의된 캐시 만료 시간. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다.  | String  |
| - x-cos-storage-class | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE가 있습니다. </br>**해당 헤더가 반환되지 않으면 플레인 텍스트 파일 스토리지 유형이 STANDARD(표준 스토리지)라는 의미입니다.** | String  |
| - x-cos-meta-\*        | 사용자 정의된 메타데이터                                           | String  |
| - NotModified         | 요청 시 IfModifiedSince가 있을 경우 해당 속성을 반환합니다. 파일이 수정되지 않은 경우 true, 수정된 경우 false입니다. | Boolean |
| - ETag                | 반환 파일의 MD5 알고리즘 검증값. ETag 값은 업로드 과정에서의 객체 손상 여부를 검사하는 데 사용할 수 있습니다. </br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다.** | String  |
| - VersionId           | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String  |
| - Body                | 반환되는 파일 콘텐츠. 기본 Buffer 포맷.                           | Buffer  |

### 크로스 도메인 설정 사전 요청

#### 기능 설명

OPTIONS Object 인터페이스는 객체에 대한 크로스 도메인 액세스 설정을 사전 요청합니다. 즉, 크로스 도메인 요청 발송 전 OPTIONS 요청과 특정 출처, HTTP 방법, 헤더 정보 등을 COS에 보내 실제 크로스 도메인 요청 가능 여부를 결정합니다. CORS 설정이 존재하지 않을 경우 요청에 대해 403 Forbidden이 반환됩니다. **사용자는 PUT Bucket cors 인터페이스를 통해 버킷의 CORS 지원을 활성화할 수 있습니다.**

#### 사용 예시

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    Origin: ’https://www.qq.com’,      /* 필수 */
    AccessControlRequestMethod: ’PUT’, /* 필수 */
    AccessControlRequestHeaders: ’origin,accept,content-type’ /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String | Yes   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| Origin                      | 크로스 도메인 액세스 시뮬레이션을 요청하는 원본 도메인                                   | String | Yes   |
| AccessControlRequestMethod  | 크로스 도메인 액세스 시뮬레이션을 요청하는 HTTP 방법                                 | String | Yes   |
| AccessControlRequestHeaders | 크로스 도메인 액세스 시뮬레이션을 요청하는 헤더                                       | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형    |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object  |
| - statusCode                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers                    | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object  |
| - headers                    | 요청 시 반환되는 헤더 정보                                           | Object  |
| - statusCode                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - AccessControlAllowOrigin   | 크로스 도메인 액세스 시뮬레이션을 요청하는 원본 도메인. 중간에 쉼표로 구분하며, 원본에서 허용하지 않는 경우 해당 Header는 반환되지 않습니다. 예: `*` | String  |
| - AccessControlAllowMethods  | 크로스 도메인 액세스 시뮬레이션을 요청하는 HTTP 방법. 중간에 쉼표로 구분하며, 요청 방법을 허용하지 않는 경우 해당 Header는 반환되지 않습니다. 예: PUT, GET, POST, DELETE, HEAD | String  |
| - AccessControlAllowHeaders  | 크로스 도메인 액세스 시뮬레이션을 요청하는 헤더. 중간에 쉼표로 구분하며, 모든 요청 헤더 시뮬레이션을 허용하지 않는 경우 해당 Header는 요청 헤더를 반환하지 않습니다. 예: accept, content-type, origin, authorization | String  |
| - AccessControlExposeHeaders | 크로스 도메인은 헤더 반환을 지원하며, 중간에 쉼표로 구분합니다. 예: ETag                  | String  |
| - AccessControlMaxAge        | OPTIONS 요청이 결과를 얻는 유효기간을 설정합니다. 예: 3600                  | String  |
| - OptionsForbidden           | OPTIONS 요청 거부 여부. 반환된 HTTP 상태 코드가 403이면 true입니다. | Boolean |

### 객체 복사

#### 기능 설명

PUT Object - Copy는 기존에 있는 COS 객체의 사본 생성을 요청합니다. 즉, 객체 하나를 원본 경로(객체 키)에서 타깃 경로(객체 키)로 복사합니다. 복사 과정에서 객체 메타데이터와 액세스 제어 리스트(ACL)는 수정될 수 있습니다.
사용자는 해당 인터페이스를 통해 복제본 생성, 객체 메타데이터 수정(원본 객체와 타깃 파일의 속성은 동일), 객체의 이동과 이름 변경(복사 후 단독으로 호출하여 인터페이스 삭제)이 가능합니다.

>! 객체의 크기는 1MB - 5GB를 권장합니다. 5GB를 초과하는 객체는 고급 인터페이스 객체 복사 [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12)을 사용하시기 바랍니다.
>

#### 사용 예시

객체 복사:

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: ’examplebucket-1250000000’,                               /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,                                            /* 필수 */
    CopySource: ’sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject’, /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

객체 스토리지 유형 수정:

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: ’examplebucket-1250000000’,                               /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: 'sourceObject',                                            /* Key는 CopySource의 Key와 동일, 필수 */
    CopySource: ’sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject’, /* 필수 */
    StorageClass: 'ARCHIVE',  /* 아카이브로 설정 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String | Yes   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| CopySource                  | 원본 객체 URL 경로입니다. URL 매개변수 ?versionId=&lt;versionId>를 통해 과거의 버전을 지정할 수 있습니다.  | String | Yes   |
| ACL                         | 객체의 액세스 제어 리스트(ACL) 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참고하십시오. <br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본 버킷 권한을 상속하십시오.** | String | No   |
| GrantRead                   | 권한 피부여자에게 객체 읽기 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>예: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No   |
| GrantWrite                  | 권한 피부여자에게 객체를 입력할 수 있는 권한을 부여합니다. 형식은id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>예: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'`</li></ul> | String | No   |
| GrantFullControl            | 권한 피부여자에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code></br>예: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` </li></ul>| String | No   |
| MetadataDirective           | 메타데이터 복사 여부. 열거 값은 Copy, Replaced이며, 기본값은 Copy입니다. Copy로 표기되어 있다면 Header의 사용자 메타데이터 정보를 무시하고 바로 복사합니다. Replaced로 표기되어 있다면 Header 정보에 따라 메타데이터를 수정합니다. **타깃 경로와 원본 경로가 일치할 때, 즉 사용자가 메타데이터를 수정하려고 할 때는 반드시 Replaced로 표기되어 있어야 합니다.** | String | No   |
| CopySourceIfModifiedSince   | 객체가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfNoneMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| CopySourceIfUnmodifiedSince | 객체가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| CopySourceIfMatch           | 객체의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfUnmodifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| CopySourceIfNoneMatch       | 객체의 Etag와 불일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfModifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| StorageClass                | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오. 기본값은 STANDARD입니다. | String | No   |
| x-cos-meta-\*                | 기타 사용자 정의된 파일 헤더                                         | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object  |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 요청 시 반환되는 헤더 정보                                           | Object |
| data           | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 요청 시 반환되는 헤더 정보                                           | Object |
| - ETag         | 파일의 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`) **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - LastModified | 객체의 마지막 수정 시간 반환. 예: 2017-06-23T12:33:27.000Z         | String |
| - VersionId    | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 단일 객체 삭제

#### 기능 설명

DELETE Object 인터페이스 요청을 통해 COS 버킷에서 단일 객체(Object) 삭제할 수 있습니다. 이 작업은 요청자가 버킷에 대한 WRITE 권한을 가지고 있어야 합니다.

#### 사용 예시

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject'                            /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket    | 버킷 이름. 필수 형식: BucketName-APPID | String | Yes   |
| Region    | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key       | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| VersionId | 삭제할 객체 버전 ID 또는 DeleteMarker 버전 ID                  | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등). **삭제에 성공하거나 파일이 존재하지 않을 경우 204 또는 200이 반환되고, 지정 Bucket을 찾지 못할 경우 404가 반환됩니다.** | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |

### 다수의 객체 삭제

#### 기능 설명

DELETE Multiple Objects 인터페이스 요청을 통해 지정된 버킷에서 객체 일괄 삭제할 수 있습니다. 한 번에 최대 1000개의 객체를 삭제합니다. COS는 응답 결과를 Verbose와 Quiet의 두 가지 모드로 제공합니다. Verbose 모드는 모든 객체의 삭제 결과를 반환하고, Quiet 모드는 오류가 보고된 객체 정보만 반환합니다.

#### 사용 예시

다수의 파일을 삭제합니다.

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Objects: [
        {Key: ’exampleobject’},
        {Key: ’exampleobject2’},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

접두사에 따라 여러 객체를 삭제합니다(지정 디렉터리의 파일 삭제).

```js
var bucket: ’examplebucket-1250000000’; /* 필수 */
var region: ’ap-beijing’;     /* 버킷이 위치한 리전. 필수 필드 */
var prefix = ’examplefolder/’;  /* 삭제할 디렉터리 또는 접두사 */
var deleteFolder = function (marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function (listError, listResult) {
        if (listError) return console.log(’list error:’, listError);
        var nextMarker = listResult.NextMarker;
        var objects = listResult.Contents.map(function (item) {
            return {Key: item.Key}
        });
        cos.deleteMultipleObject({
            Bucket: bucket,
            Region: region,
            Objects: objects,
        }, function (delError, deleteResult) {
            if (delError) {
                console.log(’delete error’, delError);
                console.log(’delete stop’);
            } else {
                console.log(’delete result’, deleteResult);
                if (listResult.IsTruncated === 'true') deleteFolder(nextMarker);
                else console.log(’delete complete’);
            }
        });
    });
}
deleteFolder();
```

#### 매개변수 설명

| 매개변수 이름      | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket      | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String      | Yes   |
| Region      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String      | Yes   |
| Quiet       | Boolean 값. 이 값은 Quiet 모드의 실행 여부를 결정합니다. true 값이면 Quiet 모드를 실행하고, false 값이면 Verbose 모드를 실행합니다. 기본값: false | Boolean     | No   |
| Objects     | 삭제할 객체 리스트                                             | ObjectArray | Yes   |
| - Key       | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      | Yes   |
| - VersionId | 삭제할 객체 버전 ID 또는 DeleteMarker 버전 ID                  | String      | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err                       | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode              | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등)             | Number      |
| - headers                 | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                      | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode              | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등)             | Number      |
| - headers                 | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Deleted                 | 이번에 삭제된 객체 정보 리스트 설명                               | ObjectArray |
| - - Key                   | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      |
| - - VersionId             | 매개변수에 VersionId를 전송하면 반환 시에도 VersionId가 수반됩니다. 방금 작업한 객체 버전 또는 DeleteMarker 버전을 표시합니다. | String      |
| - - DeleteMarker          | 버전 제어를 활성화한 상태에서 매개변수에 VersionId가 없으면 이번에는 파일 콘텐츠를 제거하지 않고 DeleteMarker만 하나 추가합니다. 이는 볼 수 있던 파일이 삭제되었다는 의미이며, 열거 값은 true와 false입니다. | String      |
| - - DeleteMarkerVersionId | 반환의 DeleteMarker가 true인 경우, 새로 추가된 DeleteMarker의 VersionId를 반환합니다. | String      |
| - Error                   | 이번에 삭제하지 못한 객체 정보 리스트 설명                               | ObjectArray |
| - - Key                   | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      |
| - - Code                  | 삭제 실패 오류 코드                                             | String      |
| - - Message               | 삭제 오류 정보                                                 | String      |


### 보관된 객체 복구

#### 기능 설명

POST Object restore 인터페이스는 아카이브 유형의 객체를 복구할 수 있습니다. 복구되어 읽을 수 있는 객체는 임시적인 것으로, 읽기 가능한 상태 및 해당 임시 사본을 삭제하는 기한을 설정할 수 있습니다. Days 매개변수를 이용해 임시 객체의 만료 기한을 지정할 수 있으며, 기한이 지나고 복사, 연장 등의 작업이 진행되지 않은 해당 임시 객체는 시스템에서 자동 삭제됩니다. 임시 객체는 아카이브 유형 객체의 사본이며, 보관된 원본 객체는 이 기간 내내 존재합니다.

#### 사용 예시

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,
    RestoreRequest: {
        Days: 1,
        CASJobParameters: {
            Tier: ’Expedited’
        }
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String | Yes    |
| Region             | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| RestoreRequest     | 복구 데이터의 컨테이너에 사용                                           | Object | Yes   |
| - Days             | 임시 사본의 만료 시간 설정                                       | Number | Yes   |
| - CASJobParameters | 아카이브 작업 매개변수의 컨테이너                                       | Object | Yes   |
| - - Tier           | 아카이브 유형의 데이터를 복구할 때 Tier는 COS가 지원하는 다음 3가지 복구 모드로 지정할 수 있습니다. <ul><li> Standard(표준 모드, 3 - 5시간 내에 복구 작업 완료)</li><li>Expedited(고속 모드, 15분 내에 복구 작업 완료)</li><li> Bulk(일괄 모드, 5 - 12시간 내에 복구 작업 완료)</li></ul>DEEP ARCHIVE 유형의 데이터 복구에는 다음 2가지 복구 모드가 있습니다. <ul><li> Standard(표준 모드, 12 - 24시간 내에 복구 작업 완료)</li><li>Bulk(일괄 모드, 24 - 48시간 내에 복구 작업 완료)</li></ul> | String | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |



## 멀티파트 작업

### 멀티파트 업로드 조회

#### 기능 설명

List Multiparts Uploads는 현재 진행 중인 멀티파트 업로드 정보를 조회하는 데 사용됩니다. 한 번에 최대 1000개의 현재 진행 중인 멀티파트 업로드를 나열합니다.

#### 사용 예시

접두사가 exampleobject인 미완료된 UploadId 리스트를 가져오는 예시는 다음과 같습니다.

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Prefix: ’exampleobject’,                        /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름         | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | 버킷의 이름. 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String | Yes   |
| Region         | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Prefix         | 객체 키의 접두사 매칭. 지정된 접두사를 포함한 객체 키만 한정하여 반환합니다. prefix를 사용하여 조회할 경우 반환되는 객체 키에 Prefix가 포함되므로 주의해야 합니다. | String | No   |
| Delimiter      | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용하며, 보통 `/`로 표시합니다. 모든 객체 키는 Prefix 또는 처음(Prefix 미지정 시)부터 첫 번째 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의하여, 모든 Common Prefix를 열거합니다. | String | No   |
| EncodingType   | 반환값의 인코딩 형식 규정. 유효한 값: url                            | String | No   |
| MaxUploads     | 반환하는 최대 항목 수 설정. 유효한 값 범위: 1 - 1000, 기본값: 1000         | String | No   |
| KeyMarker      | upload-id-marker와 함께 사용합니다.<br> <li> upload-id-marker가 지정되지 않은 경우 <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다.</br><li>upload-id-marker가 지정된 경우 <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거되고,</br>&emsp;- ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | String | No   |
| UploadIdMarker | key-marker와 함께 사용합니다.</br><li>key-marker가 지정되지 않은 경우 </br>&emsp;- upload-id-marker는 무시됩니다.</br><li>key-marker가 지정된 경우 <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거되고,</br>&emsp;- ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름               | 매개변수 설명                                                     | 유형        |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err                  | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode         | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers            | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                 | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode         | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers            | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Bucket             | 멀티파트 업로드의 타깃 버킷                                         | String      |
| - Encoding-Type      | 반환값의 인코딩 형식 규정. 유효한 값: url                            | String      |
| - KeyMarker          | 해당 key 값부터 시작하여 항목 열거                                      | String      |
| - UploadIdMarker     | 해당 UploadId 값부터 시작하여 항목 열거                                 | String      |
| - NextKeyMarker      | 반환 항목이 잘린 경우 반환된 NextKeyMarker가 다음 항목의 시작점이 됩니다. | String      |
| - NextUploadIdMarker                                         | 반환 항목이 잘린 경우 반환된 UploadId가 다음 항목의 시작점이 됩니다.     | String      |
| - MaxUploads         | 반환하는 최대 항목 수 설정. 유효한 값 범위: 1 - 1000               | String      |
| - IsTruncated        | 반환 항목의 잘림 여부. 'true' 또는 'false'                      | String      |
| - Prefix             | 객체 키의 접두사 매칭. 지정된 접두사를 포함한 객체 키만 한정하여 반환합니다.           | String      |
| - Delimiter      | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용하며, 보통 `/`로 표시합니다. 모든 객체 키는 Prefix 또는 처음(Prefix 미지정 시)부터 첫 번째 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의하여, 모든 Common Prefix를 열거합니다. | String      |
| - CommonPrefixs      | prefix부터 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의합니다. | ObjectArray |
| - - Prefix           | 구체적인 Common Prefixs 표시                                    | String      |
| - Upload             | 멀티파트 업로드의 정보 집합                                           | ObjectArray |
| - - Key              | 객체의 이름, 즉 객체 키                                         | String      |
| - - UploadId         | 이번 멀티파트 업로드의 ID 표시                                        | String      |
| - - StorageClass     | 멀티파트의 스토리지 유형을 표시하는 데 사용. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오. | String      |
| - - Initiator        | 이번에 업로드한 담당자 정보 표시                                 | Object      |
| - - - DisplayName    | 업로드 담당자 이름                                             | String      |
| - - - ID             | 업로드 담당자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - - Owner            | 멀티파트 소유자의 정보 표시                                     | Object      |
| - - - DisplayName    | 멀티파트 소유자의 이름                                             | String      |
| - - - ID             | 멀티파트 소유자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - - Initiated        | 멀티파트 업로드의 시작 시간                                           | String      |

### 멀티파트 업로드 초기화

#### 기능 설명

Initiate Multipart Uploads는 멀티파트 업로드 초기화를 요청합니다. 요청을 성공적으로 처리하면 Upload ID를 반환하고, 이는 다음 Upload Part 요청에 사용됩니다.

#### 사용 예시

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
}, function(err, data) {
    console.log(err || data);
    if (data) {
      uploadId = data.UploadId;
    }
});
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String | Yes    |
| Region             | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| CacheControl       | RFC 2616에 정의된 캐시 정책. 객체의 메타데이터로 저장됩니다.            | String | No   |
| ContentDisposition | RFC 2616에 정의된 파일 이름. 객체의 메타데이터로 저장됩니다.            | String | No   |
| ContentEncoding    | RFC 2616에 정의된 인코딩 형식. 객체의 메타데이터로 저장됩니다.            | String | No   |
| ContentType        | RFC 2616에 정의된 콘텐츠 유형(MIME). 객체의 메타데이터로 저장됩니다.    | String | No   |
| Expires            | RFC 2616에 정의된 만료 기간. 객체의 메타데이터로 저장됩니다. 만료 후에는 유효하지 않은 캐시가 되며, 파일은 삭제되지 않습니다.            | String | No   |
| ACL                | 객체의 액세스 제어 리스트(ACL) 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참고하십시오. <br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본 버킷 권한을 상속하십시오.** | String  | No   |
| GrantRead          | 권한 피부여자에게 객체 읽기 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code></br>예: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| GrantFullControl   | 권한 피부여자에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code></br>예: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| StorageClass       | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오. 기본값은 STANDARD입니다. | String | No   |
| x-cos-meta-\*       | 사용자 정의된 헤더 정보를 허용합니다. 객체의 메타데이터로 반환하며, 크기는 2KB로 제한됩니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| data     | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| Bucket   | 멀티파트 업로드의 타깃 버킷. 형식은 BucketName-APPID입니다. 예: examplebucket-1250000000 | String |
| Key      | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| UploadId | 후속 업로드에 사용되는 ID                                        | String |

### 멀티파트 업로드

#### 기능 설명

Upload Part 인터페이스 요청으로 초기화된 멀티파트 업로드를 실행합니다. 지원하는 파트 수: 1 - 10000개, 파트 크기: 1MB - 5GB.
<li>멀티파트 업로드를 초기화하려면, Initiate Multipart Upload 인터페이스로 멀티파트 업로드를 초기화한 후 uploadId를 획득합니다. 이 ID는 멀티파트 데이터의 고유 식별자일 뿐만 아니라 전체 파일에서 멀티파트 데이터의 상대적 위치를 식별합니다.</li>
<li>Upload Part를 요청할 때마다 partNumber와 uploadId가 필요합니다. partNumber는 파트의 번호로, 비순차 업로드를 지원합니다.</li>
<li>uploadId와 partNumber가 동일할 때, 나중에 전송되는 파트가 이전 파트를 덮어씁니다. uploadId가 존재하지 않을 경우 404 오류가 반환되며, 에러 코드는 NoSuchUpload입니다.</li>

#### 사용 예시

[//]: # (.cssg-snippet-upload-part)
```js
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.multipartUpload({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,       /* 필수 */
    ContentLength: '1024',
    UploadId: ’exampleUploadId’,
    PartNumber: ’1’,
    Body: fs.createReadStream(filePath)
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### 매개변수 설명

| 매개변수 이름        | 매개변수 설명                                                     | 유형             | 필수 입력 여부 |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket        | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String           | Yes   |
| Region        | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String           | Yes   |
| Key           | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String           | Yes   |
| ContentLength | RFC 2616에 정의된 HTTP 요청 콘텐츠 길이(바이트)                  | String           | Yes   |
| PartNumber    | 파트의 번호                                                   | String           | Yes   |
| UploadId      | 이번 멀티파트 업로드 작업의 번호                                       | String           | Yes   |
| Body          | 업로드한 파일의 멀티파트 콘텐츠. 문자열, File 객체 또는 Blob 객체가 될 수 있습니다.    | Stream/Buffer/String | Yes   |
| Expect        | RFC 2616에 정의된 HTTP 요청 콘텐츠의 길이(바이트). `Expect: 100-continue` 사용 시 서버의 확인을 받아야만 요청 콘텐츠를 발송할 수 있습니다. | String           | No   |
| ContentMD5    | RFC 1864에 정의된 Base64로 인코딩한 128-bit 콘텐츠 MD5 검증값. 이 헤더는 파일 콘텐츠의 변경 여부를 검증하는 데 사용됩니다. | String           | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |

### 멀티파트 복사

#### 기능 설명

Upload Part - Copy 인터페이스 요청으로 한 객체의 멀티파트 콘텐츠를 원본 경로에서 타깃 경로로 복사합니다.

> !객체 멀티파트 업로드 시에는 반드시 먼저 멀티파트 업로드를 초기화해야 합니다. 초기화된 멀티파트 업로드 응답에는 고유 디스크립터(upload ID)가 반환되며, 멀티파트 업로드 요청 시 이 ID가 반드시 수반되어야 합니다.

#### 사용 예시

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,       /* 필수 */
    CopySource: ’sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject’, /* 필수 */
    UploadId: ’exampleUploadId’,    /* 필수 */
    PartNumber: ’1’, /* 필수 */
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String | Yes   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| CopySource                  | 원본 객체 URL 경로입니다. URL 매개변수 ?versionId=&lt;versionId>를 통해 과거의 버전을 지정할 수 있습니다.  | String | Yes   |
| PartNumber                  | 멀티파트 복사한 파트 번호                                               | String | Yes   |
| UploadId                    | 파일 멀티파트 업로드 시에는 반드시 먼저 멀티파트 업로드를 초기화해야 합니다. 초기화된 멀티파트 업로드 응답에는 고유 디스크립터(upload ID)가 반환되며, 멀티파트 업로드 요청 시 이 ID가 반드시 수반되어야 합니다. | String | Yes   |
| CopySourceRange             | 원본 객체의 바이트 범위. 범위 값은 반드시 bytes=first-last 형식을 사용해야 합니다. first와 last는 0부터 시작하는 오프셋을 기반으로 합니다. 예를 들어 bytes=0-9는 원본 객체의 첫 10바이트 데이터를 복사한다는 의미입니다. 지정하지 않을 경우 객체 전체를 복사합니다. | String | No   |
| CopySourceIfMatch           | 객체의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Unmodified-Since와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | No   |
| CopySourceIfNoneMatch       | 객체의 Etag와 불일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Modified-Since와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | No   |
| CopySourceIfUnmodifiedSince | 객체가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Match와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | No   |
| CopySourceIfModifiedSince   | 객체가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-None-Match와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 요청 시 반환되는 헤더 정보                                           | Object |
| data           | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 요청 시 반환되는 헤더 정보                                           | Object |
| - ETag         | 파일의 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`) **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - LastModified | 반환된 객체의 마지막 수정 시간(GMT 형식)                               | String |

### 업로드된 파트 조회

#### 기능 설명

List Parts는 특정 멀티파트 업로드 중에서 이미 업로드된 파트를 조회하는 데 사용합니다. 즉, 지정 UploadId에서 이미 업로드에 성공한 모든 멀티파트를 나열합니다.

#### 사용 예시

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    UploadId: 'exampleUploadId', /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String | Yes   |
| Region           | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key               | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| UploadId         | 이번 멀티파트 업로드 ID 표시. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다. | String | Yes   |
| EncodingType     | 반환값의 인코딩 방식 규정                                         | String | No   |
| MaxParts         | 한 번에 반환하는 최대 항목 수. 기본값: 1000                           | String | No   |
| PartNumberMarker | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 marker부터 시작합니다.  | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                 | 매개변수 설명                                                     | 유형        |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err                    |요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode           | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers              | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                   | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode           | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers              | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Bucket               | 멀티파트 업로드의 타깃 버킷                                         | String      |
| - Encoding-type        | 반환값의 인코딩 방식 규정                                         | String      |
| - Key                  | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      |
| - UploadId             | 이번 멀티파트 업로드 ID 표시. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다.                                       | String      |
| - Initiator            | 이번 업로드 담당자 정보 표시                                 | Object      |
| - - DisplayName        | 업로드 담당자 이름                                             | String      |
| - - ID                 | 업로드 담당자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - Owner                | 해당 멀티파트 소유자 정보 표시                                 | Object      |
| - - DisplayName        | 버킷 소유자의 이름                                           | String      |
| - - ID                 | 버킷 소유자의 ID. 일반적으로 사용자의 UIN입니다.                            | String      |
| - StorageClass         | 멀티파트의 스토리지 레벨을 표시하는 데 사용. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오. | String      |
| - PartNumberMarker     | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 Marker부터 시작합니다.  | String      |
| - NextPartNumberMarker | 반환 항목이 잘린 경우 반환된 NextMarker가 다음 항목의 시작점이 됩니다.   | String      |
| - MaxParts             | 한 번에 반환하는 최대 항목 수                                       | String      |
| - IsTruncated          |반환 항목의 잘림 여부. 'true' 또는 'false'                      | String      |
| - Part                 | 멀티파트 정보 리스트                                                 | ObjectArray |
| - - PartNumber         | 파트의 번호                                                     | String      |
| - - LastModified       | 파트의 최종 수정 시간                                               | String      |
| - - ETag               | 파트의 MD5 알고리즘 검증값                                          | String      |
| - - Size               | 파트의 크기. 단위: Byte                                          | String      |

### 멀티파트 업로드 완료

#### 기능 설명

Complete Multipart Upload 인터페이스는 전체 멀티파트 업로드 완료를 요청합니다. Upload Parts를 사용해 모든 파트를 업로드한 후에는 반드시 해당 API를 호출하여 전체 파일의 멀티파트 업로드를 완료해야 합니다. 해당 API를 사용할 때에는 반드시 Body에서 모든 파트의 PartNumber와 ETag를 요청해 파트의 정확성을 검증해야 합니다.
멀티파트 업로드가 완료된 후에는 병합이 필요하며, 병합에는 몇 분 정도의 시간이 소요됩니다. 따라서 멀티파트 병합이 시작되면 COS에서 즉시 상태 코드 200을 반환하고, 병합 과정에서 주기적으로 빈 정보를 반환해 연결을 유지합니다. 병합이 완료될 때까지 COS는 Body에 병합된 파트의 콘텐츠를 반환합니다.

- 업로드된 파트가 1MB 미만인 경우 해당 API 호출 시 400 EntityTooSmall이 반환됩니다.
- 업로드된 파트의 번호가 불연속적인 경우 해당 API 호출 시 400 InvalidPart가 반환됩니다.
- 요청 Body에 있는 파트 정보를 오름차순으로 정렬하지 않은 경우 해당 API 호출 시 400 InvalidPartOrder가 반환됩니다.
- UploadId가 존재하지 않은 경우 해당 API 호출 시 404 NoSuchUpload가 반환됩니다.

> !업로드가 완료되었으나 중단되지 않은 멀티파트는 스토리지 용량을 차지하여 비용이 발생하므로, 즉시 멀티파트 업로드를 완료하거나 취소하는 것을 권장합니다.

#### 사용 예시

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    UploadId: ’exampleUploadId’,    /* 필수 */
    Parts: [
        {PartNumber: ’1’, ETag: ’exampleETag’},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket       | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String      | Yes   |
| Region       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String      | Yes   |
| Key          | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      | Yes   |
| UploadId     | 업로드 작업 번호                                                 | String      | Yes   |
| Parts        | 이번 멀티파트 업로드의 파트 정보 리스트 설명                           | ObjectArray | Yes   |
| - PartNumber | 멀티파트의 번호                                                   | String      | Yes   |
| - ETag       | 모든 파트 파일의 MD5 알고리즘 검증값<br>(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`). **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String      | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷                                         | String |
| - Key        | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| - ETag       | 병합 후 파일의 고유 ID. 형식: "uuid-<파트 수>"<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |

### 멀티파트 업로드 중지

#### 기능 설명

Abort Multipart Upload는 멀티파트 업로드 작업 중지 및 이미 업로드된 파트 삭제에 사용됩니다. Abort Multipart Upload 호출 시, 해당 UploadId를 사용해 파트 업로드를 요청한 경우 Upload Parts에서 실패를 반환합니다. 해당 UploadId가 존재하지 않을 경우 404 NoSuchUpload를 반환합니다.

> !업로드가 완료되었으나 중단되지 않은 멀티파트는 스토리지 용량을 차지하여 비용이 발생하므로, 즉시 멀티파트 업로드를 완료하거나 취소하는 것을 권장합니다.

#### 사용 예시

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,                           /* 필수 */
    UploadId: 'exampleUploadId'                       /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket   | 버킷 이름. 필수 형식: BucketName-APPID | String | Yes   |
| Region   | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key      | 객체 키(Object의 이름), 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| UploadId         | 이번 멀티파트 업로드 ID 표시. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다. | String | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |



## 고급 인터페이스(권장)

이러한 메소드는 상위 네이티브 메소드를 캡슐화한 것으로, 멀티파트 업로드/복사의 전 과정을 구현합니다. 동시 멀티파트 업로드/복사, 중단 지점부터 이어서 전송, 업로드 작업의 취소, 일시 중지 및 재시작 등을 지원합니다.

### 고급 업로드

#### 기능 설명

Upload File은 고급 업로드되며, SliceSize 매개변수를 통해서 파일 크기가 일정 수치(기본 1MB)를 초과할 경우 자동으로 멀티파트 업로드되고 그렇지 않으면 간편 업로드 되도록 제어할 수 있습니다.

#### 사용 예시

[//]: # (.cssg-snippet-transfer-upload-file)
```js
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.uploadFile({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,              /* 필수 */
    FilePath: filePath,                /* 필수 */
    SliceSize: 1024 * 1024 * 5,     /* 멀티파트 업로드의 임계값을 트리거하여, 5MB를 초과하면 멀티파트 업로드를 사용하도록 합니다. 옵션 */
    onTaskReady: function(taskId) {                   /* 옵션 */
        console.log(taskId);
    },
    onProgress: function (progressData) {           /* 옵션 */
        console.log(JSON.stringify(progressData));
    },
    onFileFinish: function (err, data, options) {
       console.log(options.Key + ’업로드’ + (err ? ’실패’ : ’완료’));
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형      | 필수 입력 여부 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket                                                       | 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String    | Yes   |
| Region                                                       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String    | Yes   |
| Key                                                          | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String    | Yes   |
| FilePath                                                         | 파일 업로드 경로                                                 | String | Yes   |
| SliceSize                                                    | 파일 크기가 일정 값 이상일 때 멀티파트 업로드 사용, 단위 Byte, 기본값 1048576(1MB), 해당 값보다 작거나 같은 경우 putObject를 통해 업로드, 해당 값보다 클 경우 sliceUploadFile를 통해 업로드                                                     | Number    | No   |
| AsyncLimit                                                   | 멀티파트 업로드의 동시 업로드 수량, 멀티파트 업로드 트리거 시에만 유효                                           | Number    | No   |
| StorageClass                                                 | 객체의 스토리지 유형. STANDARD, STANDARD_IA, ARCHIVE, DEEP_ARCHIVE 등과 같은 열거 값이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오.       | String    | No   |
| UploadAddMetaMd5                                             | 업로드 시 객체의 메타데이터 정보에 x-cos-meta-md5에 대입한 객체 콘텐츠의 MD5를 추가합니다. 형식은 32비트 소문자 알파벳 문자열입니다. 예: 4d00d79b6733c9cc066584a02ed03410 | String    | No   |
| onTaskReady                                                  | 업로드 작업 생성 시의 콜백 함수. 1개의 taskId를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function  | No   |
| - taskId                                                     | 업로드 작업의 번호                                               | String    | No   |
| onProgress                                                   | 파일 업로드 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다.      | Function  | No   |
| - progressData.loaded                                        | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number    | No   |
| - progressData.total                                         | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number    | No   |
| - progressData.speed                                         | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number    | No   |
| - progressData.percent                                       | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).       | Number    | No   |
| onFileFinish           | 모든 파일의 완료 또는 오류 콜백                                       | String    | Yes   |
| - err                  | 업로드 오류 정보                                               | Object    | No   |
| - data                 | 파일의 완료 정보                                               | Object    | No   |
| - options              | 현재 완료된 파일의 매개변수 정보                                       | Object    | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 업로드된 파일 액세스 주소                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷, 멀티파트 업로드 트리거 시에만 반환                                        | String |
| - Key        | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. 멀티파트 업로드 트리거 시에만 반환 | String |
| - ETag       | 병합 후 파일의 고유 ID. 형식: "uuid-<파트 수>"<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 객체 멀티파트 업로드

#### 기능 설명

Slice Upload File은 파일의 멀티파트 업로드에 사용되며, 대용량 파일 업로드에 적합합니다.

#### 사용 예시

[//]: # (.cssg-snippet-transfer-upload-file)
```js
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.sliceUploadFile({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    FilePath: filePath,                /* 필수 */
    onTaskReady: function(taskId) {                   /* 옵션 */
        console.log(taskId);
    },
    onHashProgress: function (progressData) {       /* 옵션 */
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) {           /* 옵션 */
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String   | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | Yes   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | Yes   |
| FilePath               | 파일 업로드 경로                                                 | String   | Yes   |
| SliceSize              | 멀티파트 크기                                                     | Number   | No   |
| AsyncLimit             | 멀티파트의 동시 전송량                                                 | Number   | No   |
| StorageClass           | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오.       | String   | No   |
| onTaskReady            | 업로드 작업 생성 시의 콜백 함수. 1개의 taskId를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function        | No   |
| - taskId               | 업로드 작업의 번호                                               | String   | No   |
| onHashProgress         | 파일의 MD5 값을 계산하는 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다. | Function | No   |
| - progressData.loaded  | 검증된 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일 검증 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일의 검증 백분율. 소수점으로 표시합니다(예: 검증 50%를 0.5로 표시).       | Number    | No   |
| onProgress             | 업로드 파일의 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다.      | Function | No   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).      | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷                                         | String |
| - Key        | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| - ETag       | 병합 후 파일의 고유 ID. 형식: "uuid-<파트 수>"<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 객체 복사

#### 기능 설명

Slice Copy File은 멀티파트 복사를 통해 원본 경로에서 타깃 경로로 파일을 복사하는 데 사용합니다. 복사 과정에서 객체 메타 속성과 ACL이 수정될 수 있습니다. 사용자는 해당 인터페이스를 통해 파일 이동, 파일 이름 변경, 파일 속성 수정 및 사본 생성을 할 수 있습니다.

#### 메소드 프로토타입

Slice Copy File을 호출하여 작업합니다.

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: ’examplebucket-1250000000’,                               /* 필수 */
    Region: 'COS_REGION',                                  /* 필수 */
    Key: ’exampleobject’,                                            /* 필수 */
    CopySource: ’sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject’, /* 필수 */
    onProgress:function (progressData) {                     /* 옵션 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String   | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | Yes   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | Yes   |
| CopySource             | 원본 객체의 URL 경로. URL 매개변수 ?versionId=&lt;versionId>를 통해 이전 버전을 지정할 수 있습니다. | String   | Yes   |
| ChunkSize              | 멀티파트 복사 시 파트 당 바이트 수. 기본값: 1048576(1MB)          | Number   | No   |
| SliceSize              | 파일 크기가 일정 값을 초과할 경우 멀티파트 복사를 사용합니다. 단위: Byte, 기본값: 5G. 해당 값 이하인 경우 putObjectCopy를 사용해 업로드하고, 초과하는 경우 sliceCopyFile을 사용해 업로드합니다. | Number   | No   |
| onProgress             | 업로드 파일의 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다.      | Function | No   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).      | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷                                         | String |
| - Key        | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| - ETag       | 병합 후 파일의 MD5 알고리즘 검증값<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 일괄 업로드

#### 기능 설명

방법1:
일괄 업로드는 putObject와 sliceUploadFile을 직접 여러 번 호출하여 일괄 업로드 효과를 구현할 수 있습니다. 인스턴스화 매개변수 FileParallelLimit을 통해 파일의 동시 전송 수를 제한합니다. 기본값은 3개입니다.

방법2:
cos.uploadFiles를 호출하여 일괄 업로드할 수 있습니다. 매개변수 SliceSize를 전송하여 파일 크기가 일정 값을 초과할 때 멀티파트 업로드를 사용하도록 제어할 수 있습니다. 다음은 uploadFiles 방법 설명입니다.

#### 메소드 프로토타입

uploadFiles를 호출하여 작업합니다.

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```js
const filePath1 = "temp-file-to-upload" // 로컬 파일 경로
const filePath2 = "temp-file-to-upload" // 로컬 파일 경로
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key: ’exampleobject’,
        FilePath: filePath1,
        onTaskReady: function(taskId) {
          /* taskId로 큐 작업을 통해 cos.cancelTask(taskId) 업로드 취소, cos.pauseTask(taskId) 업로드 중지, cos.restartTask(taskId), 업로드 재시작을 진행 할 수 있습니다. */
          console.log(taskId);
        }
    }, {
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key: '2.jpg',
        FilePath: filePath2,
        onTaskReady: function(taskId) {
          /* taskId로 큐 작업을 통해 cos.cancelTask(taskId) 업로드 취소, cos.pauseTask(taskId) 업로드 중지, cos.restartTask(taskId), 업로드 재시작을 진행 할 수 있습니다. */
          console.log(taskId);
        }
    }],
    SliceSize: 1024 * 1024 * 10,    /* 10MB 초과 시 멀티파트 업로드 설정 */
    onProgress: function (info) {
        var percent = parseInt(info.percent * 10000) / 100;
        var speed = parseInt(info.speed / 1024 / 1024 * 100) / 100;
        console.log(’진행률: ’ + percent + ’%; 속도: ’ + speed + ’Mb/s;’);
    },
    onFileFinish: function (err, data, options) {
        console.log(options.Key + ’업로드’ + (err ? ’실패’ : ’완료’));
    },
}, function (err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| files                  | 파일 리스트. 모든 항목은 putObject와 sliceUploadFile에 전송되는 매개변수 객체입니다. | Object    | Yes   |
| - Bucket               | 버킷의 이름. 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 이 형식을 따라야 합니다. | String    | Yes   |
| - Region               | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String    | Yes   |
| - Key                  | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String    | Yes   |
| - FilePath             | 파일 업로드 경로                                                 | String | Yes   |
| - onTaskReady                                                  | 업로드 작업 생성 시의 콜백 함수. 1개의 taskId를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function  | No   |
| -- taskId                                                     | 업로드 작업의 번호                                               | String    | No   |
| SliceSize              | 파일 크기가 일정 값 초과 시 멀티파트 업로드를 사용하도록 하는 매개변수(단위: Byte), 기본값1048576(1MB). 이 값 이하인 경우 putObject를 사용해 업로드하고, 초과하는 경우 sliceUploadFile을 사용해 업로드합니다. | Number | Yes   |
| onProgress             | 모든 작업의 진행률이 종합 계산된 업로드 진행률                            | String    | Yes   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number           | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number           | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number           | No   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).      | Number   | No   |
| onFileFinish           | 모든 파일의 완료 또는 오류 콜백                                       | String    | Yes   |
| - err                  | 업로드 오류 정보                                               | Object    | No   |
| - data                 | 파일의 완료 정보                                               | Object    | No   |
| - options              | 현재 완료된 파일의 매개변수 정보                                       | Object    | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형        |
| ------------ | ------------------------------------------------------------ | ----------- |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - files      | 모든 파일의 error 또는 data                                     | ObjectArray |
| - - error    | 업로드 오류 정보                                               | Object      |
| - - data     | 파일 완료 정보                                               | Object      |
| - - options  | 현재 완료된 파일의 매개변수 정보                                       | Object      |

### 멀티파트 다운로드


#### 기능 설명

멀티파트 다운로드 인터페이스, 멀티파트 동시 전송 다운로드를 지원합니다.

#### 메소드 프로토타입

멀티파트 다운로드 예시:

```js
var Key = 'test.zip';
cos.downloadFile({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing,
    Key: Key,
    FilePath: './' + Key, // 로컬 저장 경로
    ChunkSize: 1024 * 1024 * 8, // 멀티파트 크기
    ParallelLimit: 5, // 멀티파트 동시 전송 수
    RetryTimes: 3, // 멀티파트 실패 시 재시도 횟수
    onTaskReady: function (taskId) {
        console.log(taskId);
    },
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    },
}, function (err, data) {
    console.log(err || data);
});

// 다운로드 작업 취소
// cos.emit('inner-kill-task', {TaskId: '123'});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket               | 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String | Yes   |
| Region               | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                  | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| FilePath             | 다운로드 파일 저장 경로                                                 | String | Yes   |
| ChunkSize              | 다운로드 시 멀티파트 크기 | Nunber | No   |
| ParallelLimit              | 멀티파트 동시 전송 수 | Nunber | No   |
| RetryTimes              | 멀티파트 다운로드 실패 시 재시도 횟수 | Nunber | No   |
| onProgress             | 다운로드 진행률                          | String | No   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number           | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number           | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number           | No   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).      | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형        |
| ------------ | ------------------------------------------------------------ | ----------- |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                  | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 304, 403, 404 등)             | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| - CacheControl        | RFC 2616에 정의된 캐시 명령어. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - ContentDisposition  | RFC 2616에 정의된 파일 이름. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - ContentEncoding     | RFC 2616에 정의된 인코딩 형식. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - Expires             | RFC 2616에 정의된 캐시 만료 시간. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다.  | String  |
| - x-cos-storage-class | 객체의 스토리지 레벨. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE가 있습니다. <br>**해당 헤더가 반환되지 않으면 CFS 레벨이 STANDARD(표준 스토리지)라는 의미입니다.** | String  |
| - x-cos-meta-*        | 사용자 정의된 메타데이터                                           | String  |
| - NotModified         | 요청 시 IfModifiedSince가 있을 경우 해당 속성을 반환합니다. 파일이 수정되지 않은 경우 true, 수정된 경우 false입니다. | Boolean |
| - ETag                | 파일의 MD5 알고리즘 검증값 반환. ETag 값은 업로드 과정에서 객체 손상 여부를 검사하는 데 사용할 수 있습니다.<br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다.** | String  |
| - VersionId           | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String  |

### 큐 업로드

Node.js SDK에서 putObject와 sliceUploadFile을 대상으로 한 업로드 작업에는 기록 큐가 있습니다. 큐 관련 방법은 다음과 같습니다.

1. cos.getTaskList로 작업 리스트를 가져올 수 있습니다.
2. cos.pauseTask, cos.restartTask, cos.cancelTask로 작업을 진행합니다.
3. cos.on(’list-update’, callback);으로 리스트와 진행률 변화를 수신할 수 있습니다.

전체적인 큐 사용 예시는 [demo-queue](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue)를 참고하십시오.

#### 업로드 작업 취소

taskId에 따라 업로드 작업을 취소합니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = ’xxxxx’;                   /* 필수 */
cos.cancelTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. sliceUploadFile 메소드를 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | Yes   |

#### 업로드 작업 일시 중지

taskId에 따라 업로드 작업을 일시 중지합니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = ’xxxxx’;                   /* 필수 */
cos.pauseTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. sliceUploadFile 메소드를 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | Yes   |

#### 업로드 작업 재시작

taskId에 따라 업로드 작업을 재시작합니다. 사용자가 수동으로 중단(pauseTask를 호출하여 중단)하거나 오류로 중단된 업로드 작업을 재시작하는 데 사용할 수 있습니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = ’xxxxx’;                   /* 필수 */
cos.restartTask(taskId);
```

**매개변수 설명**

<table>
	<tr><th>매개변수 이름</th><th>매개변수 설명</th><th>유형</th><th>필수 입력 여부</th></tr>
	<tr><td>taskId</td><td>파일 업로드 작업 번호. sliceUploadFile 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다.</td><td>String</td><td>Yes</td></tr>
</table>
