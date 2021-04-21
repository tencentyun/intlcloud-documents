## 소개

본 문서는 객체에 대한 고급 인터페이스, 간단한 조작, 블록 작업 관련 API 개요 및 SDK 샘플 코드를 제공합니다.

**간편한 조작**

| API                                                          | 작업명         | 설명                                 |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷 하위의 일부 혹은 모든 객체 조회           |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간단한 객체 업로드   | 객체 하나를 버킷에 업로드                     |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 객체 업로드 포맷   | 포맷을 사용한 객체 업로드 요청                     |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체의 메타데이터 정보 조회                     |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 객체 하나를 로컬에 다운로드                       |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | 크로스 도메인 설정 사전 요청 | 사전 요청을 통해 실제 크로스 도메인 요청의 발송 가능 여부를 확인 |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사       | 객체를 타깃 경로에 복사(객체 키)             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | 버킷에서 지정 객체 삭제                   |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | 버킷에서 다수의 객체 삭제                   |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관 객체 복구 | 보관되어 있는 객체를 검색해 액세스 |


**블록작업**

| API                                                          | 작업명         | 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 임무 초기화                    |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 블록 업로드       | 멀티파트 업로드 객체                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 블록 복사       | 다른 객체를 하나의 블록으로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 이미 업로드된 블록 조회   | 특정 멀티파트 업로드 작업에서 이미 업로드된 블록 조회     |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 객체의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 블록 삭제 |




## 간편한 조작

### 객체 리스트 조회

#### 기능 설명

버킷 하위의 일부 혹은 모든 객체를 조회합니다.

#### 사용 예시

예시1: 디렉터리 a의 모든 파일을 나열합니다.

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 필수 */
    Prefix: 'a/',           /* 선택 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

반환 값 포맷:

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

예시2: 디렉터리 a의 모든 파일을 열거하고, 깊이 우선 탐색은 하지 않습니다.

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Prefix: 'a/',              /* 선택 */
    Delimiter: '/',            /* 선택 */
}, function(err, data) {
    console.log(err || data.CommonPrefixes);
});
```

반환 값 포맷:

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

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | 버킷의 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region       | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Prefix       | 객체 키의 접두사 매칭은 반환에서 지정된 접두사만을 포함하는 객체 키에 한정됩니다.             | String | 아니오   |
| Delimiter    | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용됩니다. 보통 `/`를 전달합니다. 모든 객체 키는 Prefix부터 혹은 처음(Prefix가 지정되지 않았을 경우)부터 첫 번째 delimiter 사이의 동일한 부분의 경로를 같은 것으로 보고 Common Prefix로 정의되며, 그 후로 모든 Common Prefix가 열거됩니다.  | String | 아니오   |
| Marker       | 객체 키가 시작되는 마크입니다. Marker부터 시작되는 MaxKeys 항목을 열거하며, UTF-8 사전 순서대로 열거되는 것이 기본값입니다. | String | 아니오   |
| MaxKeys      | 단일 반환 최대 항목 수량은 기본 1000부터 최대 1000입니다.                 | String | 아니오   |
| EncodingType | 규정된 반환 값의 인코딩 방식은 url을 선택할 수 있습니다. 반환 객체　키를 대표하는 것은 URL 인코딩(퍼센트 인코딩)값입니다. 예를 들어, "Tencent Cloud"는 `%E8%85%BE%E8%AE%AF%E4%BA%91`로 인코딩되었습니다. | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름           | 매개변수 설명                                                    | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오. | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| data              | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.                | Object      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                  | Number      |
| - Name            | 버킷의 이름 포맷은 &lt;BucketName-APPID>이며, 예를 들어 examplebucket-1250000000과 같습니다. | String      |
| - Prefix          | 객체 키의 접두사 매칭은 해당 기호 다음부터(해당 기호를 포함하지 않음) UTF-8 사전 순서에 따른 반환 객체 키 항목입니다.  | String      |
| - Marker          | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 Marker부터 시작됩니다.   | String      |
| - MaxKeys         | 요청에서 한 번에 응답할 수 있는 반환 결과의 최대 수량                       | String      |
| - Delimiter       | 구분 문자                                                       | String      |
| - IsTruncated     | 요청 항목에 대한 응답이 차단되었는지 여부는 'true' 혹은 'false'로 알 수 있습니다.             | String      |
| - NextMarker      | 반환 항목이 차단되었을 경우, 반환NextMarker가 다음 항목의 시작점을 표시합니다.   | String      |
| - CommonPrefixes  | Prefix부터 delimiter 사이의 경로를 하나로 보고, Common Prefix로 정의합니다. | ObjectArray |
| - - Prefix        | 단일 Common Prefix의 접두사                                   | String      |
| - EncodingType    | 반환 값의 인코딩 방식은 주로 Delimiter, Marker, Prefix, NextMarker, Key에 작용합니다. | String      |
| - Contents        | 객체 메타데이터 정보 리스트                                           | ObjectArray |
| - - Key           | 객체 키, 즉, 객체의 이름                                         | String      |
| - - ETag          | 객체 콘텐츠가 연산한 MD5 알고리즘 인증값에 따릅니다. 예를 들면 `"22ca88419e2ed4721c23807c678adbe4c08a7880"`입니다. **주의: 앞뒤에 쌍따옴표가 사용됩니다.** | String      |
| - - Size          | 객체의 크기 단위는 Byte입니다.                                          | String      |
| - - LastModified  | 객체의 최종 수정 시간은 ISO8601 포맷에 따릅니다. 예를 들어 2019-05-24T10:56:40Z입니다. | String      |
| - - Owner         | 객체 소유자 정보                                               | Object      |
| - - - ID          | 객체 소유자의 ID 포맷은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`이며, 예를 들어 `qcs::cam::uin/100000000001:uin/100000000001`에서 100000000001이 uin입니다. | String      |
| - - - DisplayName | 객체 소유자의 이름                                             | String      |
| - - StorageClass  | 객체의 스토리지 유형입니다. STANDARD, STANDARD_IA, ARCHIVE와 같은 열거 값이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참조하십시오. | String      |

### 간단한 객체 업로드

#### 기능 설명

PUT Object 인터페이스는 하나의 객체를 지정된 버킷에 업로드할 수 있습니다. 이 작업은 요청자가 버킷에 대한 WRITE 권한을 가지고 있어야 합니다. 최대 5GB 미만인 객체의 업로드를 지원합니다. 5GB 이상의 객체는 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 혹은 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) 업로드를 사용하십시오.

> !
> 1. Key(파일명)는 `/`로 끝나서는 안 됩니다. 그렇지 않으면 폴더로 인식될 수 있습니다.
> 2. 루트 계정(동일한 APPID)당 버킷의 ACL 규칙 수량은 최대 1000개이며, 객체 ACL 규칙 수량에는 제한이 없습니다. 객체 ACL 제어가 필요하지 않을 경우, 업로드 시 설정하지 말고 버킷 권한을 상속받으십시오.
> 3. 업로드 후, 동일한 Key로 사전 서명 링크를 생성할 수 있습니다. 다운로드는 method를 GET로 지정하십시오. 자세한 인터페이스 설명은 아래에 나와 있으며, 다른 단말기로 공유하여 다운로드할 수 있습니다. 단, 파일이 개인 읽기 권한이라면 사전 서명 링크는 유효기간이 정해져 있다는 것에 주의하십시오.

#### 사용 예시

간단한 파일 업로드는 용량이 작은 파일을 업로드하는 데 적합합니다.

[//]: # (.cssg-snippet-put-object)
```js
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    StorageClass: 'STANDARD',
    Body: fs.createReadStream(filePath), // 파일 객체 업로드
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

Buffer를 파일 콘텐츠로 업로드합니다:

[//]: # (.cssg-snippet-put-object-bytes)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    Body: Buffer.from('hello!'), /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

문자열을 파일 콘텐츠로 업로드합니다:

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

생성 디렉터리:

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'a/',              /* 필수 */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형                 | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket                 | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String               | 예   |
| Region                 | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String               | 예   |
| Key                    | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String               | 예   |
| Body                   | FileStream, 문자열, Buffer 등의 파일 콘텐츠를 업로드할 수 있습니다.            | Stream/Buffer/String | 예   |
| CacheControl           | RFC 2616에 정의된 캐시 정책은 객체의 메타데이터로 저장됩니다.             | String               | 아니오   |
| ContentDisposition     | RFC 2616에 정의된 파일 이름은 객체의 메타데이터로 저장됩니다.             | String               | 아니오   |
| ContentEncoding        | RFC 2616에 정의된 인코딩 포맷은 객체의 메타데이터로 저장됩니다.             | String               | 아니오   |
| ContentLength          | RFC 2616에 정의된 HTTP 요청 콘텐츠 길이(바이트)                   | String               | 아니오   |
| ContentType            | RFC 2616에 정의된 콘텐츠 유형(MIME)은 객체의 메타데이터로 저장됩니다.     | String               | 아니오   |
| Expires                | RFC 2616에 정의된 만료 기간은 객체의 메타데이터로 저장됩니다.             | String               | 아니오   |
| Expect                 | Expect: 100-continue를 사용할 경우, 서버의 확인을 받아야만 요청 콘텐츠를 발송할 수 있습니다. | String               | 아니오   |
| ACL                    | 객체의 액세스 제어 리스트(ACL) 속성을 정의합니다. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오. <br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 혹은 이 항목을 설정하지 말고 버킷 권한을 상속하십시오.** | String               | 아니오   |
| GrantRead              | 권한을 부여받은 대상에게 객체를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니오   |
| GrantReadAcp           | 권한을 부여받은 대상에게 객체의 액세스 제어 리스트(ACL)를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니오   |
| GrantWriteAcp          | 권한을 부여받은 대상에게 객체의 액세스 제어 리스트(ACL)를 작성할 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니오   |
| GrantFullControl       | 권한을 부여받은 대상에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니오   |
| StorageClass           | 객체의 스토리지 유형을 설정합니다. STANDARD, STANDARD_IA, ARCHIVE 와 같은 열거 값이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참조하십시오. 기본값은 STANDARD입니다. | String               | 아니오   |
| x-cos-meta-*           | 사용자 정의된 헤더 정보는 객체의 메타데이터로 저장될 수 있습니다. 크기는 2KB로 제한됩니다. | String               | 아니오   |
| onTaskReady            | 업로드 작업 생성 시의 콜백 함수는 taskId 하나를 반환합니다. 업로드 작업의 고유 표식으로, 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다.    | Function             | 아니오   |
| - taskId               | 업로드 작업의 번호                                               | String               | 아니오   |
| onProgress             | 처리 중인 콜백 함수입니다. 처리 중 콜백에 응답하는 객체(progressData)의 속성은 다음과 같습니다.    | Function             | 아니오   |
| - progressData.loaded  | 이미 업로드한 파일의 일부 크기는 바이트(Bytes)를 단위로 합니다.                | Number               | 아니오   |
| - progressData.total   | 파일 전체의 크기는 바이트(Bytes)를 단위로 합니다.                        | Number               | 아니오   |
| - progressData.speed   | 파일의 업로드 속도는 바이트/초(Bytes/s)를 단위로 합니다.                   | Number               | 아니오   |
| - progressData.percent | 파일의 업로드 퍼센트는 소수점으로 표시합니다. 즉, 다운로드 50%를 0.5로 표시합니다.       | Number               | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| - ETag       | 반환 파일의 MD5 알고리즘 인증값입니다. ETag 값은 객체가 업로드 과정에서 손상이 있었는지 검사하는 데 사용할 수 있습니다. <br>예는 다음과 같습니다. `"09cba091df696af91549de27b8e7d0f6"`, **주의: ETag값 문자열의 앞뒤에 쌍따옴표가 사용됩니다.** | String |
| - Location   | 생성 객체의 외부 네트워크 액세스 도메인                                       | String |
| - VersionId  | 버전 제어 버킷을 실행해 반환된 객체의 버전 ID를 업로드합니다. 버킷이 한 번도 실행되지 않았다면 해당 매개변수도 반환되지 않습니다.   | String |

### 표준 업로드 객체

Node.js SDK는 POST Object 인터페이스에 대응하는 방법은 제공하지 않습니다. 해당 인터페이스를 사용해야 할 경우, [Web 다이렉트 실전](https://intl.cloud.tencent.com/document/product/436/9067)에 있는 “솔루션 B: Form 표준 업로드 사용”을 참조하십시오.

### 객체 메타데이터 조회

#### 기능 설명

객체의 메타데이터 정보를 조회합니다.

#### 사용 예시

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',               /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region          | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key             | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| IfModifiedSince | 지정된 시간 이후에 수정될 경우, 상응하는 메타데이터 정보를 반환하거나 304를 반환합니다.    | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                  | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드에는 200, 304 등이 있습니다. 지정된 시간 이후에 수정을 하지 않으면 304가 반환됩니다.  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| - x-cos-object-type   | 객체의 추가 업로드 가능 여부를 표시하기 위한 열거 값에는 normal, appendable이 있으며, 기본값 normal은 반환에 표시되지 않습니다. | String  |
| - x-cos-storage-class | 객체의 스토리지 레벨 열거 값에는 STANDARD, STANDARD_IA, ARCHIVE가 있으며, 기본값인 STANDARD는 반환에 표시되지 않습니다. | String  |
| - x-cos-meta-*        | 사용자 정의된 meta                                            | String  |
| - NotModified         | 지정 시간 이후 객체의 수정 여부                                 | Boolean |
| - ETag                | 반환 파일의 MD5 알고리즘 인증값입니다. ETag 값은 객체가 업로드 과정에서 손상이 있었는지 검사하는 데 사용할 수 있습니다. <br>예는 다음과 같습니다. `"09cba091df696af91549de27b8e7d0f6"`, **주의: ETag값 문자열의 앞뒤에 쌍따옴표가 사용됩니다.** | String  |
| - VersionId           | 버전 제어 버킷을 실행해 반환된 객체의 버전 ID를 업로드합니다. 버킷이 한 번도 실행되지 않았다면 해당 매개변수도 반환되지 않습니다. | String  |

### 객체 다운로드

GET Object 인터페이스 요청은 버킷 내 지정 객체의 콘텐츠를 획득하거나 로컬 다운로드할 수 있습니다. 해당 API의 요청자는 타깃 객체에 대한 읽기 권한이 있어야 하거나, 타깃 객체의 읽기 권한이 개방되어 있어야 합니다(공개 읽기).

#### 사용 예시

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Range가 파일 콘텐츠를 획득하도록 지정합니다.

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    Range: 'bytes=1-3',        /* 선택 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

파일을 지정된 경로로 다운로드합니다.

[//]: # (.cssg-snippet-get-object-path)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    Output: './exampleobject',
}, function(err, data) {
    console.log(err || data);
});
```

파일을 지정된 파일 스트림으로 다운로드합니다.

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형               | 필수입력 여부 |
| -------------------------- | ------------------------------------------------------------ | ------------------ | ---- |
| Bucket                     | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String             | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| Output                     | 출력된 파일 경로 혹은 입력 스트림이 전송되지 않으면 완전한 콘텐츠를 콜백 함수 data에 입력하십시오. | String/WriteStream | 아니오   |
| ResponseContentType        | 응답 헤더 설정의 Content-Type 매개변수                           | String             | 아니오   |
| ResponseContentLanguage    | 응답 헤더 설정의 Content-Language 매개변수                       | String             | 아니오   |
| ResponseExpires            | 응답 헤더 설정의 Content-Expires 매개변수                        | String             | 아니오   |
| ResponseCacheControl       | 응답 헤더 설정의 Cache-Control 매개변수                          | String             | 아니오   |
| ResponseContentDisposition | 응답 헤더 설정의 Content-Disposition 매개변수                    | String             | 아니오   |
| ResponseContentEncoding    | 응답 헤더 설정의 Content-Encoding 매개변수                       | String             | 아니오   |
| Range                      | RFC 2616에 정의된 바이트 범위. 범위 값은 반드시 bytes=first-last 포맷을 사용해야 합니다. first와 last는 0에 기초하여 시작하는 오프셋입니다. 예를 들어 bytes=0-9는 객체 데이터 중 처음 10바이트를 다운로드한다는 의미입니다. 지정하지 않을 경우, 객체 전체를 다운로드한다는 의미입니다. | String             | 아니오   |
| IfModifiedSince            | 객체가 지정된 시간 이후에 수정될 경우, 객체에 상응하는 메타데이터 정보를 반환하거나 304(not modified)를 반환합니다. | String             | 아니오  |
| IfUnmodifiedSince            | 객체가 지정된 시간 이후에 수정되지 않을 경우, 객체를 반환하거나 412(precondition failed)를 반환합니다. | String             | 아니오  |
| IfMatch                    | ETag와 지정된 콘텐츠가 일치해야만 객체가 반환되며, 그렇지 않을 경우 412(precondition failed)가 반환됩니다. | String             | 아니오   |
| IfNoneMatch                | ETag와 지정된 콘텐츠가 불일치하면 객체가 반환되며, 그렇지 않을 경우 304(not modified)가 반환됩니다. | String             | 아니오   |
| VersionId                  | 다운로드할 객체의 버전 ID를 지정합니다.                                    | String             | 아니오   |
| onProgress                 | 처리 중인 콜백 함수입니다. 처리 중 콜백에 응답하는 객체(progressData)의 속성은 다음과 같습니다.      | Function           | 아니오   |
| - progressData.loaded      | 이미 다운로드한 객체의 일부 크기는 바이트(Bytes)를 단위로 합니다.                | Number             | 아니오   |
| - progressData.total       | 객체 전체의 크기는 바이트(Bytes)를 단위로 합니다.                        | Number             | 아니오   |
| - progressData.speed       | 객체의 다운로드 속도는 바이트/초(Bytes/s)를 단위로 합니다.                   | Number             | 아니오   |
| - progressData.percent     | 객체의 다운로드 퍼센트는 소수점으로 표시합니다. 즉, 다운로드 50%를 0.5로 표시합니다.       | Number             | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                  | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드에는 200, 304, 403, 404 등이 있습니다.                  | Number  |
| - headers             | 요청 시 반환되는 헤더 정보                                           | Object  |
| - CacheControl        | RFC 2616에 정의된 캐시 명령어는 객체 메타데이터 패키지에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때에만 해당 헤더를 반환합니다. | String  |
| - ContentDisposition  | RFC 2616에 정의된 파일 이름은 객체 메타데이터 패키지에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때에만 해당 헤더를 반환합니다.  | String  |
| - ContentEncoding     | RFC 2616에 정의된 인코딩 포맷은 객체 메타데이터 패키지에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때에만 해당 헤더를 반환합니다. | String  |
| - Expires             | RFC 2616에 정의된 캐시 유효기간 만료 시간은 객체 메타데이터 패키지에 이 항목이 포함되거나 요청 매개변수를 통해 이 항목이 지정되었을 때에만 해당 헤더를 반환합니다.  | String  |
| - x-cos-storage-class | 객체의 스토리지 레벨 열거 값에는 STANDARD, STANDARD_IA, ARCHIVE가 있습니다. <br>**해당 헤더가 반환되지 않으면 CFS 레벨이 STANDARD(표준 스토리지)라는 뜻입니다.** | String  |
| - x-cos-meta-*        | 사용자 정의된 메타데이터                                           | String  |
| - NotModified         | 요청 시 IfModifiedSince가 있을 경우 해당 속성을 반환합니다. 파일이 수정되지 않으면 true이고, 그렇지 않으면 false입니다. | Boolean |
| - ETag                | 반환 파일의 MD5 알고리즘 인증값입니다. ETag 값은 객체가 업로드 과정에서 손상이 있었는지 검사하는 데 사용할 수 있습니다. <br>예는 다음과 같습니다. `"09cba091df696af91549de27b8e7d0f6"`, **주의: ETag값 문자열의 앞뒤에 쌍따옴표가 사용됩니다.** | String  |
| - VersionId           | 버전 제어 버킷을 실행해 반환된 객체의 버전 ID를 업로드합니다. 버킷이 한 번도 실행되지 않았다면 해당 매개변수도 반환되지 않습니다. | String  |
| - Body                | 반환된 파일 콘텐츠의 기본값은 Buffer 형식입니다.                           | Buffer  |

### 크로스 도메인 설정 사전 요청

#### 기능 설명

OPTIONS Object 인터페이스는 객체에 대한 도메인 간 액세스 설정을 사전 요청합니다. 즉, 도메인 간 액세스 요청 발송 전 OPTIONS 요청과 특정 출처, HTTP 방법, 헤더 정보 등을 COS에 보내 실제 크로스 도메인 요청의 가능 여부를 결정합니다. CORS 설정이 존재하지 않을 경우, 요청에 대한 반환은 403 Forbidden입니다. **사용자는 PUT Bucket cors 인터페이스를 통해 버킷의 CORS 지원을 실행할 수 있습니다.**

#### 사용 예시

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    Origin: 'https://www.qq.com',      /* 필수 */
    AccessControlRequestMethod: 'PUT', /* 필수 */
    AccessControlRequestHeaders: 'origin,accept,content-type' /* 선택 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체　키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| Origin                      | 도메인 간 액세스 시뮬레이션을 요청하는 출처 도메인                                    | String | 예   |
| AccessControlRequestMethod  | 도메인 간 액세스 시뮬레이션을 요청하는 HTTP 방법                                 | String | 예   |
| AccessControlRequestHeaders | 도메인 간 액세스 시뮬레이션을 요청하는 헤더                                       | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형    |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오. | Object  |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| data                         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - AccessControlAllowOrigin   | 도메인 간 액세스 시뮬레이션을 요청하는 출처 도메인의 경우, 중간에 쉼표로 간격을 둡니다. 출처를 허용하지 않을 경우, 그 Header(예: `*`)는 반환되지 않습니다. | String  |
| - AccessControlAllowMethods  | 도메인 간 액세스 시뮬레이션을 요청하는 HTTP 방법의 경우, 중간에 쉼표로 간격을 둡니다. 요청 방법을 허용하지 않을 경우, 그 Header(예: PUT, GET, POST, DELETE, HEAD)는 반환되지 않습니다. | String  |
| - AccessControlAllowHeaders  | 도메인 간 액세스 시뮬레이션을 요청하는 헤더의 경우, 중간에 쉼표로 간격을 둡니다. 시뮬레이션 요청 헤더를 아예 허용하지 않을 경우, 그 Header(예: accept, content-type, origin, authorization)는 해당 요청 헤더에 반환되지 않습니다. | String  |
| - AccessControlExposeHeaders | 크로스 도메인은 반환 헤더를 지원하며, ETag 등 중간에 쉼표로 간격을 둡니다.                  | String  |
| - AccessControlMaxAge        | OPTIONS 요청이 결과를 얻는 유효기간을 설정합니다. (ex. 3600)                  | String  |
| - OptionsForbidden           | OPTIONS 요청이 거부되었는지 여부를 알 수 있습니다. 반환된 HTTP 상태 코드가 403이면 true입니다. | Boolean |

### 객체 복사

#### 기능 설명

PUT Object - Copy는 기존에 있는 COS 객체의 사본 생성을 요청합니다. 한 객체는 기존 경로(객체 키)에서 타깃 경로(객체 키)로 복사됩니다. 복사되는 과정에서 객체 메타데이터와 액세스 제어 리스트(ACL)는 수정이 가능합니다.
사용자는 해당 인터페이스를 통해 사본 생성, 객체 메타데이터 수정(기존 객체와 타깃 파일의 속성은 동일), 객체의 이동과 이름 변경(복사 후 단독으로 호출하여 인터페이스 삭제)이 가능합니다.

> !객체의 크기는 1MB - 5GB를 권장합니다. 5GB가 넘는 객체는 고급 인터페이스 객체 복사 [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12)를 사용하십시오.

#### 사용 예시

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000',                               /* 필수 */
    Region: 'COS_REGION',                                  /* 필수 */
    Key: 'exampleobject',                                            /* 필수 */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체　키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| CopySource                  | 원래의 객체 URL 경로입니다. URL 매개변수 ?versionId=&lt;versionId>를 통해 과거의 버전을 지정할 수 있습니다.  | String | 예   |
| ACL                         | 객체의 액세스 제어 리스트(ACL) 속성을 정의합니다. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오. <br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 혹은 이 항목을 설정하지 말고 버킷 권한을 상속하십시오.** | String | 아니오   |
| GrantRead                   | 권한을 부여받은 대상에게 객체를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니오   |
| GrantWrite                  | 권한을 부여받은 대상에게 객체를 입력할 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니오   |
| GrantFullControl       | 권한을 부여받은 대상에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니오   |
| MetadataDirective           | 메타데이터 복사 여부의 열거 값은 Copy, Replaced이며, 기본값은 Copy입니다. Copy로 표기되어 있다면 Header의 사용자 메타데이터 정보를 무시하고 바로 복사합니다. Replaced로 표기되어 있다면 Header 정보에 따라 메타데이터를 수정합니다. **타깃 경로와 원 경로가 일치할 때, 즉 사용자가 메타데이터를 수정하려고 할 때는 반드시 Replaced로 표기되어 있어야 합니다.** | String | 아니오   |
| CopySourceIfModifiedSince   | 객체가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. ** CopySourceIfNoneMatch 와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | 아니오  |
| CopySourceIfUnmodifiedSince | 객체가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. ** CopySourceIfMatch 와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | 아니오   |
| CopySourceIfMatch           | 객체의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfUnmodifiedSince 와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | 아니오   |
| CopySourceIfNoneMatch       | 객체의 Etag와 불일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfModifiedSince 와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | 아니오   |
| StorageClass                | 객체의 스토리지 유형을 설정합니다. STANDARD, STANDARD_IA, ARCHIVE 와 같은 열거 값이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참조하십시오. 기본값은 STANDARD입니다. | String | 아니오   |
| x-cos-meta-*                | 기타 사용자 정의된 파일 헤더                                         | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오. | Object  |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| data                         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object  |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| - ETag         | 파일의 MD5 알고리즘 인증값입니다. 예를 들면 `"22ca88419e2ed4721c23807c678adbe4c08a7880"`입니다. **주의: 앞뒤에 쌍따옴표가 사용됩니다.** | String |
| - LastModified | 반환된 객체의 최종 수정 시간입니다. 예를 들면2017-06-23T12:33:27.000Z입니다.         | String |
| - VersionId    | 버전 제어 버킷을 실행해 반환된 객체의 버전 ID를 업로드합니다. 버킷이 한 번도 실행되지 않았다면 해당 매개변수도 반환되지 않습니다. | String |

### 단일 객체 삭제

#### 기능 설명

DELETE Object 인터페이스는 COS의 버킷에서 하나의 객체(Object) 삭제를 요청합니다. 해당 작업을 하려면 요청자가 버킷에 대한 WRITE 권한을 가지고 있어야 합니다.

#### 사용 예시

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject'                            /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket    | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region    | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key       | 객체　키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| VersionId | 삭제할 객체 버전 ID 혹은 DeleteMarker 버전 ID입니다.                  | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드에는 200, 204, 403, 404 등이 있습니다. **삭제에 성공하거나 파일이 존재하지 않을 경우 204 혹은 200이 반환되고, 지정 Bucket을 찾지 못할 경우 404가 반환됩니다.**  | Number  |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |

### 여러 객체 삭제

#### 기능 설명

DELETE Multiple Objects 인터페이스는 지정된 버킷에서 대량의 객체 삭제를 요청합니다. 한 번에 최대 1000개의 객체 삭제를 요청할 수 있습니다. 응답 결과에 대해 COS는 Verbose와 Quiet라는 두 가지 모드를 제공합니다. Verbose 모드는 모든 객체의 삭제 결과를 알려주고, Quiet 모드는 오류가 발생한 객체의 정보만 알려줍니다.

#### 사용 예시

여러 파일을 삭제합니다.

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Objects: [
        {Key: 'exampleobject'},
        {Key: 'exampleobject2'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket    | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region    | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Quiet       | 불(Boolean)값입니다. 이 값은 Quiet 모드의 실행여부를 결정합니다. true 값이면 Quiet모드를 실행하고, false 값이면 Verbose모드를 실행합니다. 기본값은 false입니다. | Boolean     | 아니오   |
| Objects     | 삭제할 객체 리스트                                             | ObjectArray | 예   |
| - Key       | 객체　키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      | 예   |
| - VersionId | 삭제할 객체 버전 ID 혹은 DeleteMarker 버전 ID입니다.                  | String      | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err                       | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오. | Object      |
| - statusCode              | 요청 시 반환되는 HTTP 상태 코드에는 200, 204, 403, 404 등이 있습니다.             | Number      |
| - headers                 | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                      | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object      |
| - statusCode              | 요청 시 반환되는 HTTP 상태 코드에는 200, 204, 403, 404 등이 있습니다.             | Number      |
| - headers                 | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Deleted                 | 이번에 삭제된 객체 정보 리스트를 설명합니다.                               | ObjectArray |
| - - Key                   | 객체　키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - - VersionId             | VersionId에 매개변수가 전달되면, 반환 시에도 VersionId를 동반하게 되며, 방금 작업한 객체 버전 혹은 DeleteMarker 버전을 표시합니다. | String      |
| - - DeleteMarker          | 버전 컨트롤이 실행되고 있는데 매개변수에 VersionId가 없다면, 이번 삭제에서는 파일 콘텐츠를 실제로 제거하지는 않고 DeleteMarker가 하나 더 추가됩니다. 볼 수 있던 파일이 이미 삭제되었다는 의미이며, 열거 값은 true와 false입니다. | String      |
| - - DeleteMarkerVersionId | 반환된 DeleteMarker가 true일 경우, 방금 새로 추가된 DeleteMarker의 VersionId가 반환됩니다. | String      |
| - Error                   | 이번에 삭제에 실패한 객체 정보 리스트를 설명합니다.                               | ObjectArray |
| - - Key                   | 객체　키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - - Code                  | 삭제 실패 에러 코드                                             | String      |
| - - Message               | 삭제 오류 정보                                                 | String      |


### 복구 보관 객체

#### 기능 설명

POST Object restore 인터페이스는 보관 유형의 객체를 복구할 수 있습니다. 복구되어 읽을 수 있는 객체는 임시적인 것으로, 읽기 가능한 상태 및 해당 임시 사본을 삭제하는 시간을 설정할 수 있습니다. Days 매개변수를 이용해 임시 객체의 만료 기간을 지정할 수 있으며, 그 기간이 지나고 기간 동안 복사, 연장 등의 작업이 진행되지 않으면 해당 임시 객체는 시스템에서 자동 삭제됩니다. 임시 객체는 archive 유형 객체의 사본이며, 보관된 원래의 객체는 이 기간 내내 존재합니다.

#### 사용 예시

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',
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

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region             | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key                | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| RestoreRequest     | 복구 데이터의 컨테이너에 사용됩니다.                                           | Object | 예   |
| - Days             | 임시 사본의 만료 기간을 설정합니다.                                       | Number | 예   |
| - CASJobParameters | CAS 작업 매개변수의 컨테이너입니다.                                       | Object | 예   |
| - - Tier           | CAS 유형의 데이터를 복원할 때, Tier는 COS가 지원하는 세 가지의 복구 모드로 지정될 수 있습니다. <br><li> Standard(표준 모드, 3 - 5시간 내 복구 작업 완료)<br><li>Expedited(급속 모드, 15분 내 복구 작업 완료)<br><li> Bulk(대량 모드, 5 - 12 시간 내 복구 작업 완료)<br>DEEP ARCHIVE 유형 데이터의 복구에는 두 가지 복구 모드가 있습니다. <br><li> Standard(표준 모드, 복구 시간 12 - 24시간)<br><li>Bulk(대량 모드, 복구 시간 24 - 48시간) | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |



## 블록 작업

### 멀티파트 업로드 조회

#### 기능 설명

List Multiparts Uploads는 현재 진행 중인 멀티파트 업로드 정보를 조회하는 데 사용됩니다. 한 번에 최대 1000개의 현재 진행 중인 멀티파트 업로드를 나열합니다.

#### 사용 예시

접두사를 exampleobject로 삼은 미완성 UploadId 리스트의 예시는 다음과 같습니다.

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Prefix: 'exampleobject',                        /* 선택 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region         | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Prefix         | 객체 키의 접두사 매칭은 반환에서 지정된 접두사만을 포함하는 객체 키에 한정됩니다. prefix를 사용해 조회 시 반환되는 객체 키에 Prefix가 포함되어 있으니 주의하십시오.            | String | 아니오   |
| Delimiter      | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용됩니다. 보통 `/`를 전달합니다. 모든 객체 키는 Prefix부터 혹은 처음(Prefix가 지정되지 않았을 경우)부터 첫 번째 delimiter 사이의 동일한 부분의 경로를 같은 것으로 보고 Common Prefix로 정의되며, 그 후로 모든 Common Prefix가 열거됩니다.  | String | 아니오   |
| EncodingType   | 규정된 반환 값의 인코딩 포맷입니다. 합법적 값은 url입니다.                            | String | 아니오   |
| MaxUploads     | 최대 반환 수량을 설정합니다. 합법적 최대치는 1 - 1000으로, 1000이 기본값입니다.         | String | 아니오   |
| KeyMarker      | upload-id-marker와 함께 사용합니다.<br> <li> upload-id-marker가 지정되지 않았을 경우: <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다. <br><li> upload-id-marker가 지정되었을 경우: <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다. <br>&emsp;- ObjectName 알파벳 순서가 key-marker와 같고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | String | 아니오   |
| UploadIdMarker | key-marker와 함께 사용합니다. <br><li>key-marker가 지정되지 않았을 경우: <br>&emsp;- upload-id-marker는 무시됩니다. <br><li>key-marker가 지정되었을 경우: <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다. <br>&emsp;- ObjectName 알파벳 순서가 key-marker와 같고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err                  | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode         |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number |
| - headers            | 요청 시 반환되는 헤더 정보                                           | Object |
| data                 | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode         |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number |
| - headers            | 요청 시 반환되는 헤더 정보                                           | Object |
| - Bucket             | 멀티파트 업로드의 타깃 버킷                                         | String      |
| - Encoding-Type      | 규정된 반환 값의 인코딩 포맷입니다. 합법적 값은 url입니다.                            | String      |
| - KeyMarker          | 열거된 항목은 해당 key값에서 시작합니다.                                      | String      |
| - UploadIdMarker     | 열거된 항목은 해당 UploadId값에서 시작합니다.                                 | String      |
| - NextKeyMarker      | 반환 항목이 차단되었을 경우, 반환된 NextKeyMarker가 다음 항목의 시작점이 됩니다. | String      |
| - NextUploadIdMarker | 반환 항목이 차단되었을 경우, 반환된 UploadId가 다음 항목의 시작점이 됩니다.     | String      |
| - MaxUploads         | 최대 반환 수량을 설정합니다. 합법적 최대치는 1 - 1000입니다.                | String      |
| - IsTruncated        | 반환 항목의 차단 여부는 'true' 혹은 'false'입니다.                      | String      |
| - Prefix             | 객체 키의 접두사 매칭은 반환에서 지정된 접두사만을 포함하는 객체 키에 한정됩니다.           | String      |
| - Delimiter          | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용됩니다. 보통 `/`를 전달합니다. 모든 객체 키는 Prefix부터 혹은 처음(Prefix가 지정되지 않았을 경우)부터 첫 번째 delimiter 사이의 동일한 부분의 경로를 같은 것으로 보고 Common Prefix로 정의되며, 그 후로 모든 Common Prefix가 열거됩니다. | String      |
| - CommonPrefixs      | Prefix부터 delimiter 사이의 경로를 하나로 보고, Common Prefix로 정의합니다. | ObjectArray |
| - - Prefix           | 구체적인 Common Prefixs를 표시합니다.                                    | String      |
| - Upload             | 멀티파트 업로드의 정보 집합                                           | ObjectArray |
| - - Key              | 객체의 이름, 즉 객체 키                                         | String      |
| - - UploadId         | 이번에 멀티파트 업로드된 ID를 표시합니다.                                        | String      |
| - - StorageClass     | 블록의 스토리지 유형을 표시하는 데 사용됩니다. 열거　값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)문서를 참조하십시오. | String      |
| - - Initiator        | 이번에 업로드한 담당자의 정보를 표시합니다.                                 | Object      |
| - - - DisplayName    | 업로드 담당자의 이름을 표시합니다.                                             | String      |
| - - - ID             | 업로드 담당자의 ID 포맷은 다음과 같습니다. `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정의 경우, &lt;OwnerUin>과 &lt;SubUin>은 같은 값입니다. | String      |
| - - Owner            | 블록 소유자의 정보를 표시합니다.                                     | Object      |
| - - - DisplayName | 블록 소유자의 이름                                             | String      |
| - - - ID             | 블록 소유자의 ID 포맷은 다음과 같습니다. `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정의 경우, &lt;OwnerUin> 와 &lt;SubUin> 는 같은 값입니다. | String      |
| - - Initiated        | 멀티파트 업로드의 시작 시간                                           | String      |

### 멀티파트 업로드 초기화

#### 기능 설명

Initiate Multipart Uploads는 멀티파트 업로드 초기화를 요청합니다. 요청을 성공적으로 처리하면 Upload ID를 반환하고, 이는 다음 Upload Part 요청에 사용됩니다.

#### 사용 예시

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
}, function(err, data) {
    console.log(err || data);
    if (data) {
      uploadId = data.UploadId;
    }
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region             | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key                | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| CacheControl       | RFC 2616에 정의된 캐시 정책은 객체의 메타데이터로 저장됩니다.             | String | 아니오   |
| ContentDisposition | RFC 2616에 정의된 파일 이름은 객체의 메타데이터로 저장됩니다.            | String | 아니오   |
| ContentEncoding    | RFC 2616에 정의된 인코딩 포맷은 객체의 메타데이터로 저장됩니다.            | String | 아니오   |
| ContentType        | RFC 2616에 정의된 콘텐츠 유형(MIME)은 객체의 메타데이터로 저장됩니다.    | String | 아니오   |
| Expires            | RFC 2616에 정의된 만료 기간은 객체의 메타데이터로 저장됩니다.            | String | 아니오   |
| ACL                | 객체의 액세스 제어 리스트(ACL) 속성을 정의합니다. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오. <br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 혹은 이 항목을 설정하지 말고 버킷 권한을 상속하십시오.** | String | 아니오   |
| GrantRead          | 권한을 부여받은 대상에게 객체를 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니오   |
| GrantFullControl   | 권한을 부여받은 대상에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니오   |
| StorageClass       | 객체의 스토리지 유형을 설정합니다. STANDARD, STANDARD_IA, ARCHIVE 와 같은 열거 값이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참조하십시오. 기본값은 STANDARD입니다. | String | 아니오   |
| x-cos-meta-*       | 사용자 정의된 헤더 정보는 객체의 메타데이터로 반환될 수 있습니다. 크기는 2KB로 제한됩니다. | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err                  | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| data                 | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| Bucket   | 멀티파트 업로드의 타깃 버킷입니다. 포맷은 BucketName-APPID이며, 예시는 examplebucket-1250000000입니다. | String |
| Key      | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| UploadId | 후속 업로드 중 사용된 ID                                        | String |

### 블록 업로드

#### 기능 설명

Upload Part 인터페이스는 초기화 이후의 멀티파트 업로드를 요청합니다. 지원되는 블록의 수는 1 - 10000개이며, 블록의 크기는 1MB - 5GB입니다. 
<li>멀티파트 업로드를 초기화하려면, Initiate Multipart Upload 인터페이스로 멀티파트 업로드를 초기화한 후 uploadId를 획득합니다. 이 ID는 블록 데이터의 고유 표식일 뿐 아니라 전체 파일에서 블록 데이터의 상대적 위치가 어딘지 알려줍니다.</li>
<li>Upload Part를 요청할 때마다 partNumber와 uploadId가 필요합니다. partNumber는 블록의 번호로, 비순차적 업로드를 지원합니다.</li>
<li>uploadId와 partNumber가 동일할 때, 나중에 들어오는 블록은 이전 블록을 덮어쓰게 됩니다. uploadId가 존재하지 않을 경우, 404 오류가 반환됩니다. 에러 코드는 NoSuchUpload입니다.</li>

#### 사용 예시

[//]: # (.cssg-snippet-upload-part)
```js
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    ContentLength: '1024',
    UploadId: 'exampleUploadId',
    PartNumber: '1',
    Body: fs.createReadStream(filePath)
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket             | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region             | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key                | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |
| ContentLength          | RFC 2616에 정의된 HTTP 요청 콘텐츠 길이(바이트)                   | String               | 예   |
| PartNumber    | 블록의 번호                                                   | String           | 예   |
| UploadId      | 이번 멀티파트 업로드 작업의 번호                                       | String           | 예   |
| Body                   | 파일 블록의 콘텐츠를 업로드합니다.문자열, File 객체 혹은 Blob 객체일 수도 있습니다.            | Stream/Buffer/String | 예   |
| Expect        | RFC 2616에서 정의된 HTTP 요청 콘텐츠의 길이(바이트). `Expect: 100-continue`를 사용할 경우, 서버의 확인을 받아야 요청 콘텐츠를 발송할 수 있습니다. | String           | 아니오   |
| ContentMD5    | RFC 1864에서 정의된 Base64 인코딩 128-bit 콘텐츠 MD5 인증값. 이 헤더는 파일 콘텐츠에 변화가 있는지를 인증하는 데 사용됩니다. | String           | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |

### 블록 복사

#### 기능 설명

Upload Part - Copy 인터페이스는 하나의 객체 블록 콘텐츠가 원 경로에서 타깃 경로로 복사되는 것을 요청합니다.

> !멀티파트 업로드를 사용하려면, 반드시 멀티파트 업로드를 초기화해야 합니다. 초기화된 멀티파트 업로드 응답에서 고유 디스크립터(upload ID)가 반환됩니다. 멀티파트 업로드 요청 시 이 ID를 꼭 가지고 있어야 합니다.

#### 사용 예시

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /* 필수 */
    UploadId: 'exampleUploadId', /* 필수 */
    PartNumber: '1', /* 필수 */
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체　키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| CopySource                  | 원래의 객체 URL 경로입니다. URL 매개변수 ?versionId=&lt;versionId>를 통해 과거의 버전을 지정할 수 있습니다.  | String | 예   |
| PartNumber                  | 멀티파트 복사의 블록 번호                                               | String | 녜   |
| UploadId                    | 멀티파트 업로드 파일을 사용하려면, 반드시 멀티파트 업로드를 초기화해야 합니다. 초기화된 멀티파트 업로드 응답에서 고유 디스크립터(upload ID)가 반환됩니다. 멀티파트 업로드 요청 시 이 ID를 꼭 가지고 있어야 합니다. | String | 예   |
| CopySourceRange             | 원 객체의 바이트 범위입니다. 범위값은 반드시 bytes=first-last 포맷을 사용해야 하며, first와 last는 모두 0으로 시작하는 오프셋입니다. 예를 들어 bytes=0-9는 원 객체에서 처음 10바이트의 데이터를 복사하겠다는 뜻입니다. 만약 지정하지 않는다면, 객체 전체를 복사하겠다는 뜻입니다. | String | 아니오   |
| CopySourceIfMatch           | 객체의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Unmodified-Since와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | 아니오   |
| CopySourceIfNoneMatch       | 객체의 Etag와 불일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Modified-Since와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | 아니오   |
| CopySourceIfUnmodifiedSince | 객체가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Match와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | 아니오   |
| CopySourceIfModifiedSince   | 객체가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-None-Match와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오. | Object  |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| data                         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object  |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| - ETag         | 파일의 MD5 알고리즘 인증값입니다. 예를 들면 `"22ca88419e2ed4721c23807c678adbe4c08a7880"`입니다. **주의: 앞뒤에 쌍따옴표가 사용됩니다.** | String |
| - LastModified | 반환된 객체의 최종 수정 시간입니다. GMT 포맷입니다.                               | String |

### 이미 업로드된 블록 조회

#### 기능 설명

List Parts는 특정 멀티파트 업로드 중에서 이미 업로드된 블록을 조회하는 데 쓰입니다. 즉, 지정 UploadId에서 이미 업로드에 성공한 모든 블록을 열거하는 것입니다.

#### 사용 예시

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    UploadId: 'exampleUploadId', /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| UploadId         | 이번에 멀티파트 업로드된 ID를 표시합니다. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다. | String | 예   |
| EncodingType     | 규정된 반환 값의 인코딩 방식입니다                                         | String | 아니오   |
| MaxParts         | 단일 반환 시 최대 항목 수량은 기본값이 1000입니다.                           | String | 아니오   |
| PartNumberMarker | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 Marker부터 시작됩니다.  | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| data                         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object  |
| - statusCode                 |  요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number  |
| - headers                    |  요청 시 반환되는 헤더 정보                                           | Object  |
| - Bucket             | 멀티파트 업로드의 타깃 버킷                                         | String      |
| - Encoding-type        | 규정된 반환 값의 인코딩 방식입니다.                                         | String      |
| - Key                  | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - UploadId             | 이번에 멀티파트 업로드된 ID를 표시합니다. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다.                                       | String      |
| - Initiator            | 이번에 업로드한 담당자의 정보를 표시합니다.                                 | Object      |
| - - DisplayName        | 업로드 담당자의 이름을 표시합니다.                                             | String      |
| - - ID                 | 업로드 담당자의 ID 포맷은 다음과 같습니다. `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정의 경우, &lt;OwnerUin>과 &lt;SubUin>은 같은 값입니다. | String      |
| - Owner                | 블록 소유자의 정보를 표시합니다.                                 | Object      |
| - - DisplayName        | 버킷 소유자의 이름입니다.                                         | String      |
| - - ID                 | 버킷 소유자의 ID입니다. 보통 사용자의 UIN입니다.                            | String      |
| - StorageClass         | 블록의 스토리지 유형을 표시하는 데 사용됩니다. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)문서를 참조하십시오.| String      |
| - PartNumberMarker     | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 Marker부터 시작됩니다.  | String      |
| - NextPartNumberMarker | 반환 항목이 차단되었을 경우, 반환된 NextMarker가 다음 항목의 시작점이 됩니다.   | String      |
| - MaxParts             | 단일 반환 시 최대 항목 수량입니다.                                       | String      |
| - IsTruncated          | 반환 항목의 차단 여부는 'true' 혹은 'false'입니다.                      | String      |
| - Part                 | 블록 정보 리스트                                                 | ObjectArray |
| - - PartNumber         | 블록의 번호                                                     | String      |
| - - LastModified       | 블록의 최종 수정 시간                                               | String      |
| - - ETag               | 블록의 MD5 알고리즘 인증값                                          | String      |
| - - Size               | 블록의 크기 단위는 Byte입니다.                                          | String      |

### 멀티파트 업로드 완료

#### 기능 설명

Complete Multipart Upload 인터페이스는 전체 블록 업로드 완료를 요청합니다. Upload Parts를 사용해 모든 블록을 업로드한 후에는 반드시 해당 API를 호출하여 전체 파일의 멀티파트 업로드를 완료해야 합니다. 해당 API를 사용할 때에는 반드시 Body에서 모든 블록의 PartNumber와 ETag를 요청해 블록의 정확성을 인증해야 합니다.
멀티파트 업로드가 완료된 후에는 통합이 필요합니다. 통합에 몇 분 정도 시간이 걸리기 때문에, 블록 통합이 시작되면 COS는 곧바로 상태 코드 200을 반환합니다. 통합 과정에서 COS는 주기적으로 빈 칸 정보를 반환해 연결을 활성화합니다. 통합이 완료되면 COS는 Body에서 통합 후 블록의 콘텐츠를 반환합니다.

- 업로드된 블록이 1MB보다 작을 경우, 해당 API를 호출할 때 400 EntityTooSmall이 반환됩니다.
- 업로드된 블록의 번호가 불연속적일 경우, 해당 API를 호출할 때 400 InvalidPart가 반환됩니다.
- Body에 있는 블록 정보를 시리얼 넘버에 맞춰 순차적으로 요청하지 않을 경우, 해당 API를 호출할 때 400 InvalidPartOrder가 반환됩니다.
- UploadId가 존재하지 않을 경우, 해당 API를 호출할 때 404 NoSuchUpload가 반환됩니다.

> !업로드가 완료되었으나 중단되지 않은 블록이 스토리지 용량을 차지하여 비용이 발생하므로, 즉시 멀티파트 업로드를 완료하거나 취소할 것을 권장합니다.

#### 사용 예시

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    UploadId: 'exampleUploadId', /* 필수 */
    Parts: [
        {PartNumber: '1', ETag: 'exampleETag'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| UploadId     | 업로드 작업 번호                                                 | String      | 예   |
| Parts        | 이번 멀티파트 업로드된 블록 정보 리스트를 설명합니다.                           | ObjectArray | 예   |
| PartNumber    | 블록의 번호                                                   | String           | 예   |
| - ETag       | 파일의 MD5 알고리즘 인증값입니다. <br>예를 들면 `"22ca88419e2ed4721c23807c678adbe4c08a7880"`입니다. **주의: 앞뒤에 쌍따옴표가 사용됩니다.** | String      | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| - Location   | 생성 객체의 외부 네트워크 액세스 도메인                                       | String |
| - Bucket             | 멀티파트 업로드의 타깃 버킷                                         | String      |
| - Key                  | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - ETag       | 통합 후 파일의 고유 ID입니다. 포맷은 다음과 같습니다: "uuid-<블록 수>"<br>예시:  `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 앞뒤에 쌍따옴표가 사용됩니다.** | String |

### 멀티파트 업로드 중지

#### 기능 설명

Abort Multipart Upload는 멀티파트 업로드 작업 중지 및 이미 업로드된 블록 삭제에 사용됩니다. Abort Multipart Upload를 호출할 때, 이 UploadId를 사용해 블록 업로드 요청을 했다면 Upload Parts는 실패를 반환할 것입니다. 해당 UploadId가 존재하지 않을 경우, 404 NoSuchUpload가 반환될 것입니다.

> !업로드가 완료되었으나 중단되지 않은 블록이 스토리지 용량을 차지하여 비용이 발생하므로, 즉시 멀티파트 업로드를 완료하거나 취소할 것을 권장합니다.

#### 사용 예시

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',                           /* 필수 */
    UploadId: 'exampleUploadId'                       /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| UploadId | 이번에 멀티파트 업로드된 ID를 표시합니다. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |



## 고급 인터페이스(권장)

이 방법은 상위 네이티브 방법을 캡슐화한 것으로, 멀티파트 업로드/복사의 전 과정을 구현하였으며 멀티파트 업로드/복사를 동시 지원합니다. 또한, File Transfer Protocol을 지원하고, 업로드 작업의 취소, 일시 정지 및 재시작 등을 지원합니다.

### 멀티파트 업로드 객체

#### 기능 설명

Slice Upload File은 파일의 멀티파트 업로드에 사용되며, 대용량 파일 업로드에 적합합니다.

#### 사용 예시

[//]: # (.cssg-snippet-transfer-upload-file)
```js
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.sliceUploadFile({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    FilePath: filePath,                /* 필수 */
    onTaskReady: function(taskId) {                   /* 선택 */
        console.log(taskId);
    },
    onHashProgress: function (progressData) {       /* 선택 */
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) {           /* 선택 */
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| FilePath               | 업로드 파일 경로                                                 | String   | 예   |
| SliceSize              | 블록 크기                                                     | String   | 아니오   |
| AsyncLimit             | 블록의 동시 접속량                                                 | String   | 아니오   |
| StorageClass           | 객체의 스토리지 유형입니다. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참조하십시오.       | String   | 아니오   |
| onTaskReady            | 업로드 작업 생성 시의 콜백 함수는 taskId 하나를 반환합니다. 업로드 작업의 고유 표식으로, 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function | 아니오   |
| - taskId               | 업로드 작업의 번호                                               | String               | 아니오   |
| onHashProgress         | 파일의 MD5 값을 계산하는 진행 콜백 함수입니다. 콜백 매개변수는 진행 객체 progressData입니다. | Function | 아니오   |
| - progressData.loaded  | 이미 인증된 파일의 일부 크기는 바이트(Bytes)를 단위로 합니다.                | Number               | 아니오   |
| - progressData.total   | 파일 전체의 크기는 바이트(Bytes)를 단위로 합니다.                        | Number               | 아니오   |
| - progressData.speed   | 파일의 인증 속도는 바이트/초(Bytes/s)를 단위로 합니다.                   | Number               | 아니오   |
| - progressData.percent     | 파일의 인증 퍼센트는 소수점으로 표시합니다. 즉, 다운로드 50%를 0.5로 표시합니다.       | Number             | 아니오   |
| onProgress             | 업로드 파일의 진행 콜백 함수입니다. 콜백 매개변수는 진행 객체 progressData입니다.      | Function | 아니오   |
| - progressData.loaded  | 이미 업로드한 파일의 일부 크기는 바이트(Bytes)를 단위로 합니다.                | Number               | 아니오   |
| - progressData.total   | 파일 전체의 크기는 바이트(Bytes)를 단위로 합니다.                        | Number               | 아니오   |
| - progressData.speed   | 파일의 업로드 속도는 바이트/초(Bytes/s)를 단위로 합니다.                   | Number               | 아니오   |
| - progressData.percent     | 파일의 업로드 퍼센트는 소수점으로 표시합니다. 즉, 다운로드 50%를 0.5로 표시합니다.       | Number             | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| - Location   | 생성 객체의 외부 네트워크 액세스 도메인                                       | String |
| - Bucket             | 멀티파트 업로드의 타깃 버킷                                         | String      |
| - Key                  | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - ETag       | 통합 후 파일의 고유 ID입니다. 포맷은 다음과 같습니다: "uuid-<블록 수>"<br>예시:  `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 앞뒤에 쌍따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어 버킷을 실행해 반환된 객체의 버전 ID를 업로드합니다. 버킷이 한 번도 실행되지 않았다면 해당 매개변수도 반환되지 않습니다.   | String |

### 객체 복사

#### 기능 설명

Slice Copy File은 블록 복사를 통해 원 경로에서 타깃 경로로 파일을 복사하는 데 사용됩니다. 복사 과정에서 객체 메타데이터와 ACL을 수정할 수 있습니다. 사용자는 해당 인터페이스를 통해 파일 이동, 파일 이름 변경, 파일 속성 수정 및 사본 생성을 할 수 있습니다.

#### 방법 모델

Slice Copy File 실행 작업:

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: 'examplebucket-1250000000',                               /* 필수 */
    Region: 'COS_REGION',                                  /* 필수 */
    Key: 'exampleobject',                                            /* 필수 */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /* 필수 */
    onProgress:function (progressData) {                     /* 선택 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                      | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String             | 예   |
| CopySource                  | 원래의 객체 URL 경로입니다. URL 매개변수 ?versionId=&lt;versionId>를 통해 과거의 버전을 지정할 수 있습니다.  | String | 예   |
| ChunkSize              | 블록 복사 시 블록의 바이트 수 기본값은 1048576(1MB)입니다.          | Number   | 아니오   |
| SliceSize              | 파일 크기가 일정 값을 초과할 경우, 블록 복사에 사용되는 단위 Byte의 기본값은 5G입니다. 이 값보다 작으면 putObjectCopy를 사용해 업로드하고, 크면 sliceCopyFile을 사용해 업로드합니다. | Number   | 아니오   |
| onProgress             | 업로드 파일의 진행 콜백 함수입니다. 콜백 매개변수는 진행 객체 progressData입니다.      | Function | 아니오   |
| - progressData.loaded  | 이미 업로드한 파일의 일부 크기는 바이트(Bytes)를 단위로 합니다.                | Number               | 아니오   |
| - progressData.total   | 파일 전체의 크기는 바이트(Bytes)를 단위로 합니다.                        | Number               | 아니오   |
| - progressData.speed   | 파일의 업로드 속도는 바이트/초(Bytes/s)를 단위로 합니다.                   | Number               | 아니오   |
| - progressData.percent     | 파일의 업로드 퍼센트는 소수점으로 표시합니다. 즉, 다운로드 50%를 0.5로 표시합니다.       | Number             | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403 404 등이 있습니다.                   | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| - Location   | 생성 객체의 외부 네트워크 액세스 도메인                                       | String |
| - Bucket             | 멀티파트 업로드의 타깃 버킷                                         | String      |
| - Key                  | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |
| - ETag         | 통합 후 파일의 MD5 알고리즘 인증값입니다. <br>예를 들면 `"22ca88419e2ed4721c23807c678adbe4c08a7880"`입니다. **주의: 앞뒤에 쌍따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어 버킷을 실행해 반환된 객체의 버전 ID를 업로드합니다. 버킷이 한 번도 실행되지 않았다면 해당 매개변수도 반환되지 않습니다.   | String |

### 일괄 업로드

#### 기능 설명

방법1:
일괄 업로드는 putObject와 sliceUploadFile을 직접 여러 번 호출하여 일괄 업로드를 완료할 수 있습니다. 인스턴스 매개변수 FileParallelLimit을 통해 파일의 동시 전송 수량을 제한합니다. 기본값은 3개입니다.

방법2: 
cos.uploadFiles를 호출하여 일괄 업로드할 수 있습니다. 매개변수 SliceSize는 파일 크기를 일정 값 이상으로 제어할 때 멀티파트 업로드를 사용할 수 있습니다. 다음은 uploadFiles 방법 설명입니다.

#### 방법 모델

uploadFiles 실행 작업:

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```js
const filePath1 = "temp-file-to-upload" // 로컬 파일 경로
const filePath2 = "temp-file-to-upload" // 로컬 파일 경로
cos.uploadFiles({
    files: [{
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key: 'exampleobject',
        FilePath: filePath1,
    }, {
        Bucket: 'examplebucket-1250000000',
        Region: 'COS_REGION',
        Key: '2.jpg',
        FilePath: filePath2,
    }],
    SliceSize: 1024 * 1024,
    onProgress: function (info) {
        var percent = parseInt(info.percent * 10000) / 100;
        var speed = parseInt(info.speed / 1024 / 1024 * 100) / 100;
        console.log('진도:' + percent + '%; 속도:' + speed + 'Mb/s;');
    },
    onFileFinish: function (err, data, options) {
        console.log(options.Key + '업로드' + (err ? '실패':'완료'));
    },
}, function (err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| files                  | 파일 리스트입니다. 모든 항목은putObject와 sliceUploadFile의 매개변수 객체로 전송됩니다. | Object | 예   |
| - Bucket               | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| - Region               | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| - Key       | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      | 예   |
| - FilePath             | 업로드 파일 경로                                                 | String | 예   |
| SliceSize              | 파일 크기가 일정 값을 초과할 경우, 멀티파트 업로드에 단위 Byte를 사용합니다. 이 값보다 작으면 putObject를 사용해 업로드하고, 크면 sliceUploadFile을 사용해 업로드합니다. | Number   | 예   |
| onProgress             | 모든 작업 진도를 계산하여 업로드하는 작업입니다.                            | String | 예   |
| - progressData.loaded  | 이미 업로드한 파일의 일부 크기는 바이트(Bytes)를 단위로 합니다.                | Number               | 아니오   |
| - progressData.total   | 파일 전체의 크기는 바이트(Bytes)를 단위로 합니다.                        | Number               | 아니오   |
| - progressData.speed   | 파일의 업로드 속도는 바이트/초(Bytes/s)를 단위로 합니다.                   | Number               | 아니오   |
| - progressData.percent     | 파일의 업로드 퍼센트는 소수점으로 표시합니다. 즉, 다운로드 50%를 0.5로 표시합니다.       | Number             | 아니오   |
| onFileFinish           | 파일마다 완료 혹은 오류를 콜백합니다.                                       | String | 예   |
| - err                  | 업로드 오류 정보                                               | Object | 아니오   |
| - data                 | 파일 완료 정보                                               | Object | 아니오   |
| - options              | 최근 완료된 파일의 매개변수 정보                                       | Object | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ----------- |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청이 제대로 되지 않은 경우, [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 파일의 세부 사항을 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드에는 200, 403, 404 등이 있습니다.                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 성공 시 객체가 반환됩니다. 요청에 오류가 발생할 경우 아무 것도 뜨지 않습니다.               | Object |
| - files      | 모든 파일의 error 혹은 data                                     | ObjectArray |
| - - error    | 업로드 오류 정보                                               | Object      |
| - - data     | 파일 완료 정보                                               | Object      |
| - - options  | 최근 완료된 파일의 매개변수 정보                                       | Object      |

### 큐 업로드

putObject와 sliceUploadFile을 대상으로 한 Node.js SDK의 업로드 작업에는 기록 큐가 있습니다. 큐와 관련된 방법은 다음과 같습니다.

1. cos.getTaskList은 작업 리스트를 획득할 수 있습니다.
2. cos.pauseTask, cos.restartTask, cos.cancelTask가 작업을 진행합니다.
3. cos.on('list-update', callback); 리스트와 진도의 변화를 리슨할 수 있습니다.

모범적인 큐 사용 예시는 [demo-queue](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue)를 참조하십시오.

#### 업로드 작업 취소

taskId에 따라 업로드 작업을 취소합니다.

** 이용 사례**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = 'xxxxx';                   /* 필수 */
cos.cancelTask(taskId);
```

**매개변수 설명**

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호입니다. sliceUploadFile 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | 예   |

#### 업로드 작업 일시 정지

taskId에 따라 업로드 작업을 일시 정지합니다.

** 이용 사례**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = 'xxxxx';                   /* 필수 */
cos.pauseTask(taskId);
```

**매개변수 설명**

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호입니다. sliceUploadFile 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | 예   |

#### 업로드 작업 재시작

taskId에 따라 업로드 작업을 다시 시작합니다. 사용자가 수동으로 중단(pauseTask 중지 호출)했거나 혹은 오류로 중단된 업로드 작업을 다시 시작하는 데 사용할 수 있습니다.

** 이용 사례**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = 'xxxxx';                   /* 필수 */
cos.restartTask(taskId);
```

**매개변수 설명**

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호입니다. sliceUploadFile 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | 예   |
