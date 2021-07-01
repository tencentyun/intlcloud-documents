## 소개

본 문서는 간단한 객체 작업, 기타 작업과 관련된 API 개요 및 SDK 예시 코드에 대해 설명하며, 예시를 통해 사용 방법을 제시합니다.

**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                 |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷의 일부 또는 모든 객체 조회           |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간편한 객체 업로드   | 버킷에 객체 업로드                     |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 폼을 사용한 객체 업로드   | 폼을 사용한 객체 업로드 요청                     |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체의 메타데이터 정보 조회                  |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 하나의 객체를 다운로드                             |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | 크로스 도메인 설정 사전 요청 | 사전 요청을 통해 실제 크로스 도메인 요청의 발송 가능 여부 확인 |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사       | 객체를 타깃 경로에 복사(객체 키)             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제 | 버킷에서 지정 객체 삭제                   |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | 버킷에서 객체 일괄 삭제                   |

**기타 작업**

| API                                                          | 작업명       | 작업 설명                           |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스           |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정| 버킷의 특정 객체의 액세스 제어 리스트 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회             |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 사용 예시

예시1: 디렉터리 a의 모든 파일을 나열합니다.

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',     /* 필수 */
    Prefix: 'a/',           /* 옵션 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

반환값 포맷:

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
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Prefix: 'a/',              /* 옵션 */
    Delimiter: '/',            /* 옵션 */
}, function(err, data) {
    console.log(err || data.CommonPrefixes);
});
```

반환값 포맷:

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
var bucket = 'examplebucket-1250000000';
var region = 'ap-beijing';
var prefix = 'examplefolder/';  /* 삭제할 디렉터리 또는 접두사 */
var listFolder = function(marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function(err, data) {
        if (err) {
            return console.log('list error:', err);
        } else {
            console.log('list result:', data.Contents);
            if (data.IsTruncated === 'true') listFolder(data.NextMarker);
            else return console.log('list complete');
        }
    });
};
listFolder();
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예    |
| Region       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Prefix       | 객체 키의 접두사 매칭. 지정된 접두사를 포함한 객체 키만 한정하여 반환합니다.             | String | 아니요   |
| Delimiter    | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용하며, 보통 `/`로 표시합니다. 모든 객체 키는 Prefix 또는 처음(Prefix 미지정 시)부터 첫 번째 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의하여, 모든 Common Prefix를 열거합니다. | String | 아니요   |
| Marker       | 시작하는 객체 키를 표시. 해당 표기 다음부터(해당 표기 불포함) UTF-8 사전 순서에 따라 객체 키 항목을 반환합니다. | String | 아니요   |
| MaxKeys      | 한 번에 반환하는 최대 항목 수. 기본값은 1000이며, 최대값은 1000입니다.                 | String | 아니요   |
| EncodingType | 반환값의 인코딩 방식 규정. 옵션값: url. 반환된 객체 키가 URL 인코딩(퍼센트 인코딩)된 후의 값을 의미합니다. 예를 들어, 'Tencent Cloud'는 `%E8%85%BE%E8%AE%AF%E4%BA%91`로 인코딩됩니다. | String | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| data              | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - Name            | 버킷 이름. 포맷은 BucketName-APPID입니다. 예: examplebucket-1250000000 | String      |
| - Prefix          | 객체 키 접두사 매칭. 해당 표기 다음부터(해당 표기 불포함) UTF-8 사전 순서에 따라 객체 키 항목을 반환합니다. | String      |
| - Marker          | 시작하는 객체 키를 표시. 해당 표기 다음부터(해당 표기 불포함) UTF-8 사전 순서에 따라 객체 키 항목을 반환합니다. | String      |
| - MaxKeys         | 단일 응답 요청에 반환되는 결과의 최대 항목 수                       | String      |
| - Delimiter       | 구분 문자                                                     | String      |
| - IsTruncated     | 응답 요청 항목이 잘렸는지 여부. 값: 'true' 또는 'false'             | String      |
| - NextMarker      | 반환 항목이 잘린 경우 NextMarker를 반환하며, 다음 항목의 시작점을 표시합니다.   | String      |
| - CommonPrefixes  | Prefix부터 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의합니다. | ObjectArray |
| - - Prefix        | 단일 Common Prefix의 접두사                                   | String      |
| - EncodingType    | 반환값의 인코딩 방식. Delimiter, Marker, Prefix, NextMarker, Key에 적용됩니다. | String      |
| - Contents        | 객체 메타데이터 정보 리스트                                           | ObjectArray |
| - - Key           | 객체 키. 즉 객체의 이름                                         | String      |
| - - ETag          | 객체 콘텐츠에 따라 계산된 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`) **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String      |
| - - Size          | 객체의 크기. 단위: Byte                                          | String      |
| - - LastModified  | ISO8601 포맷의 객체 최종 수정 시간. 예: 2019-05-24T10:56:40Z    | String      |
| - - Owner         | 객체 소유자 정보                                               | Object      |
| - - - ID          | 객체 소유자의 전체 ID. 포맷은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`입니다. 예: `qcs::cam::uin/100000000001:uin/100000000001`, 여기에서 100000000001이 uin입니다. | String      |
| - - - DisplayName | 객체 소유자 이름                                             | String      |
| - - StorageClass  | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 자세한 내용은 [스토리지 유형](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참조하십시오. | String      |

### 간편한 객체 업로드

#### 기능 설명

PUT Object 인터페이스로 단일 객체를 지정 버킷에 업로드할 수 있습니다. 이 작업을 위해 요청자가 버킷에 대한 쓰기 권한을 가지고 있어야 합니다.

> !
> 1. Key(파일명)는 `/`로 끝날 수 없습니다. 그렇지 않으면 폴더로 인식될 수 있습니다.
> 2. 루트 계정(동일한 APPID)당 버킷의 ACL 규칙 수량은 최대 1000개이며, 객체 ACL 규칙 수량은 제한이 없습니다. 객체 ACL 제어가 필요하지 않을 경우 업로드 시 설정하지 마십시오. 기본 버킷 권한이 상속됩니다.
> 3. 업로드 후, 동일한 Key로 사전 서명된 링크를 생성할 수 있습니다. 다운로드 시 method를 GET으로 지정하십시오. 자세한 인터페이스 설명은 아래에 나와 있으며, 다른 단말기로 공유하여 다운로드할 수 있습니다. 주의: 파일이 개인 읽기 권한인 경우 사전 서명 링크에 유효기간이 있습니다.

#### 사용 예시

문자열을 파일 콘텐츠로 업로드합니다.

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

디렉터리를 생성합니다.

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'a/',              /* 필수 */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String   | 예    |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String   | 예   |
| Key                    | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String   | 예   |
| Body                   | 생성 파일의 텍스트 콘텐츠. 문자열일 수 있습니다.                           | String   | 예   |
| CacheControl           | RFC 2616에 정의된 캐시 정책. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| ContentDisposition     | RFC 2616에 정의된 파일 이름. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| ContentEncoding        | RFC 2616에 정의된 인코딩 포맷. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| ContentLength          | RFC 2616에 정의된 HTTP 요청 콘텐츠 길이(바이트)                   | String   | 아니요   |
| ContentType            | RFC 2616에 정의된 콘텐츠 유형(MIME). 객체의 메타데이터로 저장됩니다.    | String   | 아니요   |
| Expires                | RFC 2616에 정의된 만료 시간. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| Expect                 | Expect: 100-continue 사용 시 서버의 확인을 받아야만 요청 콘텐츠를 발송할 수 있습니다. | String   | 아니요   |
| ACL                    | 객체의 액세스 제어 리스트(ACL) 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오.<br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본 버킷 권한을 상속하십시오.** | String   | 아니요   |
| GrantRead              | 권한을 부여받은 대상에게 객체를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | 아니요   |
| GrantReadAcp           | 권한을 부여받은 대상에게 객체의 액세스 제어 리스트(ACL)를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다.<br/><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | 아니요   |
| GrantWriteAcp          | 권한을 부여받은 대상에게 객체의 액세스 제어 리스트(ACL)를 쓸 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | 아니요   |
| GrantFullControl       | 권한을 부여받은 대상에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다.<br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | 아니요   |
| StorageClass           | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 기본값은 STANDARD입니다. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오. | String   | 아니요   |
| x-cos-meta-*           | 사용자 정의된 헤더 정보 허용. 객체의 메타데이터로 저장하며, 크기는 2KB로 제한됩니다. | String               | 아니요   |
| onTaskReady            | 업로드 작업 생성 시의 콜백 함수. taskId 하나를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function | 아니요   |
| - taskId               | 업로드 작업의 번호                                               | String   | 아니요   |
| onProgress             | 진행률 콜백 함수. 진행률 콜백 응답 객체(progressData)의 속성은 다음과 같습니다.   | Function | 아니요   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | 아니요   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number               | 아니요   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number               | 아니요   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다 예: 업로드 50%를 0.5로 표시       | Number   | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| - ETag                | 파일의 MD5 알고리즘 검증값 반환. ETag 값은 업로드 과정에서 객체 손상 여부를 검사하는 데 사용할 수 있습니다.<br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다.** | String  |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 폼을 사용한 객체 업로드

POST Object 인터페이스 요청을 통해 사용자 wx.chooseImage가 선택한 파일 객체(Object)를 지정 버킷에 업로드할 수 있습니다. 이 작업은 요청자가 버킷에 대해 쓰기 권한을 가지고 있어야 합니다.

>! onProgress 진행률 피드백은 미니프로그램 [UploadTask.onProgressUpdate](https://developers.weixin.qq.com/miniprogram/dev/api/network/upload/UploadTask.onProgressUpdate.html)에 종속됩니다. 일부 안드로이드 모델은 진행률이 정확하지 않은 문제가 발생할 수 있습니다.

#### 사용 예시

간편한 파일 업로드

[//]: # (.cssg-snippet-post-object)
```js
cos.postObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
    FilePath: tmpFilePath, // wx.chooseImage 파일을 선택해 획득한 tmpFilePath
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function (err, data) {
    console.log(err || data);
});
```

지정 디렉터리에 파일을 업로드합니다.

```js
var folder = 'examplefolder/';
cos.postObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: folder + filename,              /* 필수 */
    FilePath: tmpFilePath, // wx.chooseImage 파일을 선택해 획득한 tmpFilePath
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String   | 예    |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String   | 예   |
| Key                    | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String   | 예   |
| ContentLength          | RFC 2616에 정의된 HTTP 요청 콘텐츠 길이(바이트)                   | String   | 예   |
| CacheControl           | RFC 2616에 정의된 캐시 정책. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| ContentDisposition     | RFC 2616에 정의된 파일 이름. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| ContentEncoding        | RFC 2616에 정의된 인코딩 포맷. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| ContentType            | RFC 2616에 정의된 콘텐츠 유형(MIME). 객체의 메타데이터로 저장됩니다.    | String   | 아니요   |
| Expires                | RFC 2616에 정의된 만료 시간. 객체의 메타데이터로 저장됩니다.            | String   | 아니요   |
| Expect                 | Expect: 100-continue 사용 시 서버의 확인을 받아야만 요청 콘텐츠를 발송할 수 있습니다. | String   | 아니요   |
| ACL                    | 객체의 액세스 제어 리스트(ACL) 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오.<br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본 버킷 권한을 상속하십시오.** | String   | 아니요   |
| StorageClass           | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 기본값은 STANDARD입니다. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오. | String   | 아니요   |
| x-cos-meta-*           | 사용자 정의된 헤더 정보 허용. 객체의 메타데이터로 저장하며, 크기는 2KB로 제한됩니다. | String   | 아니요   |
| FilePath               | 파일 업로드의 임시 파일 경로. wx.chooseImage 방법을 통해 얻을 수 있습니다.   | String   | 예   |
| onProgress             | 진행률 콜백 함수. 호출 시 첫 매개변수는 processData 객체입니다.         | Function | 아니요   |
| - progressData.loaded  | 다운로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | 아니요   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number               | 아니요   |
| - progressData.speed   | 파일의 다운로드 속도. 단위: 바이트/초(Bytes/s)                   | Number               | 아니요   |
| - progressData.percent | 파일의 다운로드 백분율. 소수점으로 표시합니다. 예: 다운로드 50%를 0.5로 표시       | Number   | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| - ETag       | 객체의 MD5 알고리즘 검증값 반환. ETag 값은 업로드 과정에서 Object 손상 여부를 검사하는 데 사용할 수 있습니다.<br>**주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다. 예: `"09cba091df696af91549de27b8e7d0f6"`**  | String |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성 반환                                       | String |
| - VersionId  | 버전 제어가 활성화된 버킷에서 객체의 버전 ID를 반환합니다.                  | String |

### 객체 메타데이터 조회

#### 기능 설명

객체의 메타데이터 정보를 조회합니다.

#### 사용 예시

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',               /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예   |
| Region          | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key             | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| IfModifiedSince | 객체가 지정된 시간 이후에 수정되는 경우 해당 객체의 메타데이터 정보를 반환하며, 그렇지 않을 경우 304를 반환합니다. | String | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   |요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                  | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 304 등). 지정 시간이 지난 후 수정되지 않은 경우 304를 반환합니다. | Number |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| - x-cos-object-type   | 객체의 추가 업로드 가능 여부 표시. 열거 값은 normal, appendable이 있으며, 기본값은 normal로 반환에 표시되지 않습니다. | String  |
| - x-cos-storage-class | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE가 있으며 기본값 STANDARD는 반환 중에는 표시되지 않습니다. 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오. | String  |
| - x-cos-meta-*        | 사용자 정의된 meta                                            | String  |
| - NotModified         | 지정 시간 이후 객체의 수정 여부                                 | Boolean |
| - ETag                | 파일의 MD5 알고리즘 검증값 반환. ETag 값은 업로드 과정에서 객체 손상 여부를 검사하는 데 사용할 수 있습니다.<br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다.** | String  |
| - VersionId           | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 객체 다운로드

GET Object 인터페이스 요청을 통해 버킷에 있는 지정 파일의 콘텐츠를 획득할 수 있습니다. 획득하는 파일 콘텐츠는 문자열 포맷입니다.

#### 사용 예시

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Range를 지정하여 파일 콘텐츠를 가져옵니다.

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    Range: 'bytes=1-3',        /* 옵션 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                     | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String   | 예    |
| Region                     | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String   | 예   |
| Key                        | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String   | 예   |
| ResponseContentType        | 응답 헤더의 Content-Type 매개변수 설정                           | String   | 아니요   |
| ResponseContentLanguage    | 반환 헤더의 Content-Language 매개변수 설정                       | String   | 아니요   |
| ResponseExpires            | 반환 헤더의 Content-Expires 매개변수 설정                       | String   | 아니요   |
| ResponseCacheControl       | 반환 헤더의 Cache-Control 매개변수 설정                          | String   | 아니요   |
| ResponseContentDisposition | 반환 헤더의 Content-Disposition 매개변수 설정                    | String   | 아니요   |
| ResponseContentEncoding    | 반환 헤더의 Content-Encoding 매개변수 설정                       | String   | 아니요   |
| Range                      | RFC 2616에 정의된 바이트 범위. 범위 값은 반드시 bytes=first-last 포맷을 사용해야 합니다. first와 last는 0부터 시작하는 오프셋을 기반으로 합니다. 예를 들어 bytes=0-9는 객체의 첫 10바이트 데이터를 다운로드한다는 의미입니다. 지정하지 않을 경우 객체 전체를 다운로드합니다. | String   | 아니요   |
| IfModifiedSince            | 객체가 지정된 시간 이후에 수정되는 경우 해당 객체의 메타데이터 정보를 반환하며, 그렇지 않을 경우 304(not modified)를 반환합니다. | String   | 아니요   |
| IfUnmodifiedSince            | 객체가 지정된 시간 이후에 수정되지 않을 경우 객체를 반환하며, 그렇지 않을 경우 412(precondition failed)를 반환합니다. | String   | 아니요   |
| IfMatch                    | ETag가 지정된 콘텐츠와 일치해야 객체를 반환하며, 그렇지 않을 경우 412(precondition failed)를 반환합니다. | String   | 아니요   |
| IfNoneMatch                | ETag가 지정된 콘텐츠와 불일치해야 객체를 반환하며, 그렇지 않을 경우 304(not modified)를 반환합니다.  | String   | 아니요   |
| VersionId                  | 다운로드할 객체의 버전 ID 지정                                    | String   | 아니요   |
| onProgress                 | 진행률 콜백 함수. 진행률 콜백 응답 객체(progressData)의 속성은 다음과 같습니다.   | Function | 아니요   |
| - progressData.loaded      | 다운로드한 객체의 일부 크기. 단위: 바이트(Bytes)                | Number   | 아니요   |
| - progressData.total       | 객체의 전체 크기. 단위: 바이트(Bytes)                        | Number   | 아니요   |
| - progressData.speed       | 객체의 다운로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | 아니요   |
| - progressData.percent     | 객체의 다운로드 백분율. 소수점으로 표시합니다. 예: 다운로드 50%를 0.5로 표시       | Number   | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   |요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                  | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 304, 403, 404 등)             | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| - CacheControl        | RFC 2616에 정의된 캐시 명령어. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - ContentDisposition  | RFC 2616에 정의된 파일 이름. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - ContentEncoding     | RFC 2616에 정의된 인코딩 포맷. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다. | String  |
| - Expires             | RFC 2616에 정의된 캐시 만료 시간. 객체 메타데이터에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때만 해당 헤더를 반환합니다.  | String  |
| - x-cos-storage-class | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE가 있습니다.<br>**주의: 해당 헤더가 반환되지 않으면 CFS 유형이 STANDARD(표준 스토리지)라는 의미입니다. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오.** | String  |
| - x-cos-meta-*        | 사용자 정의된 메타데이터                                           | String  |
| - NotModified         | 요청 시 IfModifiedSince가 있을 경우 해당 속성을 반환합니다. 파일이 수정되지 않은 경우 true, 수정된 경우 false입니다. | Boolean |
| - ETag                | 파일의 MD5 알고리즘 검증값 반환. ETag 값은 업로드 과정에서 객체 손상 여부를 검사하는 데 사용할 수 있습니다.<br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 앞뒤에 큰따옴표가 사용됩니다.** | String  |
| - VersionId           | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |
| - Body                | 반환되는 파일 콘텐츠. 기본값은 String 포맷                           | String  |

### 크로스 도메인 설정 사전 요청

#### 기능 설명

OPTIONS Object 인터페이스는 객체에 대한 크로스 도메인 액세스 설정을 사전 요청합니다. 즉, 크로스 도메인 요청 발송 전 OPTIONS 요청과 특정 출처, HTTP 방법, 헤더 정보 등을 COS에 보내 실제 크로스 도메인 요청 가능 여부를 결정합니다. CORS 설정이 존재하지 않을 경우 요청에 대해 403 Forbidden이 반환됩니다. **사용자는 PUT Bucket cors 인터페이스를 통해 버킷의 CORS 지원을 활성화할 수 있습니다.**

#### 사용 예시

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    Origin: 'https://www.qq.com',      /* 필수 */
    AccessControlRequestMethod: 'PUT', /* 필수 */
    AccessControlRequestHeaders: 'origin,accept,content-type' /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| Origin                      | 크로스 도메인 액세스 시뮬레이션을 요청하는 원본 도메인                                   | String | 예   |
| AccessControlRequestMethod  | 크로스 도메인 액세스 시뮬레이션을 요청하는 HTTP 방법                                 | String | 예   |
| AccessControlRequestHeaders | 크로스 도메인 액세스 시뮬레이션을 요청하는 헤더                                       | String | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형    |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object  |
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
사용자는 해당 인터페이스를 통해 사본 생성, 객체 메타데이터 수정(원본 객체와 타깃 파일의 속성은 동일), 객체의 이동과 이름 변경(복사 후 단독으로 호출하여 인터페이스 삭제)이 가능합니다.

> !객체의 크기는 1MB~5GB를 권장합니다. 5GB가 넘는 객체는 고급 인터페이스 객체 복사 [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12)을 사용하십시오.



#### 사용 예시

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000',                               /* 필수 */
    Region: 'ap-beijing',                                  /* 필수 */
    Key: 'picture.jpg',                                            /* 필수 */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.jpg', /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| CopySource                  | 원본 객체의 URL 경로. URL 매개변수 ?versionId=&lt;versionId>를 통해 이전 버전을 지정할 수 있습니다.  | String | 예   |
| ACL                         | 객체의 액세스 제어 리스트(ACL) 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오.<br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본 버킷 권한을 상속하십시오.** | String | 아니요   |
| GrantRead                   | 권한을 부여받은 대상에게 객체를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니요   |
| GrantWrite                  | 권한을 부여받은 대상에게 객체를 쓸 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니요   |
| GrantFullControl            | 권한을 부여받은 대상에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다.<br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니요   |
| MetadataDirective           | 메타데이터 복사 여부. 열거 값은 Copy, Replaced이며, 기본값은 Copy입니다. Copy로 표기되어 있다면 Header의 사용자 메타데이터 정보를 무시하고 바로 복사합니다. Replaced로 표기되어 있다면 Header 정보에 따라 메타데이터를 수정합니다. **타깃 경로와 원본 경로가 일치할 때, 즉 사용자가 메타데이터를 수정하려고 할 때는 반드시 Replaced로 표기되어 있어야 합니다.** | String | 아니요   |
| CopySourceIfModifiedSince   | 객체가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfNoneMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | 아니요   |
| CopySourceIfUnmodifiedSince | 객체가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.**| String | 아니요   |
| CopySourceIfMatch           | 객체의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfUnmodifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | 아니요   |
| CopySourceIfNoneMatch       | 객체의 Etag와 불일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfModifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | 아니요   |
| StorageClass           | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA 등이 있으며, 기본값은 STANDARD입니다. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오. | String   | 아니요   |
| x-cos-meta-*                | 기타 사용자 정의된 파일 헤더                                         | String | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object  |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 요청 시 반환되는 헤더 정보                                           | Object |
| data           | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 요청 시 반환되는 헤더 정보                                           | Object |
| - ETag         | 파일의 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`) **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String      |
| - LastModified | 객체의 최종 수정 시간 반환. 예: 2017-06-23T12:33:27.000Z         | String |
| - VersionId    | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 단일 객체 삭제

#### 기능 설명

DELETE Object 인터페이스 요청을 통해 COS 버킷에서 단일 객체(Object) 삭제할 수 있습니다. 이 작업은 요청자가 버킷에 대한 WRITE 권한을 가지고 있어야 합니다.

#### 사용 예시

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',                                            /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket    | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예   |
| Region    | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key       | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| VersionId | 삭제할 객체 버전 ID 또는 DeleteMarker 버전 ID                  | String | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등). **삭제에 성공하거나 파일이 존재하지 않을 경우 204 또는 200이 반환되고, 지정 Bucket을 찾지 못할 경우 404가 반환됩니다.** | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |

### 다수의 객체 삭제

#### 기능 설명

DELETE Multiple Objects 인터페이스 요청을 통해 지정된 버킷에서 객체 일괄 삭제할 수 있습니다. 한 번에 최대 1000개의 객체를 삭제합니다. COS는 응답 결과를 Verbose와 Quiet의 두 가지 모드로 제공합니다. Verbose 모드는 모든 객체의 삭제 결과를 반환하고, Quiet 모드는 오류가 보고된 객체 정보만 반환합니다.

#### 사용 예시

다수의 파일을 삭제합니다.

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Objects: [
        key = "picture.jpg";
        {Key: '2.zip'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

접두사에 따라 다수의 객체를 삭제합니다(지정 디렉터리의 파일 삭제).

```js
var bucket: 'examplebucket-1250000000'; /* 필수 */
var region: 'ap-beijing';     /* 버킷이 위치한 리전. 필수 필드 */
var prefix = 'examplefolder/';  /* 삭제할 디렉터리 또는 접두사 */
var deleteFolder = function (marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function (listError, listResult) {
        if (listError) return console.log('list error:', listError);
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
                console.log('delete error', delError);
                console.log('delete stop');
            } else {
                console.log('delete result', deleteResult);
                if (listResult.IsTruncated === 'true') deleteFolder(nextMarker);
                else console.log('delete complete');
            }
        });
    });
}
deleteFolder();
```

#### 매개변수 설명

| 매개변수 이름      | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket      | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String      | 예   |
| Region      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String      | 예   |
| Quiet       | Boolean 값. 이 값은 Quiet 모드의 실행 여부를 결정합니다. true 값이면 Quiet 모드를 실행하고, false 값이면 Verbose 모드를 실행합니다. 기본값: false | Boolean     | 아니요   |
| Objects     | 삭제할 객체 리스트                                             | ObjectArray | 예   |
| - Key       | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      | 예   |
| - VersionId | 삭제할 객체 버전 ID 또는 DeleteMarker 버전 ID                  | String      | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err                       | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode              | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등)             | Number      |
| - headers                 | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                      | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode              | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등)             | Number      |
| - headers                 | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Deleted                 | 이번에 삭제된 객체 정보 리스트를 설명                               | ObjectArray |
| - - Key                   | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - - VersionId             | 매개변수에 VersionId를 전송하면 반환 시에도 VersionId가 수반됩니다. 방금 작업한 객체 버전 또는 DeleteMarker 버전을 표시합니다. | String      |
| - - DeleteMarker          | 버전 제어를 활성화한 상태에서 매개변수에 VersionId가 없으면 이번에는 파일 콘텐츠를 제거하지 않고 DeleteMarker만 하나 추가합니다. 이는 볼 수 있던 파일이 삭제되었다는 의미이며, 열거 값은 true와 false입니다. | String      |
| - - DeleteMarkerVersionId | 반환된 DeleteMarker가 true인 경우, 새로 추가된 DeleteMarker의 VersionId를 반환합니다. | String      |
| - Error                   | 이번에 삭제하지 못한 객체 정보 리스트 설명                               | ObjectArray |
| - - Key                   | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - - Code                  | 삭제 실패 에러 코드                                             | String      |
| - - Message               | 삭제 오류 정보                                                 | String      |

## 기타 작업

### 보관된 객체 복구

#### 기능 설명

POST Object restore 인터페이스는 아카이브 유형의 객체를 복구할 수 있습니다. 복구되어 읽을 수 있는 객체는 임시적인 것으로, 읽기 가능한 상태 및 해당 임시 사본을 삭제하는 기한을 설정할 수 있습니다. Days 매개변수를 이용해 임시 객체의 만료 기한을 지정할 수 있으며, 기한이 지나고 복사, 연장 등의 작업이 진행되지 않은 해당 임시 객체는 시스템에서 자동 삭제됩니다. 임시 객체는 아카이브 유형 객체의 사본이며, 보관된 원본 객체는 이 기간 내내 존재합니다.

#### 사용 예시

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',
    RestoreRequest: {
        Days: 1,
        CASJobParameters: {
            Tier: 'Expedited'
        }
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예    |
| Region             | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key                | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| RestoreRequest     | 복구 데이터의 컨테이너에 사용                                           | Object | 예   |
| - Days             | 임시 사본의 만료 시간 설정                                       | Number | 예   |
| - CASJobParameters | CAS 작업 매개변수의 컨테이너                                       | Object | 예   |
| - - Tier           | CAS 유형의 데이터를 복구할 때 Tier는 Standard(표준 모드, 3~5시간 내에 복구 작업 완료), Expedited(고속 모드, 15분 내에 복구 작업 완료), Bulk(일괄 모드, 5~12시간 내에 복구 작업 완료)와 같이 COS가 지원하는 3가지 복구 모드를 지정할 수 있습니다. DEEP ARCHIVE 유형의 데이터를 복구할 때 Tier는 Standard(표준 모드, 12~24시간 내에 복구 작업 완료), Bulk(일괄 모드, 24~48시간 내에 복구 작업 완료)와 같이 2가지 복구 모드를 지정할 수 있습니다. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |

### 객체 ACL 설정

#### 기능 설명

PUT Object acl 인터페이스는 특정 버킷에서 한 객체의 액세스 제어 리스트(ACL)를 설정할 때 사용합니다.

> !루트 계정(동일한 APPID)당 버킷의 ACL, Policy 및 CAM 관련 정책은 최대 1000개까지 설정할 수 있으며, 객체 액세스 제어 리스트(ACL) 규칙은 수량 제한이 없습니다. 객체 액세스 제어 리스트(ACL) 제어가 필요하지 않을 경우 설정하지 마십시오. 기본 버킷 권한을 상속합니다.

#### 사용 예시

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    ACL: 'public-read',        /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

특정 사용자에게 객체의 모든 권한을 부여합니다.

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    GrantFullControl: 'id="100000000001"' // 100000000001: 루트 계정 uin
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicy를 통해 객체의 쓰기 권한을 부여합니다.

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy에는 반드시 owner가 있음
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001은 Bucket이 속한 사용자의 QQ 번호
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011은 QQ 번호
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String      | 예    |
| Region              | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String      | 예   |
| Key                 | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      | 예   |
| ACL                 | 객체의 액세스 제어 리스트(ACL) 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오.<br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본 버킷 권한을 상속하십시오.** | String      | 아니요   |
| GrantRead           | 권한을 부여받은 대상에게 객체를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String      | 아니요   |
| GrantFullControl    | 권한을 부여받은 대상에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다.<br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String      | 아니요   |
| AccessControlPolicy | 객체의 액세스 제어 리스트(ACL) 속성 정보 설정                        | Object      | 아니요   |
| - Owner             | 객체 소유자 정보                                             | Object      | 아니요   |
| - - ID              | 객체 소유자 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      | 아니요   |
| - - DisplayName     | 객체 소유자 이름                                             | String      | 아니요   |
| - Grants            | 권한을 부여받은 대상의 정보 및 권한 정보 리스트                                   | ObjectArray | 아니요   |
| - -Permission      | 권한을 부여받은 대상의 권한 정보 표시. 열거 값: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      | 아니요   |
| - - Grantee         | 권한을 부여받은 대상의 정보                                               | Object      | 아니요   |
| - - - DisplayName   | 권한을 부여받은 대상의 이름                                               | String      | 아니요   |
| - - - ID            | 권한을 부여받은 대상의 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등)             | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |

### 객체 ACL 조회

#### 기능 설명

GET Object acl 인터페이스는 버킷의 객체 액세스 권한을 조회할 때 사용합니다. 버킷 소유자에게만 작업 권한이 주어집니다.

#### 사용 예시

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예    |
| Region | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key    | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| data              | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| - ACL             | 객체의 액세스 제어 리스트(ACL) 속성. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오. | String      |
| - Owner           | 리소스 소유자 식별                                             | Object      |
| - - ID              | 객체 소유자 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정 ID인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - - DisplayName   | 객체 소유자 이름                                             | String      |
| - Grants            | 권한을 부여받은 대상의 정보 및 권한 정보 리스트                                   | ObjectArray |
| - -Permission      | 권한을 부여받은 대상의 권한 정보 표시. 열거 값: READ, READ_ACP, WRITE_ACP, FULL_CONTROL | String      |
| - - Grantee       | 권한을 부여받은 대상 정보                                             | Object      |
| - - - DisplayName | 사용자 이름                                                   | String      |
| - - - ID          | 사용자 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정 ID인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |

## 고급 인터페이스(권장)

이 클래스의 방법은 상위 네이티브 방법을 캡슐화한 것으로, 멀티파트 복사의 전 과정을 구현합니다. 동시 멀티파트 복사, 중단 지점부터 이어서 전송, 업로드 작업의 취소, 일시 중지 및 재시작 등을 지원합니다.

### 객체 복사

#### 기능 설명

Slice Copy File은 멀티파트 복사를 통해 원본 경로에서 타깃 경로로 파일을 복사하는 데 사용합니다. 복사 과정에서 객체 메타데이터와 ACL이 수정될 수 있습니다. 사용자는 해당 인터페이스를 통해 파일 이동, 파일 이름 변경, 파일 속성 수정 및 사본 생성을 할 수 있습니다.

#### 방법 모델

Slice Copy File을 호출하여 작업합니다.

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000',                               /* 필수 */
    Region: 'ap-beijing',                                  /* 필수 */
    Key: '1.zip',                                            /* 필수 */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.zip', /* 필수 */
    onProgress:function (progressData) {                     /* 옵션 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | 버킷의 이름. 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String   | 예    |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String   | 예   |
| Key                    | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String   | 예   |
| CopySource             | 원본 객체의 URL 경로. URL 매개변수 ?versionId=&lt;versionId>를 통해 이전 버전을 지정할 수 있습니다.  | String   | 예   |
| ChunkSize              | 멀티파트 복사 시 파트당 바이트 수. 기본값: 1048576(1MB)          | Number   | 아니요   |
| SliceSize              | 파일 크기가 일정 값 초과 시 멀티파트 복사를 사용하도록 하는 매개변수. 단위: Byte, 기본값: 5G. 해당 값 이하인 경우 putObjectCopy를 사용해 업로드하고, 초과하는 경우 sliceCopyFile을 사용해 업로드합니다. | Number   | 아니요   |
| onProgress             | 업로드 파일의 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다.      | Function | 아니요   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | 아니요   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number               | 아니요   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number               | 아니요   |
| - progressData.percent | 파일의 복사 백분율. 소수점으로 표시합니다. 예: 복사 50%를 0.5로 표시       | Number   | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷                                         | String |
| - Key                  | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - ETag       | 병합 후 파일의 MD5 알고리즘 검증값<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 큐 업로드

미니프로그램 SDK는 putObject에서 보낸 업로드 작업을 모두 큐에 기록하며 큐에 관한 방법은 다음과 같습니다.

1. cos.getTaskList로 작업 리스트를 가져올 수 있습니다.
2. cos.pauseTask, cos.restartTask, cos.cancelTask로 작업을 진행합니다.
3. cos.on('list-update', callback);으로 리스트와 진행률 변화를 수신할 수 있습니다.

전체적인 큐 사용 예시는 [demo-queue](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue)를 참조하십시오.

#### 업로드 작업 취소

taskId에 따라 업로드 작업을 취소합니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = 'xxxxx';                   /* 필수 */
cos.cancelTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. putObject 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | 예   |

#### 업로드 작업 일시 중지

taskId에 따라 업로드 작업을 일시 중지합니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = 'xxxxx';                   /* 필수 */
cos.pauseTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. putObject 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | 예   |

#### 업로드 작업 재시작

taskId에 따라 업로드 작업을 재시작합니다. 사용자가 수동으로 중단(pauseTask를 호출하여 중단)하거나 오류로 중단된 업로드 작업을 재시작하는 데 사용할 수 있습니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* 필수 */
cos.restartTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. putObject를 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | 예   |
