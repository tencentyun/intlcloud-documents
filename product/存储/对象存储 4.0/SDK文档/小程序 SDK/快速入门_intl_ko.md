## 다운로드 및 설치

### 관련 리소스

미니 프로그램 SDK 리소스 다운로드 주소: [GitHub 다운로드](https://github.com/tencentyun/cos-wx-sdk-v5).

### 환경 의존

WeChat 미니 프로그램 환경에 적합합니다.

### SDK 설치
미니 프로그램 SDK는 수동 설치 및 npm 설치의 두 가지 방식이 있으며 구체적인 설치 방법은 다음과 같습니다.

- 수동 설치
소스 코드의 [cos-wx-sdk-v5.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/lib/cos-wx-sdk-v5.js)를 자신의 미니 프로그램 코드 디렉터리에 복사하고 코드는 상대 경로를 통해 인용할 수 있습니다.
```shell
var COS = require('./cos-wx-sdk-v5.js')
```
- npm 설치
미니 프로그램 코드가 webpack을 사용하여 패키지된 경우 npm을 통해 의존을 설치하면 됩니다.
```shell
npm install cos-wx-sdk-v5
```
그 중 미니 프로그램 코드는 `var COS = require('cos-wx-sdk-v5');`를 사용하여 인용합니다.

### 사전 준비

1. [COS 콘솔](https://console.cloud.tencent.com/cos4)에 로그인하여 버킷을 생성하고 Bucket(버킷 이름) 및 Region(지역 이름)을 획득합니다.
2. 콘솔의 [키 관리](https://console.cloud.tencent.com/capi)를 통해 프로젝트의 SecretId와 SecretKey를 획득합니다.

#### 서명 계산

서명 계산을 프런트 엔드에 진행하면 SecretId 및 SecretKey가 노출될 수 있으므로 서명 계산 과정은 백 엔드에 두고 진행해야 합니다. 프런트 엔드는 ajax를 통해 임시 키를 백 엔드로 가져옵니다. 정식 배포 시에는 백 엔드에 자신의 웹사이트 자체에 권한 검증 레이어를 추가하십시오.

여기서는 PHP 및 Node.js의 [서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/)를 제공하며 기타 언어는 임시 키를 사용합니다. [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)에서 자세한 내용을 참조하십시오.

## 시작 가이드

### 초기화

```js
var cos = new COS({
    // ForcePathStyle: true, // 여러 버킷을 사용한 경우 후위식을 통해 구성된 화이트리스트 도메인 이름 수량을 줄일 수 있습니다. 요청 시 소재 지역 도메인 이름을 사용합니다
    getAuthorization: function (options, callback) {
        // 비동기 서명 획득
        wx.request({
            url: 'https://example.com/sts.php',
            data: {
                Method: options.Method,
                Key: options.Key
            },
            dataType: 'text',
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    ExpiredTime: data.expiredTime, // SDK는 ExpiredTime 시간 전에 다시 getAuthorization을 호출하지 않습니다
                });
            }
        });
    }
});
```

초기화 방법의 자세한 내용은 [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-sdk.js) 예시를 참조하십시오.

### 버킷 생성

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
}, function (err, data) {
    console.log(err || data);
});
```

>!미니 프로그램에서 버킷 생성을 해야 하지만 버킷 이름을 알 수 없을 경우 버킷 이름을 도메인 이름 화이트리스트에 추가할 수 없습니다. 관련 처리 조치는 [FAQ](https://cloud.tencent.com/document/product/436/30746#.E5.B0.8F.E7.A8.8B.E5.BA.8F.E9.87.8C.E8.AF.B7.E6.B1.82.E5.A4.9A.E4.B8.AA.E5.9F.9F.E5.90.8D.EF.BC.8C.E6.88.96.E8.80.85.E5.AD.98.E5.82.A8.E6.A1.B6.E5.90.8D.E7.A7.B0.E4.B8.8D.E7.A1.AE.E5.AE.9A.EF.BC.8C.E6.80.8E.E4.B9.88.E8.A7.A3.E5.86.B3.E7.99.BD.E5.90.8D.E5.8D.95.E9.85.8D.E7.BD.AE.E5.92.8C.E9.99.90.E5.88.B6.E9.97.AE.E9.A2.98.EF.BC.9F)를 참조하십시오.

### 버킷 리스트 조회

```js
cos.getService(function (err, data) {
    console.log(err || data);
});
```

### 업로드 객체

미니 프로그램 업로드 API wx.uploadFile은 POST 요청만 지원합니다. SDK 업로드 파일은 postObject API를 사용해야 합니다. 미니 프로그램 안에서 파일 업로드 API만 필요한 경우 SDK를 인용하지 않는 것이 좋습니다. 간단한 예시는 [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js)를 참조하십시오.

```js
// 먼저 파일을 선택하여 임시 경로를 가져옵니다
wx.chooseImage({
    count: 1, // 기본값은 9
    sizeType: ['original'], // 원본 이미지와 압축 이미지 중에서 지정할 수 있으며 기본으로 원본 이미지입니다
    sourceType: ['album', 'camera'], // 소스를 앨범 또는 카메라 중에서 지정할 수 있으며 기본값은 둘 다입니다
    success: function (res) {
        var filePath = res.tempFiles[0].path;
        var filename = filePath.substr(filePath.lastIndexOf('/') + 1);
        cos.postObject({
            Bucket: 'examplebucket-1250000000',
            Region: 'ap-beijing',
            Key: filename,
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
    Prefix: 'exampledir/',
}, function (err, data) {
    console.log(err || data);
});
```

### 객체 획득 Url

```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.png',
}, function (err, data) {
    console.log(err || data.Url);
});
```

### 객체에 파일 내용 업로드

텍스트 내용 업로드는 putObject API를 통해 완료할 수 있으며 해당 API는 실제로 wx.request API를 호출합니다.

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.txt',
    Body: 'hello',
    onProgress: function (info) {
        console.log(JSON.stringify(info));
    }
}, function (err, data) {
    console.log(err || data);
});
```

### 객체의 텍스트 내용 읽기

```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.txt',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### 객체 삭제

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: '1.png',
}, function (err, data) {
    console.log(err || data.Body);
});
```

## FAQ
미니 프로그램 SDK 사용 중 질문이 있는 경우 [FAQ](https://cloud.tencent.com/document/product/436/30746#.E5.B0.8F.E7.A8.8B.E5.BA.8F.E9.87.8C.E8.AF.B7.E6.B1.82.E5.A4.9A.E4.B8.AA.E5.9F.9F.E5.90.8D.EF.BC.8C.E6.88.96.E8.80.85.E5.AD.98.E5.82.A8.E6.A1.B6.E5.90.8D.E7.A7.B0.E4.B8.8D.E7.A1.AE.E5.AE.9A.EF.BC.8C.E6.80.8E.E4.B9.88.E8.A7.A3.E5.86.B3.E7.99.BD.E5.90.8D.E5.8D.95.E9.85.8D.E7.BD.AE.E5.92.8C.E9.99.90.E5.88.B6.E9.97.AE.E9.A2.98.EF.BC.9F) 문서의 미니 프로그램 부분을 참조하십시오.


## 관련 문서

완전한 문서는 보완 중이며 현재 미니 프로그램은 멀티파트 관련 API를 지원하지 않습니다. 업로드, 다운로드 관련 기능을 사용해야 할 경우 [소스 코드](https://github.com/tencentyun/cos-wx-sdk-v5) 및 [demo](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/demo/demo-no-sdk.js)를 참조하십시오. 기타 API 문서는 JavaScript SDK의 [API 문서](https://cloud.tencent.com/document/product/436/12260)를 참조하십시오.
