## 다운로드 및 설치

#### 관련 리소스

- COS의 XML JS SDK 소스 코드 다운로드 주소: [XML JavaScript SDK](https://github.com/tencentyun/cos-js-sdk-v5)
- SDK 고속 다운로드 주소: [XML JavaScript SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-js-sdk-v5/latest/cos-js-sdk-v5.zip)
- 예시 Demo 다운로드 주소: [XML JavaScript SDK Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo)
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/JavaScript)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [JavaScript SDK FAQ](https://intl.cloud.tencent.com/document/product/436/40775)를 참고하십시오.


>? SDK 사용 시 함수 또는 메소드 없음 등 오류가 발생하였을 경우, 먼저 SDK를 최신 버전으로 업데이트한 후 재시도하십시오.
>

#### 환경 준비

1. JavaScript SDK에는 ajax로 파일을 업로드하거나 파일의 MD5 값을 계산할 수 있도록 HTML5의 기본 특성을 지원하는 브라우저(IE10 이상을 지원하는 브라우저)가 필요합니다.
2. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인해 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참고해 버킷을 생성하고, 버킷 이름과 [리전 이름](https://intl.cloud.tencent.com/document/product/436/6224)을 획득합니다.
3. [CAM 콘솔](https://console.cloud.tencent.com/capi)에 로그인해 프로젝트의 SecretId와 SecretKey를 획득합니다.
4. CORS 규칙을 설정하고 AllowHeader를 `*`로 설정합니다. 아래 이미지와 같이, ExposeHeaders에는 ETag, Content-Length 및 기타 js가 읽어야 하는 header 필드가 필요합니다. 작업에 대한 자세한 내용은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318) 문서를 참고하십시오.


> ?본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭에 대한 의미와 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.

#### SDK 설치

다음과 같은 방법으로 SDK를 설치할 수 있습니다.

#### script 도입
>? [여기를 클릭](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/dist/cos-js-sdk-v5.min.js)해 최신 cos-js-sdk-v5.min.js를 다운로드합니다.
```html
<script src="https://unpkg.com/cos-js-sdk-v5/dist/cos-js-sdk-v5.min.js"></script>
```

script 태그가 SDK를 참고할 때, SDK는 전역 변수 이름 COS를 점유하며 해당 구조 함수를 통해 SDK 인스턴스를 생성할 수 있습니다.

#### webpack 도입 방식

`npm i cos-js-sdk-v5 --save`를 통해 SDK 종속을 설치하여, webpack 패키지 시나리오를 지원합니다. 사용자는 npm을 모듈로 도입할 수 있으며, 코드는 다음과 같습니다.

```js
var COS = require('cos-js-sdk-v5');
```

## 사용하기

### 임시 키 획득

프런트 엔드에 고정 키를 두면 보안 리스크가 있기 때문에, 정식 배포 시 임시 키 사용을 권장합니다. 구현 과정은 다음과 같습니다. 우선, 프런트 엔드가 서버를 요청하면 서버가 고정 키로 STS 서비스를 호출해서 임시 키를 신청합니다. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 문서를 참고하십시오. 이후 임시 키를 프런트 엔드로 반환합니다.

>!웹 사이트에 로그인 상태가 있는 경우, 로그인 상태 검증을 임시 키 획득 인터페이스에 추가해야 합니다.

### 초기화

1. web.html를 생성하고 아래 코드를 입력합니다. 또한 web.html의 버킷 이름과 Region을 수정합니다.
2. 백그라운드의 임시 키 서비스를 배포하고 getAuthorization의 키 서비스 주소를 수정합니다.
3. web.html을 Web 서버에 올리고, 브라우저로 페이지에 액세스해 파일 업로드를 테스트합니다. web.html 파일의 예시 코드는 다음과 같습니다.

```html
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'examplebucket-1250000000';
var Region = 'COS_REGION';     /* 버킷이 위치한 리전, 필수 필드 */

// 인스턴스 초기화
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 임시 키 비동기 획득
        $.get('http://example.com/server/sts.php', {
            bucket: options.Bucket,
            region: options.Region,
        }, function (data) {
            var credentials = data && data.credentials;
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                SecurityToken: credentials.sessionToken,
                // 사용자 브라우저 로컬 시간과의 편차가 너무 커 서명에 오류가 발생하지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다.
                StartTime: data.startTime, // 타임스탬프. 단위: 초. 예: 1580000000
                ExpiredTime: data.expiredTime, // 타임스탬프. 단위: 초. 예: 1580000900
            });
        });
    }
});

// 이어서 cos 인스턴스를 통해 COS 요청을 호출할 수 있습니다.
// TODO

</script>
```

### 설정 항목

#### 사용 예시

COS SDK 인스턴스 한 개를 생성합니다. COS SDK는 다음과 같은 형식 생성을 지원합니다.

- 형식1(권장): 백그라운드에서 임시 키를 획득하여 프런트 엔드로 보내고, 프런트 엔드에서 서명을 계산합니다.

[//]: # ".cssg-snippet-global-init-sts"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버 JS와 PHP 예시: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // 서버의 기타 언어는 COS STS SDK: https://github.com/tencentyun/qcloud-cos-sts-sdk를 참고하십시오.
        // STS 상세 문서 가이드는 https://intl.cloud.tencent.com/document/product/436/14048을 참고하십시오.
        $.get('http://example.com/server/sts.php', {
            // options에서 필요한 매개변수 획득 가능
        }, function (data) {
            var credentials = data && data.credentials;
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                SecurityToken: credentials.sessionToken,
                // 사용자 브라우저 로컬 시간과의 편차가 너무 커 서명에 오류가 발생하지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다.
                StartTime: data.startTime, // 타임스탬프. 단위: 초. 예: 1580000000
                ExpiredTime: data.expiredTime, // 타임스탬프. 단위: 초. 예: 1580000900
            });
        });
    }
});
```

- 형식2(권장): 세밀한 권한 제어. 백그라운드에서 임시 키를 획득하여 프런트 엔드로 보냅니다. 동일한 요청을 하는 경우에만 프런트 엔드가 임시 키를 재사용합니다. 백그라운드는 Scope을 통해 권한을 세밀하게 제어합니다.

[//]: # ".cssg-snippet-global-init-sts-scope"
```js
var COS = require('cos-js-sdk-v5');
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버 예시: https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/scope.md
        $.ajax({
            method: 'POST',
            url: ' http://example.com/server/sts-scope.php',
            data: JSON.stringify(options.Scope),
            beforeSend: function (xhr) {
                xhr.setRequestHeader('Content-Type', 'application/json');
            },
            dataType: 'json',
            success: function (data) {
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    SecurityToken: credentials.sessionToken,
                    // 사용자 브라우저 로컬 시간과의 편차가 너무 커 서명에 오류가 발생하지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다.
                    StartTime: data.startTime, // 타임스탬프. 단위: 초. 예: 1580000000
                    ExpiredTime: data.expiredTime, // 타임스탬프. 단위: 초. 예: 1580000900
                    ScopeLimit: true, // 세밀한 권한 제어는 true로 설정해 키가 동일한 요청을 하는 경우에만 재사용하도록 제한합니다.
                });
            }
        });
    }
});
```

- 형식3(권장하지 않음): 매번 프런트 엔드가 요청하기 전에 getAuthorization을 통해 서명을 획득하고, 백그라운드는 고정 키 또는 임시 키를 사용해 서명을 계산하여 프런트 엔드로 반환해야 합니다. 해당 형식의 멀티파트 업로드 권한은 제어하기 쉽지 않기 때문에 사용을 권장하지 않습니다.

[//]: # ".cssg-snippet-global-init-signature"
```js
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버에서 서명을 획득합니다. 해당 언어의 COS SDK: https://cloud.tencent.com/document/product/436/6474를 참고하십시오.
        // 주의사항: 보안 리스크가 있기 때문에 백그라운드는 method, pathname을 통해 권한을 엄격히 제어해야 합니다. 예: put / 비허용 등
        $.get('http://example.com/server/auth.php', {
            method: options.Method,
            pathname: '/' + options.Key,
        }, function (data) {
            if (!data || !data.authorization) return console.error('authorization invalid');
            callback({
                Authorization: data.authorization,
                // SecurityToken: data.sessionToken, // 임시 키를 사용하는 경우, sessionToken을 SecurityToken에 전송해야 합니다.
            });
        });
    },
    // 옵션 매개변수
    FileParallelLimit: 3,    // 파일 동시 업로드 수 제어
    ChunkParallelLimit: 3,   // 단일 파일의 멀티파트 동시 업로드 수 제어
    ProgressInterval: 1000,  // 업로드한 onProgress 콜백 간격 제어
});
```

- 형식4(권장하지 않음): 프런트 엔드는 고정 키를 사용해 서명을 계산합니다. 해당 형식은 프런트 엔드 디버깅에 적합하며, 사용 시 키가 노출되지 않도록 주의하십시오.

[//]: # ".cssg-snippet-global-init"
```js
// SECRETID와 SECRETKEY는 https://console.cloud.tencent.com/cam/capi에 로그인하여 조회 및 관리하십시오.
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
});
```

#### 구조 함수 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId               | 사용자의 SecretId                                              | String   | 아니요   |
| SecretKey              | 사용자의 SecretKey. 키가 노출되지 않도록 프런트 엔드 디버깅 시에만 사용하는 것을 권장합니다.       | String   | 아니요   |
| FileParallelLimit      | 동일한 인스턴스에 업로드하는 파일의 동시 전송 수. 기본값: 3                        | Number   | 아니요   |
| ChunkParallelLimit     | 동일한 업로드 파일의 멀티파트 동시 전송 수. 기본값: 3                          | Number   | 아니요   |
| ChunkRetryTimes        | 멀티파트 업로드 및 멀티파트 복사 시 오류가 발생하여 재시도한 횟수. 기본값: 3(첫 번째 시도를 더하면 요청은 총 4번) | Number   | 아니요   |
| ChunkSize              | 멀티파트 업로드 시 각 파트의 바이트 수. 기본값: 1048576(1MB)           | Number   | 아니요   |
| SliceSize              | uploadFiles로 일괄 업로드 시, 파일 크기가 해당 값보다 크면 멀티파트 업로드를 사용하고, 그렇지 않을 경우 간편 업로드를 호출합니다. 단위: Byte, 기본값: 1048576(1MB) | Number   | 아니요   |
| CopyChunkParallelLimit | 멀티파트 복사 작업 중에 멀티파트 업로드한 동시 전송 수. 기본값: 20             | Number   | 아니요   |
| CopyChunkSize          | sliceCopyFile로 파일 멀티파트 복사 시, 각 파트의 바이트 수. 기본값: 10485760(10MB) | Number   | 아니요   |
| CopySliceSize          | sliceCopyFile로 파일 멀티파트 복사 시, 파일 크기가 해당 값보다 크면 멀티파트 복사를 사용하고, 그렇지 않을 경우 간편 복사를 호출합니다. 기본값: 10485760(10MB) | Number   | 아니요   |
| ProgressInterval       | 업로드 진행률 콜백 방법 onProgress의 콜백 빈도. 단위: ms, 기본값: 1000 | Number   | 아니요   |
| Protocol               | 요청 시 사용하는 프로토콜. 옵션 항목으로 `https:`와 `http:`가 있습니다. 기본적으로 현재 페이지가 `http:`인 경우 `http:`를 사용하고, 아닌 경우 `https:`를 사용합니다. | String   | 아니요   |
| Domain                 | 버킷 및 객체 작업 API 호출 시 요청 도메인을 사용자 정의합니다. `"{Bucket}.cos.{Region}.myqcloud.com" `과 같은 템플릿을 사용할 수 있으며, API 호출 시 매개변수로 전달하는 Bucket 및 Region으로 변경할 수 있습니다. | String   | 아니요   |
| UploadQueueSize        | 업로드 큐 최대 길이. 초과된 작업이 waiting, checking, uploading 상태가 아닌 경우 정리합니다. 기본값: 10000 | Number   | 아니요   |
| ForcePathStyle         | 강제 사용 후 확장명 모드로 요청 발송. 확장명 모드의 Bucket에 도메인 뒤의 pathname을 넣고, 서명 pathname 계산을 추가합니다. 기본값: false | Boolean  | 아니요   |
| UploadCheckContentMd5  | 파일 업로드 시 Content-MD5 검증. 기본값: false. 활성화할 경우, 파일 업로드 시 파일 콘텐츠에 대해 MD5를 계산합니다. 파일 용량이 클수록 시간이 오래 걸립니다. | Boolean  | 아니요   |
| getAuthorization       | 서명을 획득하는 콜백 방법. SecretId, SecretKey가 없는 경우 이 매개변수는 필수입니다. <br> **주의사항: 해당 콜백 방법은 인스턴스 초기화 시 전송되며, 인스턴스로 인터페이스를 호출해야 실행되어 서명을 획득합니다. ** | Function | 아니요   |
| Timeout                | 타임아웃 시간. 단위: 밀리초. 기본값: 0. 즉 타임아웃 시간을 설정하지 않습니다.               | Number   | 아니요   |

#### getAuthorization 콜백 함수 설명의 함수 설명(형식1 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization의 콜백 매개변수 설명:

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | -------- |
| options  | 임시 키에 필요한 매개변수 객체 획득                                   | Object   |
| - Bucket | 버킷의 이름. 이름 생성 형식이 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String   |
| - Region | 버킷이 위치한 리전. 열거 값은 [버킷 리전 정보](https://intl.cloud.tencent.com/document/product/436/6224)를 참고하십시오. | String   |
| callback | 임시 키 획득 후 리턴 방법                                 | Function |

임시 키 획득 후 callback은 하나의 객체를 리턴합니다. 리턴 객체의 속성 리스트는 다음과 같습니다.

| 속성 이름            | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId       | 획득한 임시 키의 tmpSecretId                             | String | 예   |
| TmpSecretKey      | 획득한 임시 키의 tmpSecretKey                            | String | 예   |
| SecurityToken | 획득한 임시 키의 sessionToken. 해당 header의 x-cos-security-token 필드 | String | 예   |
| StartTime         | 키를 획득한 시작 시간. 즉 획득한 시간의 타임스탬프. 단위: 초. startTime. 예: 1580000000. 서명 시작 시간에 사용됩니다. 해당 매개변수를 전송하면 프런트 엔드 시간의 편차로 인한 서명 만료 문제를 방지할 수 있습니다. | String | 아니요   |
| ExpiredTime       | 획득한 임시 키의 expiredTime. 타임아웃 시간의 타임스탬프. 단위: 초. 예: 1580000900 | String | 예   |

#### getAuthorization 콜백 함수 설명(형식2 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization 함수 설명 및 콜백 매개변수 설명:

| 매개변수 이름     | 매개변수 설명                                                     | 유형     |
| ---------- | ------------------------------------------------------------ | -------- |
| options    | 서명에 필요한 매개변수 객체 획득                                       | Object   |
| - Method   | 현재 요청한 Method                                            | String   |
| - Pathname | 요청 경로. 서명 계산에 사용                                       | String   |
| - Key      | 객체 키(Object의 이름). 객체는 버킷에 있는 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.<br> **주의사항: 인스턴스로 요청한 인터페이스가 객체 작업과 관련된 인터페이스가 아닐 경우, 해당 매개변수는 빈칸으로 표시됩니다. ** | String   |
| - Query    | 현재 요청한 query 매개변수 객체. {key: 'val'} 의 형식               | Object   |
| - Headers  | 현재 요청한 header 매개변수 객체. {key: 'val'}의 형식              | Object   |
| callback   | 임시 키 획득 후 콜백                                     | Function |

getAuthorization 계산 완료 후 callback 리턴 매개변수는 두 가지 형식을 지원합니다.
형식1: 자격 증명 문자열 Authorization 리턴
형식2: 하나의 객체 리턴. 리턴 속성 리스트는 다음과 같습니다.

| 속성 이름            | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | 계산 후 얻은 서명 문자열                                         | String | 예   |
| SecurityToken | 획득한 임시 키의 sessionToken. 해당 header의 x-cos-security-token 필드 | String | 아니요   |

#### 자격 증명 획득

인스턴스 자체 자격 증명은 인스턴스화 중에 전송된 매개변수를 통해 제어하거나 획득할 수 있습니다. 획득 방법은 세 가지입니다.

1. 인스턴스화 시 SecretId, SecretKey를 전송합니다. 서명이 필요할 때마다 인스턴스 내부에서 계산합니다.
2. 인스턴스화 시 getAuthorization 콜백을 전송합니다. 서명이 필요할 때마다 해당 콜백으로 계산하고, 서명을 인스턴스로 반환합니다.
3. 인스턴스화 시 getAuthorization 콜백을 전송하고, 콜백 호출 시 임시 키 자격 증명을 반환합니다. 임시 키 자격 증명이 만료되면 다시 해당 콜백을 호출합니다.

다음은 자주 사용하는 일부 인터페이스 예시입니다. 자세한 초기화 방법은 [demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo/demo.js) 예시를 참고하십시오.

### 객체 업로드

간편 업로드는 용량이 작은 파일을 업로드하는 데 적합합니다. 큰 파일은 멀티파트 업로드 인터페이스를 사용하십시오. 자세한 내용은 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31538) 문서를 참고하십시오.

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드 */
    Key: 'exampleobject',              /* 필수 */
    StorageClass: 'STANDARD',
    Body: fileObject, // 파일 객체 업로드
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### 객체 리스트 조회

[//]: # ".cssg-snippet-get-bucket"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드 */
    Prefix: 'a/',           /* 옵션 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### 객체 다운로드

> !이 인터페이스는 객체 콘텐츠를 가져오는 데 사용합니다. 브라우저에서 파일 다운로드 요청이 필요한 경우 cos.getObjectUrl을 통해 url을 획득하여 브라우저 다운로드를 트리거할 수 있습니다. 자세한 내용은 [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31540) 문서를 참고하십시오.

[//]: # ".cssg-snippet-get-object"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드 */
    Key: 'exampleobject',              /* 필수 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

### 객체 삭제

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드 */
    Key: 'exampleobject'        /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```
