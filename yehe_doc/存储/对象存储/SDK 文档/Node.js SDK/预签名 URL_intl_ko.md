## 소개

Node.js SDK는 객체 URL과 사전 서명된 URL 요청을 가져오는 인터페이스를 제공합니다. 자세한 내용은 본 문서의 설명과 예시를 참조하십시오.

## 서명 계산

COS XML API의 요청에서 프라이빗 리소스 작업은 모두 현재 요청이 합법인지 판단할 인증 자격 증명 Authorization이 필요합니다.

인증 자격 증명을 사용하는 방식에는 두 가지가 있습니다.

1. header 매개변수에서 사용, 필드 이름: authorization
2. url 매개변수에서 사용, 필드 이름: sign

COS.getAuthorization 방법은 인증 자격 증명(Authorization) 계산에 사용되며, 이는 요청의 유효성 인증에 사용되는 서명 정보입니다.

> !해당 방법은 프런트 엔드 디버깅 시에만 사용하는 것을 권장합니다. 프로젝트가 온라인 상태일 경우, 키가 노출될 리스크가 있기 때문에 프런트 엔드를 사용해 서명을 계산하는 방법은 권장하지 않습니다.

#### 사용 예시

파일 다운로드의 인증 자격 증명 획득:

[//]: # (.cssg-snippet-get-authorization)
```js
// SECRETID와 SECRETKEY는 https://console.cloud.tencent.com/cam/capi에 로그인하여 조회 및 관리하십시오.
var COS = require('cos-nodejs-sdk-v5');
var Authorization = COS.getAuthorization({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
    Method: 'get',
    Key: 'a.jpg',
    Expires: 60,
    Query: {},
    Headers: {}
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 입력 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId  | 사용자의 SecretId                                              | String | 예   |
| SecretKey | 사용자의 SecretKey                                             | String | 예   |
| Method    | 작업 방법. 예: get, post, delete, head 등 HTTP 방법           | String | 예   |
| Key       | 객체 키(Object의 이름). 객체는 버킷에 있는 고유 식별자입니다. **파일에 대한 요청 작업인 경우 파일명이자 필수 매개변수입니다**. 버킷에 대한 작업인 경우 빈칸으로 표시됩니다. | String | 아니요   |
| Query     | 요청 query 매개변수 객체                                        | Object | 아니요   |
| Headers   | 요청 header 매개변수 객체                                       | Object | 아니요   |
| Expires   | 서명 후 몇 초가 지나면 유효하지 않습니다. 기본값: 900초                                  | Number | 아니요   |

#### 반환값 설명

반환값은 계산으로 얻은 인증 자격 증명 문자열 authorization입니다.

## 사전 서명된 URL 요청 가져오기

### 다운로드 요청 예시

예시1: 서명이 없는 Object Url 획득

[//]: # (.cssg-snippet-get-presign-download-url-nosign)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: '1.jpg',
    Sign: false
});
```

예시2: 서명이 있는 Object Url 획득

[//]: # (.cssg-snippet-get-presign-download-url)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: '1.jpg'
});
```

예시3: 서명 과정이 비동기 획득인 경우, callback을 통해 서명이 있는 Url을 획득해야 합니다.

[//]: # (.cssg-snippet-get-presign-download-url-callback)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: '1.jpg',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

예시4: 링크 유효 시간 지정

[//]: # (.cssg-snippet-get-presign-download-url-expiration)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: '1.jpg',
    Sign: true,
    Expires: 3600, // 단위: 초
}, function (err, data) {
    console.log(err || data.Url);
});
```

예시5: 파일 Url을 가져와 객체 다운로드

[//]: # (.cssg-snippet-get-presign-download-url-then-fetch)
```js
var request = require('request');
var fs = require('fs');
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    console.log(data.Url);
    var req = request(data.Url, function (err, response, body) {
        console.log(err || body);
    });
    var writeStream = fs.createWriteStream(__dirname + '/1.jpg');
    req.pipe(writeStream);
});
```

### 업로드 요청 예시

예시1: 사전 서명된 Put Object를 가져와 Url 업로드

[//]: # (.cssg-snippet-get-presign-upload-url)
```js
var request = require('request');
var fs = require('fs');
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Method: 'PUT',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    console.log(data.Url);
    var readStream = fs.createReadStream(__dirname + '/1.jpg');
    var req = request({
        method: 'PUT',
        url: data.Url,
    }, function (err, response, body) {
        console.log(err || body);
    });
    readStream.pipe(req);
});
```

### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 입력 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String  | 예   |
| Region  | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String  | 예   |
| Key     | 객체 키(Object의 이름). 객체는 버킷에 있는 고유 식별자입니다. **파일에 대한 요청 작업인 경우 파일명이자 필수 매개변수입니다**. 버킷에 대한 작업인 경우 빈칸으로 표시됩니다. | String  | 예   |
| Sign    | 서명이 있는 Url 반환 여부                                       | Boolean | 아니요   |
| Protocol    | `http:` 또는 `https:`를 선택할 수 있습니다. 기본값: `http:`(콜론 포함)                         | String | 아니요   |
| Domain    | 버킷 액세스 도메인. 기본값: {BucketName-APPID}.cos.{Region}.myqcloud.com     | String | 아니요   |
| Method  | 작업 방법. 예: get, post, delete, head 등 HTTP 방법. 기본값: get | String  | 아니요   |
| Query   | 서명 계산에 참여하는 query 매개변수 객체                                | Object  | 아니요   |
| Headers | 서명 계산에 참여하는 header 매개변수 객체                               | Object  | 아니요   |
| Expires | 서명 후 몇 초가 지나면 유효하지 않습니다. 기본값: 900초                                  | Number  | 아니요   |

### 반환값 설명

반환값은 하나의 문자열로 다음과 같은 두 가지 상황이 있습니다.

1. 서명 계산에서 동기화 계산이 가능한 경우(예시: SecretId와 SecretKey를 인스턴스화 전송), 기본적으로 서명이 있는 url을 반환합니다.
2. 그렇지 않은 경우 서명이 없는 url을 반환합니다.

### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 완료 시 빈칸으로 표시됩니다. 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object |
| data   | 요청 완료 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| - Url  | 계산 후 얻은 Url                                               | String |
