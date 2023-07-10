## 소개

본문은 버킷 Referer 에 대한 얼로우/블록리스트의 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 버킷 Referer 설정 | 버킷 Referer 얼로우 또는 블록리스트 설정 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 버킷 Referer 쿼리| 버킷 Referer 얼로우 또는 블록리스트 쿼리 |

## 버킷 Referer 설정

#### 기능 설명

버킷의 Referer의 얼로우 또는 블록리스트를 설정합니다(PUT Bucket referer).

#### 요청 예시

[//]: # ".cssg-snippet-put-bucket-referer"
```js
cos.putBucketReferer({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    RefererConfiguration: {
        Status: 'Enabled',
        RefererType: 'White-List',
        DomainList: {
            Domains: [
                '*.qq.com',
                '*.qcloud.com',
            ]
        },
        EmptyReferConfiguration: 'Allow',
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;        | 설명                                                         | 유형           | 필수 입력 여부 |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket        | 버킷 정책의 버킷 설정. 형식: BucketName-APPID  | String      | Yes       |
| Region                                                       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String    | Yes   |
| RefererConfiguration        | 링크 도용 방지 설정 정보. 자세한 내용은 [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423)를 참고하십시오. | Object      | Yes   |
| - Status         | 링크 도용 방지 활성화 여부. 열거 값: Enabled、Disabled           | String | Yes   |
| - RefererType    | 링크 도용 방지 유형. 열거 값: Black-List, White-List          | String | Yes   |
| - DomainList   | 적용 도메인 리스트. 여러 도메인 및 접두사 매칭 지원, 포트의 도메인 및 IP 지원, 와일드카드\* 지원, 2단계 도메인 또는 여러 단계 도메인의 와일드카드 수행   | Object | Yes   |
| - - Domains    | 적용 도메인. 두 가지 쓰기 방법 지원: 단일'\*.qq.com'또는 다중['\*.qq.com', '\*.qcloud.com']                              | String\Array      | Yes   |
| -  EmptyReferConfiguration  | 빈 Referer 액세스 허용 여부. 열거 값: Allow, Deny, 기본값: Deny | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |

## 버킷 Referer 쿼리

#### 기능 설명

버킷의 Referer의 얼로우 또는 블록리스트를 쿼리합니다(PUT Bucket referer).

#### 요청 예시

[//]: # ".cssg-snippet-get-bucket-referer"
```js
cos.getBucketReferer({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 예시 반환

```json
{
    "RefererConfiguration": {
        "Status": "Enabled",
        "RefererType": "White-List",
        "DomainList": {
            "Domains": [
                "*.qq.com",
                "*.qcloud.com"
            ]
        },
        "EmptyReferConfiguration": "Allow"
    },
    "statusCode": 200,
    "headers": {},
}
```

#### 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 권한 정책의 버킷 쿼리. 형식: BucketName-APPID | String | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String           | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 매개변수 설명                                                     | 유형   |
| --------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| data           | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - RefererConfiguration        | 링크 도용 방지 설정 정보. 자세한 내용은 [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615)를 참고하십시오. | Object      |
| - - Status     | 링크 도용 방지 활성화 여부. 열거 값: Enabled、Disabled    | String    |
| - - RefererType    | 링크 도용 방지 유형. 열거 값: Black-List, White-List     | String |
| - - DomainList   | 적용 도메인 리스트. 여러 도메인 및 접두사 매칭 지원, 포트의 도메인 및 IP 지원, 와일드카드* 지원, 2단계 도메인 또는 여러 단계 도메인의 와일드카드 수행   | Object |
| - - - Domains    | 적용 도메인                            | Array      |
| - - EmptyReferConfiguration  | 빈 Referer 액세스 허용 여부. 열거 값: Allow, Deny, 기본값: Deny | String |
