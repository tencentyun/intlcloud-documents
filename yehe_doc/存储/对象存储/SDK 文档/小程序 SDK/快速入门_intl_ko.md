## 다운로드 및 설치

#### 관련 리소스

- COS의 XML 미니프로그램 SDK 소스 코드 다운로드 주소: [XML 미니프로그램 SDK](https://github.com/tencentyun/cos-wx-sdk-v5).
- SDK 고속 다운로드 주소: [XML 미니프로그램 SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-wx-sdk-v5/latest/cos-wx-sdk-v5.zip).
- 예시 Demo 다운로드 주소: [XML 미니프로그램 SDK Demo](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/MiniProgram)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [미니프로그램 SDK FAQ](https://intl.cloud.tencent.com/document/product/436/38958)를 참고하십시오.

>? SDK 사용 시 함수 또는 메소드 없음 등 오류가 발생하였을 경우, 먼저 SDK를 최신 버전으로 업데이트한 후 재시도하십시오.
>

#### 환경 종속

1. 해당 SDK는 WeChat 미니프로그램 환경에만 적용됩니다.
2. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인해 버킷을 생성한 후 버킷 이름과 [리전 정보](https://intl.cloud.tencent.com/document/product/436/6224)를 획득합니다.
3. [CAM 콘솔](https://console.cloud.tencent.com/capi)에 로그인해 프로젝트의 SecretId와 SecretKey를 획득합니다.

>? 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭에 대한 의미와 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
>

#### SDK 설치

미니프로그램 SDK 설치 방법은 수동 설치와 npm 설치 두 가지입니다. 구체적인 설치 방법은 다음과 같습니다.

#### 수동 설치

소스 코드 파일의 [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js)를 사용자의 미니프로그램 코드와 루트 디렉터리의 임의 경로로 복사하고, 상대 경로를 참고합니다.

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

#### npm 설치

미니프로그램 코드가 webpack 패키지를 사용한 경우, npm을 통해 종속 설치합니다.

```plaintext
npm install cos-wx-sdk-v5
```

그 중 미니프로그램 코드는 `var COS = require('cos-wx-sdk-v5');`를 사용하여 참고합니다.

## 사용하기

### 미니프로그램 도메인 화이트리스트 설정

미니프로그램에서 COS를 요청하면 [WeChat 공식 계정 플랫폼](https://mp.weixin.qq.com)에 로그인해 [개발] > [개발 설정] > [서버 도메인]을 선택하고 도메인 화이트리스트를 설정해야 합니다. SDK는 두 개의 인터페이스를 사용합니다.

1. cos.postObject는 wx.uploadFile 방법을 사용합니다.
2. 기타 방법은 wx.request 방법을 사용합니다.

해당 화이트리스트에서 COS 도메인을 설정해야 합니다. 화이트리스트 형식은 두 가지가 있습니다.

1. 표준 요청인 경우 버킷 도메인을 화이트리스트로 설정할 수 있습니다. 예:
   `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.
2. 미니프로그램에서 사용하는 버킷이 많은 경우 확장명을 선택하여 COS를 요청할 수 있습니다. SDK 인스턴스화 시 `ForcePathStyle: true`를 전송해야 합니다. 해당 방식은 리전 도메인을 화이트리스트로 설정해야 합니다. 예: `cos.ap-guangzhou.myqcloud.com`.

### 초기화

```js
var COS = require('./lib/cos-wx-sdk-v5.js')
```

```js
var cos = new COS({
    // ForcePathStyle: true, // 많은 버킷을 사용한 경우 확장명을 열어 설정한 화이트리스트 수를 줄이면 요청 시 리전 도메인을 사용합니다.
    getAuthorization: function (options, callback) {
        // 임시 키 비동기 획득
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                bucket: options.Bucket,
                region: options.Region,
            },
            dataType: 'json',
            success: function (result) {
                var data = result.data;
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    // 사용자 브라우저 로컬 시간과의 편차가 너무 커 서명에 오류가 발생하지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다.
                    StartTime: data.startTime, // 타임스탬프. 단위: 초. 예: 1580000000
                    ExpiredTime: data.expiredTime, // 타임스탬프. 단위: 초. 예: 1580000900
                });
            }
        });
    }
});

// 이어서 cos 인스턴스를 통해 COS 요청을 호출할 수 있습니다.
// TODO
```

### 설정 항목

#### 사용 예시

COS SDK 인스턴스 한 개를 생성합니다. COS SDK는 다음과 같은 형식 생성을 지원합니다.

- 형식1(권장): 백그라운드에서 임시 키를 획득하여 프런트 엔드로 보내고, 프런트 엔드에서 서명을 계산합니다.

```js
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버 JS와 PHP 예시: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // 서버의 기타 언어는 COS STS SDK: https://github.com/tencentyun/qcloud-cos-sts-sdk를 참고하십시오.
        // STS 상세 문서 가이드는 https://intl.cloud.tencent.com/document/product/436/14048을 참고하십시오.
        wx.request({
            url: 'https://example.com/server/sts.php',
            data: {
                // options에서 필요한 매개변수 획득 가능
            },
            success: function (result) {
                var data = result.data;
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    // 사용자 브라우저 로컬 시간과의 편차가 너무 커 서명에 오류가 발생하지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다.
                    StartTime: data.startTime, // 타임스탬프. 단위: 초. 예: 1580000000
                    ExpiredTime: data.expiredTime, // 타임스탬프. 단위: 초. 예: 1580000900
                });
            }
        });
    }
});
```
>? 임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.
>

- 형식2(권장): 세밀한 권한 제어. 백그라운드에서 임시 키를 획득하여 프런트 엔드로 보냅니다. 동일한 요청을 하는 경우에만 프런트 엔드가 임시 키를 재사용합니다. 백그라운드는 Scope을 통해 권한을 세밀하게 제어합니다.

```js
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버 예시: https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
        wx.request({
            url: 'https://example.com/server/sts-scope.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                var credentials = data && data.credentials;
                if (!data || !credentials) return console.error('credentials invalid');
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
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

>? 임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.
>

- 형식3(권장하지 않음): 매번 프런트 엔드가 요청하기 전에 getAuthorization을 통해 서명을 획득하고, 백그라운드는 고정 키 또는 임시 키를 사용해 서명을 계산하여 프런트 엔드로 반환해야 합니다. 해당 형식의 멀티파트 업로드 권한은 제어하기 쉽지 않기 때문에 사용을 권장하지 않습니다.

```js
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버에서 서명을 획득합니다. 해당 언어의 COS SDK: https://cloud.tencent.com/document/product/436/6474를 참고하십시오.
        // 주의사항: 보안 리스크가 있기 때문에 백그라운드는 method, pathname을 통해 권한을 엄격히 제어해야 합니다. 예: put / 비허용 등
        wx.request({
            url: 'https://example.com/server/auth.php',
            data: JSON.stringify(options.Scope),
            success: function (result) {
                var data = result.data;
                if (!data || !data.authorization) return console.error('authorization invalid');
                callback({
                    Authorization: data.authorization,
                    // XCosSecurityToken: data.sessionToken, // 임시 키를 사용하는 경우, sessionToken을 XCosSecurityToken에 전송해야 합니다.
                });
            }
        });
    },
});
```

- 형식4(권장하지 않음): 프런트 엔드는 고정 키를 사용해 서명을 계산합니다. 해당 형식은 프런트 엔드 디버깅에 적합하며, 사용 시 키가 노출되지 않도록 주의하십시오.

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
| SecretId               | 사용자의 SecretId                                              | String   | No   |
| SecretKey              | 사용자의 SecretKey. 키가 노출되지 않도록 프런트 엔드 디버깅 시에만 사용하는 것을 권장합니다.       | String   | No   |
| FileParallelLimit      | 동일한 인스턴스에 업로드하는 파일의 동시 전송 수. 기본값: 3                        | Number   | No   |
| ChunkParallelLimit     | 동일한 업로드 파일의 멀티파트 동시 전송 수. 기본값: 3                          | Number   | No   |
| ChunkRetryTimes        | 멀티파트 업로드 및 멀티파트 복사 시 오류가 발생하여 재시도한 횟수. 기본값: 3(첫 번째 시도를 더하면 요청은 총 4번) | Number   | No   |
| ChunkSize              | 멀티파트 업로드 시 각 파트의 바이트 수. 기본값: 1048576(1MB)           | Number   | No   |
| SliceSize              | uploadFiles로 일괄 업로드 시, 파일 크기가 해당 값보다 크면 멀티파트 업로드 sliceUploadFile을 사용하고, 그렇지 않을 경우 간편 업로드 putObject를 사용합니다. 기본값: 1048576(1MB) | Number   | No   |
| CopyChunkParallelLimit | 멀티파트 복사 작업 중에 멀티파트 업로드한 동시 전송 수. 기본값: 20             | Number   | No   |
| CopyChunkSize          | sliceCopyFile로 파일 멀티파트 복사 시, 각 파트의 바이트 수. 기본값: 10485760(10MB) | Number   | No   |
| CopySliceSize          | sliceCopyFile로 파일 멀티파트 복사 시, 파일 크기가 해당 값보다 크면 멀티파트 복사 sliceCopyFile을 사용하고, 그렇지 않을 경우 간편 복사 putObjectCopy를 사용합니다. 기본값: 10485760(10MB) | Number   | No   |
| ProgressInterval       | 업로드 진행률 콜백 방법 onProgress의 콜백 빈도. 단위: ms, 기본값: 1000 | Number   | No   |
| Protocol               | 요청 시 사용하는 프로토콜. 옵션 항목으로 `https:`와 `http:`가 있습니다. 기본적으로 현재 페이지가 `http:`인 경우 `http:`를 사용하고, 아닌 경우 `https:`를 사용합니다. | String   | No   |
| ServiceDomain          | getService 방법 호출 시 요청하는 도메인. 예: `service.cos.myqcloud.com` | String   | No   |
| Domain                 | 버킷 및 객체 작업 API 호출 시 요청 도메인을 사용자 정의합니다. `"{Bucket}.cos.{Region}.myqcloud.com" `과 같은 템플릿을 사용할 수 있으며, API 호출 시 매개변수로 전달하는 Bucket 및 Region으로 변경할 수 있습니다. | String   | No   |
| UploadQueueSize        | 업로드 큐 최대 길이. 초과된 작업이 waiting, checking, uploading 상태가 아닌 경우 정리합니다. 기본값: 10000 | Number   | No   |
| ForcePathStyle         | 강제 사용 후 확장명 모드로 요청 발송. 확장명 모드의 Bucket에 도메인 뒤의 pathname을 넣고, 서명 pathname 계산을 추가합니다. 기본값: false | Boolean  | No   |
| UploadCheckContentMd5  | 파일을 강제 업로드하여 Content-MD5 검사. 파일에 대해 Body를 요청하여 md5를 계산하고 header의 Content-MD5 필드에 올립니다. 기본값: false | Boolean  | No   |
| getAuthorization       | 서명을 획득하는 콜백 방법. SecretId, SecretKey가 없는 경우 이 매개변수는 필수입니다. <br> **주의사항: 해당 콜백 방법은 인스턴스 초기화 시 전송되며, 인스턴스로 인터페이스를 호출해야 실행되어 서명을 획득합니다.** | Function | No   |

#### getAuthorization 콜백 함수 설명의 함수 설명(형식1 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization의 콜백 매개변수 설명:

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
| XCosSecurityToken | 획득한 임시 키의 sessionToken. 해당 header의 x-cos-security-token 필드 | String | Yes   |
| StartTime         | 키를 획득한 시작 시간. 즉 획득한 시각의 타임스탬프. 단위: 초. startTime. 예: 1580000000. 서명 시작 시간에 사용됩니다. 해당 매개변수를 전송하면 프런트 엔드 시간의 편차로 인한 서명 만료 문제를 방지할 수 있습니다. | String | No   |
| ExpiredTime       | 획득한 임시 키의 expiredTime. 타임아웃 시간의 타임스탬프. 단위: 초. 예: 1580000900 | String | Yes   |

#### getAuthorization 콜백 함수 설명(형식2 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization 함수 설명 및 콜백 매개변수 설명:

| 매개변수 이름     | 매개변수 설명                                                     | 유형     |
| ---------- | ------------------------------------------------------------ | -------- |
| options    | 서명에 필요한 매개변수 객체 획득                                       | Object   |
| - Method   | 현재 요청한 Method                                            | Object   |
| - Pathname | 요청 경로. 서명 계산에 사용                                       | String   |
| - Key      | 객체 키(Object의 이름). 객체는 버킷에 있는 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.<br> **주의사항: 인스턴스로 요청한 인터페이스가 객체 작업과 관련된 인터페이스가 아닐 경우, 해당 매개변수는 빈칸으로 표시됩니다.** | String   |
| - Query    | 현재 요청한 query 매개변수 객체. {key: 'val'} 의 형식               | Object   |
| - Headers  | 현재 요청한 header 매개변수 객체. {key: 'val'}의 형식              | Object   |
| callback   | 임시 키 획득 후 콜백                                     | Function |

getAuthorization 계산 완료 후 callback 리턴 매개변수는 두 가지 형식을 지원합니다.
형식1: 자격 증명 문자열 Authorization 리턴.
형식2: 하나의 객체 리턴. 리턴 속성 리스트는 다음과 같습니다.

| 속성 이름            | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | 계산 후 얻은 서명 문자열                                         | String | Yes   |
| XCosSecurityToken | 획득한 임시 키의 sessionToken. 해당 header의 x-cos-security-token 필드 | String | No   |

#### 자격 증명 획득

인스턴스 자체 인증 자격 증명은 인스턴스 시 전달한 매개변수를 통해 어떻게 획득할지 통제할 수 있습니다. 획득 방법은 세 가지입니다.

1. 인스턴스화 시 SecretId, SecretKey를 전송합니다. 서명이 필요할 때마다 인스턴스 내부에서 계산합니다.
2. 인스턴스화 시 getAuthorization 콜백을 전송합니다. 서명이 필요할 때마다 해당 콜백으로 계산하고, 서명을 인스턴스로 반환합니다.
3. 인스턴스화 시 getSTS 콜백을 전송합니다. 임시 키가 필요할 때마다 해당 콜백을 통해 돌아가 인스턴스에 반환합니다. 요청할 때마다 인스턴스 내부에서 임시 키로 계산하여 서명을 얻습니다.

다음은 자주 사용하는 일부 인터페이스 예시입니다. 자세한 초기화 방법은 [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/) 예시를 참고하십시오.

### 버킷 생성

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

>! 미니프로그램에서 버킷을 생성해야 하지만 버킷 이름을 모르는 경우, 버킷 이름을 도메인 화이트리스트로 설정할 수 없지만 확장명으로 호출할 수 있습니다. 관련 처리 조치는 [FAQ](https://intl.cloud.tencent.com/document/product/436/10687)를 참고하십시오.
>

### 버킷 리스트 조회

```js
cos.getService(function (err, data) {
    console.log(data && data.Buckets);
});
```

### 객체 업로드

미니프로그램 업로드 인터페이스 wx.uploadFile은 POST 요청만 지원합니다. SDK 파일 업로드는 postObject 인터페이스를 사용해야 합니다. 미니프로그램에서 파일 업로드 인터페이스만 사용해야 하는 경우 SDK를 참고하지 않는 것을 권장합니다. 간단한 예시는 [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js)를 참고하십시오.

```js
// 먼저 파일을 선택하고 임시 경로를 획득합니다.
wx.chooseImage({
    count: 1, // 기본값: 9
    sizeType: ['original'], // 원본 이미지 또는 압축 이미지를 지정할 수 있습니다. 기본값은 원본 이미지입니다.
    sourceType: ['album', 'camera'], // 출처를 갤러리 또는 카메라로 지정할 수 있습니다. 기본값은 둘 다입니다.
    success: function (res) {
        var filePath = res.tempFiles[0].path;
        var filename = filePath.substr(filePath.lastIndexOf('/') + 1);
        cos.postObject({
            Bucket: 'examplebucket-1250000000',
            Region: 'ap-beijing',
            Key: '타깃 경로/' + filename,
            FilePath: filePath,
            onProgress: function (info) {
                console.log(JSON.stringify(info));
            }
        }, function (err, data) {
            console.log(err || data);
        });
    }
});
```

### 객체 리스트 조회

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Prefix: 'exampledir/', // 여기서 열거한 파일 접두사를 전달합니다.
}, function (err, data) {
    console.log(err || data.Contents);
});
```

### 객체 다운로드

>! 이 인터페이스는 객체 콘텐츠를 가져오는 데 사용합니다. 브라우저에서 파일 다운로드 요청이 필요한 경우 cos.getObjectUrl을 통해 url을 획득하여 다시 브라우저 다운로드를 트리거할 수 있습니다. 자세한 내용은 [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31711) 문서를 참고하십시오.
>

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'exampleobject.txt',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### 객체 삭제

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
}, function (err, data) {
    console.log(err || data);
});
```
