## 다운로드 및 설치

#### 관련 리소스

- COS 서비스의 XML JS SDK 리소스 github 주소: [XML Node.js SDK](https://github.com/tencentyun/cos-nodejs-sdk-v5).
- SDK 고속 다운로드 주소: [XML Node.js SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-nodejs-sdk-v5/latest/cos-nodejs-sdk-v5.zip).
- 예시 Demo 다운로드 주소: [XML Node.js SDK Demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/NodeJS)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.

>? SDK 사용 시 함수 또는 메소드 없음 등 오류가 발생하였을 경우, 먼저 SDK를 최신 버전으로 업데이트한 후 재시도하십시오.
>

#### 환경 종속

1. SDK를 사용하려면 사용자의 실행 환경에 nodejs 및 npm이 포함되어 있어야 하며, 그중 nodejs 버전은 ≥ 6을 요구합니다.
2. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인해 버킷을 생성한 후 버킷 이름과 [리전 이름](https://intl.cloud.tencent.com/document/product/436/6224)을 획득합니다.
3. [CAM 콘솔](https://console.cloud.tencent.com/capi)에 로그인해 프로젝트의 SecretId와 SecretKey를 획득합니다.

> ?본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭에 대한 의미와 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.

#### SDK 설치

npm으로 SDK 환경 설치: [npm 주소](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```bash
npm i cos-nodejs-sdk-v5 --save
```

## 사용하기

### 초기화

#### 영구 키로 초기화

CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 SecretId와 SecretKey를 획득합니다.
SecretId, SecretKey, Bucket, Region을 실제 개발 환경 값으로 수정하고 파일 업로드를 테스트합니다. 아래 예시 코드를 참고하십시오.

[//]: # (.cssg-snippet-global-init)
```js
// SECRETID와 SECRETKEY는 https://console.cloud.tencent.com/cam/capi에 로그인하여 조회 및 관리하십시오.
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY'
});
```

#### 임시 키로 초기화 하기

임시 키 생성 및 사용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오. Node.js SDK는 임시 키 전송을 통한 초기화 작업을 지원합니다. 아래의 예시 코드를 참고하십시오.

[//]: # (.cssg-snippet-global-init-sts)
```js
var request = require('request');
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 임시 키 비동기 획득
        request({
            url: 'https://example.com/sts',
            data: {
                // options에서 필요한 매개변수 획득 가능
            }
        }, function (err, response, body) {
            try {
                var data = JSON.parse(body);
                var credentials = data.credentials;
            } catch(e) {}
            if (!data || !credentials) return console.error('credentials invalid');
            callback({
                TmpSecretId: credentials.tmpSecretId,        // 임시 키의 tmpSecretId
                TmpSecretKey: credentials.tmpSecretKey,      // 임시 키의 tmpSecretKey
                SecurityToken: credentials.sessionToken, // 임시 키의 sessionToken
                ExpiredTime: data.expiredTime,               // 임시 키 유효하지 않은 타임스탬프. 임시 키 신청 시 타임스탬프에 durationSeconds를 추가합니다.
            });
        });
    }
});
```

다음은 자주 사용하는 일부 인터페이스 예시입니다. 자세한 초기화 방법은 [demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/demo.js) 예시를 참고하십시오.

### 설정 항목

#### 구조 함수 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| SecretId               | 사용자의 SecretId                                              | String   | Yes   |
| SecretKey              | 사용자의 SecretKey. 키가 노출되지 않도록 프런트 엔드 디버깅 시에만 사용하는 것을 권장합니다.       | String   | Yes   |
| FileParallelLimit      | 동일한 인스턴스에 업로드하는 파일의 동시 전송 수. 기본값: 3                        | Number   | No   |
| ChunkParallelLimit     | 동일한 업로드 파일의 멀티파트 동시 전송 수. 기본값: 3                          | Number   | No   |
| ChunkRetryTimes        | 멀티파트 업로드 및 멀티파트 복사 시 오류가 발생하여 재시도한 횟수. 기본값: 3(첫 번째 시도를 더하면 요청은 총 4번) | Number   | No   |
| ChunkSize              | 멀티파트 업로드 시 각 파트의 바이트 수. 기본값: 1048576(1MB)           | Number   | No   |
| SliceSize              | uploadFiles로 일괄 업로드 시, 파일 크기가 해당 값보다 크면 멀티파트 업로드를 사용하고, 그렇지 않을 경우 간편 업로드를 호출합니다. 단위: Byte, 기본값: 1048576(1MB) | Number   | No   |
| CopyChunkParallelLimit | 멀티파트 복사 작업 중에 멀티파트 업로드한 동시 전송 수. 기본값: 20             | Number   | No   |
| CopyChunkSize          | sliceCopyFile로 파일 멀티파트 복사 시, 각 파트의 바이트 수. 기본값: 10485760(10MB) | Number   | No   |
| CopySliceSize          | sliceCopyFile로 파일 멀티파트 복사 시, 파일 크기가 해당 값보다 크면 멀티파트 복사를 사용하고, 그렇지 않을 경우 간편 복사를 호출합니다. 기본값: 10485760(10MB) | Number   | No   |
| ProgressInterval       | 업로드 진행률 콜백 방법 onProgress의 콜백 빈도. 단위: ms, 기본값: 1000 | Number   | No   |
| Protocol               | 요청 시 사용하는 프로토콜. 옵션 항목으로 `https:`와 `http:`가 있습니다. 기본적으로 현재 페이지가 `http:`인 경우 `http:`를 사용하고, 아닌 경우 `https:`를 사용합니다. | String   | No   |
| ServiceDomain          | getService 방법 호출 시 요청하는 도메인. 예: `service.cos.myqcloud.com` | String   | No   |
| Domain                 | 버킷 및 객체 작업 API 호출 시 요청 도메인을 사용자 정의합니다.<br>`"{Bucket}.cos.{Region}.myqcloud.com" `과 같은 템플릿을 사용할 수 있으며, API 호출 시 매개변수로 전달하는 Bucket 및 Region으로 변경할 수 있습니다. | String   | No   |
| UploadQueueSize        | 업로드 큐 최대 길이. 작업이 큐 크기를 초과하고, 실패/완료/취소 상태인 경우 정리합니다. 기본값: 1000 | Number   | No   |
| ForcePathStyle         | 강제 사용 후 확장명 모드로 요청 발송. 확장명 모드의 Bucket은 도메인 뒤의 pathname에 넣고, Bucket은 서명 pathname 계산을 추가합니다. 기본값: false | Boolean  | No   |
| UploadCheckContentMd5  | 강제로 업로드한 파일도 Content-MD5 검증. 파일에 대해 Body를 요청하여 md5를 계산하고 header의 Content-MD5 필드에 올립니다. 기본값: false | Boolean  | No   |
| Timeout                | 타임아웃 시간. 단위: 밀리초. 기본값: 0. 즉 타임아웃 시간을 설정하지 않습니다.               | Number   | No   |
| KeepAlive              | 다수의 요청이 모두 TCP 연결을 사용. 기본값: true. 동시 요청량이 많은 경우 활성화 권장   | Boolean   | No   |
| StrictSsl              | HTTPS 인증서 엄격 검증. 기본값: true | Boolean | No   |
| Proxy                  | 요청 시 HTTP 프록시 사용. 예: `http://127.0.0.1:8080`   | String | No   |
| getAuthorization       | 서명을 획득하는 콜백 방법. SecretId, SecretKey가 없는 경우 이 매개변수는 필수입니다. | Function | No   |


#### getAuthorization 콜백 함수 설명의 함수 설명(형식1 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization 함수 설명:

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | -------- |
| options  | 임시 키에 필요한 매개변수 객체 획득                                   | Object   |
| - Bucket | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String   |
| - Region | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   |
| callback | 임시 키 획득 후 리턴 방법                                 | Function |

임시 키 획득 후 callback은 하나의 객체를 리턴합니다. 리턴 객체의 속성 리스트는 다음과 같습니다.

| 속성 이름            | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId       | 획득한 임시 키의 tmpSecretId                             | String | Yes   |
| TmpSecretKey      | 획득한 임시 키의 tmpSecretKey                            | String | Yes   |
| SecurityToken | 획득한 임시 키의 sessionToken. 해당 header의 x-cos-security-token 필드 | String | Yes   |
| StartTime         | 키를 획득한 시작 시간. 즉 획득한 시각의 타임스탬프. 단위: 초. startTime. 예: 1580000000. 서명 시작 시간에 사용됩니다. 해당 매개변수를 전송하면 프런트 엔드 시간의 편차로 인한 서명 만료 문제를 방지할 수 있습니다. | String | No   |
| ExpiredTime       | 획득한 임시 키의 expiredTime. 타임아웃 시간의 타임스탬프. 단위: 초. 예: 1580000900 | String | Yes   |

#### getAuthorization 콜백 함수 설명(형식2 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization 함수 설명:

| 매개변수 이름     | 매개변수 설명                                                     | 유형     |
| ---------- | ------------------------------------------------------------ | -------- |
| options    | 서명에 필요한 매개변수 객체 획득                                       | Object   |
| - Method   | 현재 요청한 Method                                            | String   |
| - Pathname | 요청 경로. 서명 계산에 사용                                       | String   |
| - Key      | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   |
| - Query    | 현재 요청한 query 매개변수 객체. {key: 'val'} 의 형식               | Object   |
| - Headers  | 현재 요청한 header 매개변수 객체. {key: 'val'}의 형식              | Object   |
| callback   | 임시 키 획득 후 콜백                                     | Function |

getAuthorization 계산 완료 후 callback 리턴 매개변수는 두 가지 형식을 지원합니다.
형식1: 자격 증명 문자열 Authorization 리턴.
형식2: 하나의 객체 리턴. 리턴 속성 리스트는 다음과 같습니다.


| 속성 이름            | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | 계산 후 얻은 서명 문자열                                         | String | Yes   |
| SecurityToken | 획득한 임시 키의 sessionToken. 해당 header의 x-cos-security-token 필드 | String | No   |

#### 자격 증명 획득

인스턴스 자체 자격 증명은 인스턴스화 중에 전송된 매개변수를 통해 제어하거나 획득할 수 있습니다. 획득 방법은 세 가지입니다.

1. 인스턴스화 시 SecretId, SecretKey를 전송합니다. 서명이 필요할 때마다 인스턴스 내부에서 계산합니다.
2. 인스턴스화 시 getAuthorization 콜백을 전송합니다. 서명이 필요할 때마다 해당 콜백으로 계산하고, 서명을 인스턴스로 반환합니다.
3. 인스턴스화 시 getSTS 콜백을 전송합니다. 임시 키가 필요할 때마다 해당 콜백을 통해 돌아가 인스턴스에 반환합니다. 요청할 때마다 인스턴스 내부에서 임시 키로 계산하여 서명을 얻습니다.

### 버킷 생성

[//]: # (.cssg-snippet-put-bucket)
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

### 버킷 리스트 조회

[//]: # (.cssg-snippet-get-service)
```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### 객체 업로드

해당 인터페이스는 용량이 작은 파일을 업로드하는 데 적합합니다. 큰 파일은 멀티파트 업로드 인터페이스를 사용하십시오. 자세한 내용은 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31710) 문서를 참고하십시오.

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: fs.createReadStream('./exampleobject'), // 파일 객체 업로드
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### 객체 리스트 조회

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

### 객체 다운로드

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

### 객체 삭제

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject'       /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```
