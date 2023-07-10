## 소개

본 문서에서는 버킷의 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 버킷 및 해당 권한 인덱스 | 버킷 존재 여부 및 액세스 권한 보유 여부 인덱스 |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 버킷 삭제         | 지정 계정의 빈 버킷 삭제           |



## 버킷 및 해당 권한 인덱스

#### 기능 설명

HEAD Bucket은 해당 버킷이 존재하는지 여부와 액세스 권한 여부 확인을 요청하며, 다음과 같은 상황이 있을 수 있습니다.

- 버킷이 존재하며 읽기 권한이 있는 경우 HTTP 상태 코드 200을 반환합니다.
- 버킷에 대한 읽기 권한이 없는 경우 HTTP 상태 코드 403을 반환합니다.
- 버킷이 존재하지 않는 경우 HTTP 상태 코드 404를 반환합니다.

#### 사용 예시

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000',         /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 입력 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 형식을 따라야 합니다. | String  | 예   |
| Region       | 버킷이 위치한 리전의 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 매개변수 설명                                                     | 유형   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err                                                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 완료 시 빈칸으로 표시됩니다. 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                                                         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object      |

## 버킷 삭제

#### 기능 설명

특정 계정의 빈 버킷을 삭제합니다. 삭제 완료 후 HTTP 상태 코드가 200 또는 204로 반환되는 점에 유의하십시오.

> ?버킷 삭제 전, 버킷에 저장되어 있는 데이터와 업로드가 완료되지 않은 블록 데이터를 모두 삭제하였는지 확인하십시오. 모두 삭제되지 않은 경우 버킷이 삭제되지 않습니다.

#### 사용 예시

[//]: # (.cssg-snippet-delete-bucket)
```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000',         /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 입력 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 형식을 따라야 합니다. | String  | 예   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 매개변수 설명                                                     | 유형   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err            | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object  |
| data                                                         | 요청 성공 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object  |

