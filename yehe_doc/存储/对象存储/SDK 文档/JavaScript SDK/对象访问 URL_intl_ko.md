## 소개

본 문서는 객체 액세스 URL을 획득하는 코드 예시를 제공합니다.

## 객체 액세스 URL 획득

#### 기능 설명

객체 액세스 URL을 조회합니다. 해당 인터페이스는 객체의 실제 존재 여부를 판단하지 않습니다.

#### 사용 예시

[//]: # (.cssg-snippet-get-presign-download-url)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* 버킷이 위치한 리전, 필수 필드 */
    Key: 'exampleobject',
    Sign: false,    /* 서명이 없는 객체 URL 획득 */
});
```

#### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 입력 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 형식을 따라야 합니다. | String  | 예   |
| Region                     | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | 예   |
| Key                        | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | 예   |
| Sign    | 서명이 있는 Url 반환 여부. 기본값: true                          | Boolean | 아니요   |
| Protocol    | `http:` 또는 `https:`를 선택할 수 있습니다. 기본값: `http:`(콜론 포함)                          | String | 아니요   |
| Domain    | 버킷 액세스 도메인. 기본값: {BucketName-APPID}.cos.{Region}.myqcloud.com     | String | 아니요   |
| Method  | 작업 메소드. 예: GET, POST, DELETE, HEAD 등 HTTP 메소드. 기본값: GET | String  | 아니요   |
| - Query    | 서명 계산에 참여하는 query 매개변수 객체. {key: 'val'} 의 형식               | Object   | 아니오   |
| Headers | 서명 계산에 참여하는 header 매개변수 객체                               | Object  | 아니요   |
| Expires | 서명 만료 시간(초). 기본값: 900초                                  | Number  | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 완료 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| data   | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| - Url  | 계산 후 얻은 Url                                               | String |
