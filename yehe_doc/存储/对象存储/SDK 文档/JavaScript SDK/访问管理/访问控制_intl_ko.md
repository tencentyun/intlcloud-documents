## 소개

본 문서는 버킷, 객체의 액세스 제어 리스트(ACL) 관련 API 개요 및 SDK 예시 코드를 제공합니다.

**버킷 ACL**

| API                                                          | 작업명         | 작업 설명                                |
| :----------------------------------------------------------- | :------------- | :-------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 버킷 ACL 설정 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 설정 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) |버킷 ACL 조회 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 조회 |

**객체 ACL**

| API                                                          | 작업명       | 작업 설명                           |
| :----------------------------------------------------------- | :----------- | :--------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정| 버킷의 한 객체의 액세스 제어 리스트 설정  |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회             |

## 버킷 ACL

### 버킷 ACL 설정

#### 기능 설명

PUT Bucket acl 인터페이스는 지정 버킷의 액세스 권한 제어 리스트(ACL) 설정에 사용됩니다.

#### 사용 예시

버킷 공개 읽기 설정

[//]: # (.cssg-snippet-put-bucket-acl)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
    ACL: 'public-read'
}, function(err, data) {
    console.log(err || data);
});
```

특정 사용자에게 버킷의 모든 권한을 부여합니다.

[//]: # (.cssg-snippet-put-bucket-acl-user)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001은 uin
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicy를 통해 버킷 권한 수정:

[//]: # (.cssg-snippet-put-bucket-acl-acp)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy에는 반드시 owner가 있음
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001은 Bucket이 속한 사용자의 Uin
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011은 Uin
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 버킷의 이름. 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String      | 예   |
| Region              | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String      | 예   |
| ACL                 | 버킷의 ACL 속성을 정의합니다. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중 버킷의 ACL 사전 설정 부분을 참조하십시오. 예를 들어 private, public-read 등이 있으며, 기본값은 private입니다. | String      | 아니요   |
| GrantRead        | 권한 피부여자에게 버킷을 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, <br>반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"` <br/><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` <br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' ` | String      | 아니요   |
| GrantWrite       | 권한 피부여자에게 버킷을 쓸 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, <br>반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"` <br/><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` <br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' ` | String      | 아니요   |
| GrantReadAcp     | 권한 피부여자에게 버킷의 ACL과 정책(Policy)을 읽을 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"` <br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` <br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니요   |
| GrantWriteAcp    | 권한 피부여자에게 버킷의 ACL과 정책(Policy)을 쓸 수 있는 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"` <br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` <br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String               | 아니요   |
| GrantFullControl | 권한 피부여자에게 버킷을 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <br><li>서브 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"` <br><li>루트 계정에 권한을 부여할 경우, `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"` </br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 아니요   |
| AccessControlPolicy | 크로스 도메인 리소스 공유 설정의 모든 정보 리스트                               | Object      | 아니요   |
| - Owner             | 버킷 소유자 정보                                           | Object      | 아니요   |
| - - ID           | 버킷 소유자의 전체 ID로, 포맷은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`입니다. <br>예시: `qcs::cam::uin/100000000001:uin/100000000001`, 여기에서 100000000001이 uin입니다. | String      | 아니요   |
| - Grants            | 권한 피부여자의 정보 및 권한 정보 리스트                                   | ObjectArray | 아니요   |
| - -Permission      | 부여받은 권한 정보. 옵션 항목: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL. 열거 값에 대한 자세한 내용은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서의 버킷 작업 부분을 참조하십시오. | String      | 아니요   |
| - - Grantee         | 권한 피부여자의 정보                                               | Object      | 아니요   |
| - - ID            | 권한 피부여자의 전체 ID로, 포맷은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`입니다.</br> 예시: `qcs::cam::uin/100000000001:uin/100000000001`, 여기에서 100000000001이 uin입니다. | String      | 아니요   |
| - - - DisplayName   | 권한 피부여자의 이름. 일반적으로 ID와 일치한 문자열로 입력                 | String      | 아니요   |
| - - - URI           | 사용자 그룹 사전 설정. [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서의 사용자 그룹 사전 설명 부분을 참조하십시오. 예시: `http://cam.qcloud.com/groups/global/AllUsers` 또는 `http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String      | 아니요     |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err                                                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 완료 시 빈칸으로 표시됩니다. 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 403, 404 등)                  | Number |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object |
| data                                                         | 요청 완료 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 403, 404 등)                  | Number |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object |

### 버킷 ACL 조회

#### 기능 설명

GET Bucket acl 인터페이스는 버킷의 ACL 조회에 사용됩니다. 해당 API의 요청자는 버킷에 ACL 권한을 입력해야 합니다.

#### 사용 예시

[//]: # (.cssg-snippet-get-bucket-acl)
```js
cos.getBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
}, function(err, data) {
    console.log(err || data);
});
```

#### 예시 반환

```json
{
    "GrantFullControl": "",
    "GrantWrite": "",
    "GrantRead": "",
    "GrantReadAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "GrantWriteAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "ACL": "private",
    "Owner": {
        "ID": "qcs::cam::uin/100000000001:uin/100000000001",
        "DisplayName": "qcs::cam::uin/100000000001:uin/100000000001"
    },
    "Grants": [{
        "Grantee": {
            "ID": "qcs::cam::uin/100000000011:uin/100000000011",
            "DisplayName": "qcs::cam::uin/100000000011:uin/100000000011"
        },
        "Permission": "READ"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | 버킷의 이름. 이름 생성 포맷이 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String  | 예   |
| Region | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름 | 매개변수 설명                                                    | 유형        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err                                                          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 완료 시 빈칸으로 표시됩니다. 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오. | Object      |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 403, 404 등)                  | Number      |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data                                                         | 요청 완료 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.                 | Object      |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 403, 404 등)                  | Number      |
| - headers                                                    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - ACL                                                        | 버킷의 ACL 속성을 정의합니다. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중 버킷의 ACL 사전 설정 부분을 참조하십시오. 예를 들면 private, public-read 등이 있으며, 기본값은 private입니다. | String      |
| - GrantRead                                                  | 버킷 읽기 권한을 보유한 권한 피부여자 ID 정보                         | String      |
| - GrantWrite                                                  | 버킷 쓰기 권한을 보유한 권한 피부여자 ID 정보                         | String      |
| - GrantReadAcp                                               | 버킷 ACL과 버킷 정책(Policy) 읽기 권한을 보유한 권한 피부여자 ID 정보                         | String      |
| - GrantWriteAcp                                              | 버킷 ACL과 버킷 정책(Policy) 쓰기 권한을 보유한 권한 피부여자 ID 정보                         | String      |
| - GrantFullControl                                           | 버킷의 모든 권한을 보유한 권한 피부여자 ID 정보                         | String      |
| - Owner                                                      | 버킷 소유자 정보                                           | Object      |
| - - DisplayName                                              | 버킷 소유자 이름                                         | String      |
| - - ID                                                       | 버킷 소유자의 전체 ID <br>포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - Grants                                                     | 권한 피부여자의 정보 및 권한 정보 리스트                                   | ObjectArray |
| - - Permission                                               | 권한 피부여자의 권한 정보 표시. 열거 값: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      |
| - - Grantee                                                  | 권한 피부여자 정보                                             | Object      |
| - - - DisplayName                                            | 권한 피부여자 이름                                               | String      |
| - - - ID                                                     | 권한 피부여자의 전체 ID <br>루트 계정인 경우, 포맷: `qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>` <br>또는 `qcs::cam::anyone:anyone`(모든 사용자를 대신 지칭) <br>서브 계정인 경우, 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String      |
| - - - URI                                                    | 사용자 그룹 사전 설정. [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서의 사용자 그룹 사전 설명 부분을 참조하십시오. 예시: `http://cam.qcloud.com/groups/global/AllUsers` 또는 `http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String      |


## 객체 ACL

### 객체 ACL 설정

#### 기능 설명

PUT Object acl 인터페이스는 특정 버킷에서 어떤 객체의 액세스 제어 리스트(ACL)를 설정할 때 쓰입니다.

> !루트 계정(동일한 APPID)당 버킷 ACL, Policy 및 CAM 관련 정책은 최대 1000개까지 설정 가능하며 객체 액세스 제어 리스트(ACL) 규칙은 수량에 제한이 없습니다. 객체 액세스 제어 리스트(ACL) 제어가 불필요한 경우 설정하지 마십시오. 기본적으로 버킷 권한을 상속합니다.

#### 사용 예시

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
    Key: 'exampleobject',              /* 필수 */
    ACL: 'public-read',        /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

사용자에게 객체의 모든 권한 부여:

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
    Key: 'exampleobject',              /* 필수 */
    GrantFullControl: 'id="100000000001"' // 100000000001은 루트 계정 uin
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicy를 통해 객체에 쓰기 권한 부여:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
    Key: 'exampleobject',              /* 필수 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy에는 반드시 owner가 있음
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001은 Bucket이 속한 사용자의 UIN 계정
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011은 Bucket이 속한 사용자의 서브 계정 UIN
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 버킷의 이름. 이름 생성 포맷이 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String      | 예   |
| Region              | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String      | 예   |
| Key                 | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String           | 예   |
| ACL                 | 객체의 ACL 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분 참조 <br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본적인 버킷 권한을 상속하십시오.** | String      | 아니요   |
| GrantRead           | 권한 피부여자에게 객체 읽기 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code><br><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>예: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String           | 아니요   |
| GrantFullControl    | 권한 피부여자에게 객체를 조작할 수 있는 모든 권한을 부여합니다. 포맷은 id="[OwnerUin]"이며, 반각 쉼표(,)를 사용하여 다음과 같이 여러 그룹의 권한 피부여자를 구분합니다. <ul  style="margin: 0;"><li>서브 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>루트 계정에 권한을 부여할 경우, <code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>예: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul>| String | 아니요   |
| AccessControlPolicy | 객체의 ACL 속성 정보 설정                        | Object      | 아니요   |
| - Owner             | 객체 소유자 정보                                             | Object      | 아니요   |
| - - ID              | 객체 소유자 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      | 아니요   |
| - - DisplayName     | 객체 소유자 이름                                             | String      | 아니요   |
| - Grants            | 권한 피부여자의 정보 및 권한 정보 리스트                                   | ObjectArray | 아니요   |
| - -Permission      | 권한 피부여자에게 권한 정보를 부여하도록 지시, 열거 값: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      | 아니요   |
| - - Grantee         | 권한 피부여자의 정보                                               | Object      | 아니요   |
| - - - DisplayName   | 권한 피부여자의 이름                                               | String      | 아니요   |
| - - - ID            | 권한 피부여자의 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<;SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 완료 시 빈칸으로 표시됩니다. 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참조하십시오. | Object      |
| - statusCode                                                 | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 403, 404 등)                  | Number  |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |
| data         | 요청 완료 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 204, 403, 404 등)             | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object |

### 객체 ACL 조회

#### 기능 설명

GET Object acl 인터페이스는 버킷의 객체 액세스 권한을 조회할 때 사용합니다. 버킷 소유자에게만 작업 권한이 주어집니다.

#### 사용 예시

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 버킷이 위치한 리전. 필수 필드*/
    Key: 'exampleobject',              /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷의 이름. 이름 생성 포맷이 BucketName-APPID이며, 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String | 예   |
| Region | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. | String | 예   |
| Key    | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 완료 시 빈칸으로 표시됩니다. 자세한 내용은 [에러 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참조하십시오. | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| data              | 요청 완료 시 반환되는 객체. 요청에 오류가 발생할 경우 빈칸으로 표시됩니다.               | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예시: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| - ACL             | 객체의 ACL 속성 정의. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참조하십시오. <br>**주의: 객체 ACL 제어가 필요하지 않을 경우, default로 설정하거나 이 항목을 설정하지 말고 기본적인 버킷 권한을 상속하십시오.** | String      |
| - Owner           | 리소스 소유자 식별                                             | Object      |
| - - ID            | 객체 소유자 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>루트 계정 ID인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - - DisplayName   | 객체 소유자의 이름                                             | String      |
| - Grants          | 권한 피부여자의 정보 및 권한 정보 리스트                                   | ObjectArray |
| - -Permission      | 권한 피부여자의 권한 정보 표시. 열거 값: READ, READ_ACP, WRITE_ACP, FULL_CONTROL | String      |
| - - Grantee       | 권한 피부여자의 정보                                           | Object      |
| - - - DisplayName | 사용자 이름                                                   | String      |
| - - - ID          | 사용자 ID. 포맷: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` </br>루트 계정 ID인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |





