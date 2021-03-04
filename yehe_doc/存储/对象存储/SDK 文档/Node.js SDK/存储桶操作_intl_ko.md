## 소개

본 문서에서는 버킷의 기본 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service(List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | 버킷 리스트     | 특정 계정의 모든 버킷 리스트 조회     |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 버킷 생성         | 특정 계정에서 버킷 생성         |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 버킷 및 해당 권한 조회 | 버킷 존재 여부 및 액세스 권한이 있는지 여부 조회 |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 버킷 삭제         | 특정 계정의 빈 버킷 삭제           |



## 버킷 리스트 조회

#### 기능 설명

GET Service 인터페이스는 요청자의 모든 버킷 리스트 또는 특정 리전에 있는 버킷 리스트(Bucket list)를 조회합니다. 자세한 내용은 [GET Service](https://intl.cloud.tencent.com/document/product/436/8291)를 참조하십시오.

#### 사용 예시

예시1: 버킷 리스트 조회하기

[//]: # (.cssg-snippet-get-service)
```js
cos.getService(function(err, data) {
    console.log(err || data);
});
```

예시2: 특정 리전의 버킷 리스트 조회하기

[//]: # (.cssg-snippet-get-regional-service)
```js
cos.getService({
    Region: 'COS_REGION',
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Region | 버킷이 위치한 리전으로, 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름           | 매개변수 설명                                                     | 유형   |
| ---------------- | ------------------------------------------------------------ | ------ |
| err              | 요청 과정에서 네트워크 오류와 작업 오류를 포함한 오류 발생 시 반환되는 객체입니다. 요청 성공 시 null이 되며, 자세한 정보는 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참조하십시오.  | Object |
| - statusCode     | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers        | 요청 시 반환되는 헤더 정보입니다.                                           | Object |
| data             | 요청 성공 시 반환되는 객체로, 요청에 오류가 발생한 경우 null이 됩니다.               | Object |
| - statusCode     | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers        | 요청 시 반환되는 헤더 정보입니다.                                           | Object |
| - Owner          | 버킷 소유자의 객체를 의미합니다.                                       | Object |
| - - ID           | 버킷 소유자의 완전한 ID로, 포맷은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`입니다.<br>예시: `qcs::cam::uin/100000000001:uin/100000000001`, 여기에서 100000000001이 uin입니다. | String |
| - - DisplayName  | 버킷 소유자의 이름입니다.                                           | String |
| - Buckets        | 버킷 정보 리스트입니다.                                               | Object |
| - - Name         | 버킷의 이름으로, 포맷은 <BucketName-APPID>입니다. 예시: examplebucket-1250000000 | String |
| - - Location     | 버킷이 위치한 리전으로, 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참조하십시오. 예시: ap-guangzhou, ap-beijing, ap-hongkong 등 | String |
| - - CreationDate | 버킷 생성 시간으로, ISO8601 포맷을 사용합니다. 예시: 2019-05-24T10:56:40Z    | String |

## 버킷 생성

#### 기능 설명

PUT Bucket 인터페이스로 특정 계정에서의 버킷 생성을 요청합니다.

#### 사용 예시

[//]: # (.cssg-snippet-put-bucket)
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷의 이름으로, 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전으로, 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String             | 예   |
| ACL              | 버킷의 액세스 제어 리스트(ACL) 속성을 정의합니다. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중 버킷의 ACL 사전 설정 부분을 참조하십시오. 예를 들면 private, public-read 등이 있으며, 기본값은 private입니다. | String | 아니오   |
| GrantRead        | 권한을 부여받은 대상에게 버킷을 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니오   |
| GrantWrite       | 권한을 부여받은 대상에게 버킷을 쓸 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니오   |
| GrantReadAcp     | 권한을 부여받은 대상에게 버킷의 액세스 제어 리스트(ACL)와 정책(Policy)을 읽을 수 있는 권한을 부여합니다. 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니오   |
| GrantWriteAcp    | 권한을 부여받은 대상에게 버킷의 액세스 제어 리스트(ACL)와 정책(Policy)을 쓸 수 있는 권한을 부여합니다. 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니오   |
| GrantFullControl | 권한을 부여받은 대상에게 버킷을 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 대상을 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니오   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 네트워크 오류와 작업 오류를 포함한 오류 발생 시 반환되는 객체입니다. 요청 성공 시 null이 되며, 자세한 정보는 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보입니다.                                           | Object |
| data         | 요청 성공 시 반환되는 객체로, 요청에 오류가 발생한 경우 null이 됩니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보입니다.                                           | Object |

## 버킷 및 해당 권한 조회

#### 기능 설명

HEAD Bucket은 해당 버킷이 존재하는지 여부와 액세스 권한 여부 확인을 요청하며, 다음과 같은 상황이 있을 수 있습니다.

- 버킷이 존재하며 읽기 권한이 있는 경우 HTTP 상태 코드 200을 반환합니다.
- 버킷에 대한 읽기 권한이 없는 경우 HTTP 상태 코드 403을 반환합니다.
- 버킷이 존재하지 않는 경우 HTTP 상태 코드 404를 반환합니다.

#### 사용 예시

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷의 이름으로, 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region | 버킷이 위치한 리전으로, 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 네트워크 오류와 작업 오류를 포함한 오류 발생 시 반환되는 객체입니다. 요청 성공 시 null이 되며, 자세한 정보는 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보입니다.                                           | Object |
| data         | 요청 성공 시 반환되는 객체로, 요청에 오류가 발생한 경우 null이 됩니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보입니다.                                           | Object |

## 버킷 삭제

#### 기능 설명

특정 계정의 빈 버킷을 삭제합니다. 삭제 완료 후 HTTP 상태 코드가 200 또는 204로 반환되는 점에 유의하십시오.

> ?버킷 삭제 전, 버킷에 저장되어 있는 데이터와 업로드가 완료되지 않은 블록 데이터를 모두 삭제하였는지 확인하십시오. 모두 삭제되지 않은 경우 버킷이 삭제되지 않습니다.

#### 사용 예시

[//]: # (.cssg-snippet-delete-bucket)
```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION'     /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷의 이름으로, 이름 생성 포맷은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region | 버킷이 위치한 리전으로, 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }

```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 네트워크 오류와 작업 오류를 포함한 오류 발생 시 반환되는 객체입니다. 요청 성공 시 null이 되며, 자세한 정보는 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.  | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보입니다.                                           | Object |
| data         | 요청 성공 시 반환되는 객체로, 요청에 오류가 발생한 경우 null이 됩니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드이며 200, 403, 404 등이 있습니다.                  | Number |
| - headers    | 요청 시 반환되는 헤더 정보입니다.                                           | Object |

