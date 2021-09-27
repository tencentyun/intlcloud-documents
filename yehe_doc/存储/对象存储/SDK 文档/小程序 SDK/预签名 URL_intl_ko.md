## 개요

미니프로그램 SDK는 서명 계산, 객체 URL과 사전 서명된 URL 요청을 가져오기 등 예시를 제공합니다.

## 서명 계산

COS XML API의 요청에서 프라이빗 리소스 작업은 모두 현재 요청이 합법인지 판단할 자격 증명 Authorization이 필요합니다.

자격 증명을 사용하는 방식에는 두 가지가 있습니다.

1. header 매개변수에서 사용, 필드 이름: authorization
2. url 매개변수에서 사용, 필드 이름: sign

COS.getAuthorization 방법은 자격 증명(Authorization) 계산에 사용되며, 이는 요청의 유효성 인증에 사용되는 서명 정보입니다.

>! 해당 방법은 프런트 엔드 디버깅 시에만 사용하는 것을 권장합니다. 프로젝트가 온라인 상태일 경우, 키가 노출될 리스크가 있기 때문에 프런트 엔드를 사용해 서명을 계산하는 방법은 권장하지 않습니다.
>

#### 사용 예시

객체 다운로드의 자격 증명 획득:

[//]: # (.cssg-snippet-get-authorization)
```js
// SECRETID와 SECRETKEY는 https://console.cloud.tencent.com/cam/capi에 로그인하여 조회 및 관리하십시오.
var Authorization = COS.getAuthorization({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
    Method: 'get',
    Key: 'picture.jpg',
    Expires: 60,
    Query: {},
    Headers: {}
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId  | 사용자의 SecretId                                              | String | 예   |
| SecretKey | 사용자의 SecretKey                                             | String | 예   |
| Method    | 작업 방법. 예: GET, POST, DELETE, HEAD 등 HTTP 방법         | String | 예   |
| Key       | 객체 키(Object의 이름). 객체는 버킷에 있는 고유 식별자입니다.<br><li>**파일에 대한 요청 작업인 경우 파일명이자 필수 매개변수입니다.**<br><li>버킷에 대한 작업인 경우 빈칸으로 표시됩니다. | String | 아니요   |
| Query     | 요청 query 매개변수 객체                                        | Object | 아니요   |
| Headers   | 요청 header 매개변수 객체                                       | Object | 아니요   |
| Expires   | 서명 만료 시간(초). 기본값: 900초                                  | Number | 아니요   |

#### 반환값 설명

반환값은 계산으로 얻은 자격 증명 문자열 authorization입니다.

## 사전 서명된 URL 요청 가져오기

#### 업로드 요청 설명

POST Object 인터페이스를 통해서만 미니프로그램에 파일을 업로드할 수 있습니다. 여기서 가져온 사전 서명된 URL은 POST Object 인터페이스에 적합하지 않습니다. 직접 파일을 업로드해야 할 경우, [미니프로그램 다이렉트 업로드 사례](https://intl.cloud.tencent.com/document/product/436/30934) 가이드를 참고하십시오.

#### 요청 예시 다운로드

예시1: 서명이 없는 객체의 Url 획득

[//]: # (.cssg-snippet-get-presign-download-url-nosign)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
    Sign: false
});
```

예시2: 서명이 있는 객체의 Url 획득

[//]: # (.cssg-snippet-get-presign-download-url)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg'
});
```

예시3: callback을 통해 서명이 있는 Url 획득

> ?서명 과정이 비동기화 가져오기인 경우, callback을 통해 서명이 있는 Url을 획득해야 합니다.

[//]: # (.cssg-snippet-get-presign-download-url-callback)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
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
    Region: 'ap-beijing',
    Key: 'picture.jpg',
    Sign: true,
    Expires: 3600, // 단위: 초
}, function (err, data) {
    console.log(err || data.Url);
});
```

예시5: 객체 Url을 가져와 객체 다운로드

[//]: # (.cssg-snippet-get-presign-download-url-then-fetch)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
    Sign: true
}, function (err, data) {
    if (!err) return console.log(err);
    wx.downloadFile({
        url: data.Url, // url 도메인을 다운로드 화이트리스트로 추가
        success (res) {
            console.log(res.statusCode, res.tempFilePath);
        },
        fail: function (err) {
            console.log(err);
        },
    });
});
```



#### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 입력 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket                      | 버킷의 이름. 이름 생성 형식은 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | 예   |
| Key     | 객체 키(Object의 이름). 객체는 버킷에 있는 고유 식별자입니다.<br><li>**파일에 대한 요청 작업인 경우 파일명이자 필수 매개변수입니다.**<br><li>버킷에 대한 작업인 경우 빈칸으로 표시됩니다. | String  | 예   |
| Sign    | 서명이 있는 Url 반환 여부. 기본값: true                          | Boolean | 아니요   |
| Protocol    | ‘http:’ 또는 ‘https:’를 선택할 수 있습니다. 기본값: ‘http:’(콜론 포함)                          | String | 아니요   |
| Domain    | 버킷 액세스 도메인. 기본값: {BucketName-APPID}.cos.{Region}.myqcloud.com     | String | 아니요   |
| Method  | 작업 방법. 예: GET, POST, DELETE, HEAD 등 HTTP 방법. 기본값: GET | String  | 아니요   |
| - Query    | 서명 계산에 참여하는 query 매개변수 객체. {key: 'val'} 의 형식               | Object   | 아니요   |
| Headers | 서명 계산에 참여하는 header 매개변수 객체                               | Object  | 아니요   |
| Expires | 서명 만료 시간(초). 기본값: 900초                                  | Number  | 아니요   |

#### 반환값 설명

반환값은 하나의 문자열로 다음과 같은 두 가지 상황이 있습니다.

1. 서명 계산에서 동기화 계산이 가능한 경우(예: SecretId와 SecretKey를 인스턴스화 전송), 기본적으로 서명이 있는 url을 반환합니다.
2. 그렇지 않은 경우 서명이 없는 url을 반환합니다.

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| data   | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| - Url  | 계산 후 얻은 Url                                               | String |


