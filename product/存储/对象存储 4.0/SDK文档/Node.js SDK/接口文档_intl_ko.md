>?글에서 나오는 SecretId, SecretKey, Bucket 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오

Node.js SDK github 주소: [tencentyun/cos-nodejs-sdk-v5](https://github.com/tencentyun/cos-nodejs-sdk-v5)

## Service 작업

### Get Service

#### 기능 설명

Get Service API는 해당 사용자의 모든 버킷 리스트를 획득하는 것을 구현합니다. 해당 API는 Authorization 서명을 통해 인증해야 하며, 서명 중의 AccessID 소속 계정의 버킷 리스트만 획득할 수 있습니다.

#### 작업 방법 프로토타입

Get Service 호출:

```js
cos.getService(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

- **전용 매개변수 없음**

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| err        | 요청에서 오류 발생 시 반환되는 객체이며, 네트워크 오류 및 비즈니스 오류를 포함합니다. 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Owner      | 버킷 소유자 정보                                     | Object |
| uin           | 버킷 소유자 UIN                                           | string |
| Buckets    | 이번에 반환된 버킷 리스트의 모든 정보                         | Array  |
| Name         | 버킷 이름                                                  | string |
| CreateDate | 버킷 생성 시간. ISO8601 형식                                | String |



## 도구 방법

### 사전 서명 링크 획득

#### 사용 사례

예시1: 서명이 없는 Object Url을 획득합니다.

```js
var url = cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
});
```

예시2: 서명이 있는 Object Url을 획득합니다.

```js
var url = cos.getObjectUrl({
    Key: '1.jpg'
});
```

예시3: 서명 프로세스가 비동기화로 획득할 경우 콜백을 통해 서명이 있는 Url을 획득해야 합니다.

```js
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

예시4: 사전 서명 Put Object 회득하여 Url을 업로드합니다.

```js
cos.getObjectUrl({
    Method: 'PUT',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    console.log(err || data.Url);
});
```

#### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 항목 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region  | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Key     | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID이며, **파일에 대한 조작 요청일 경우 파일 이름이고 필수 입력 매개변수**입니다. 버킷에 대한 조작일 경우 비워둡니다 | String  | 예   |
| Sign    | 서명이 있는 Url 반환 여부                                       | Boolean | 아니요   |
| Method  | 조작 방식, 예를 들면 get, post, delete, head 등 HTTP 방식, 기본값은 get | String  | 아니요   |
| Query   | 서명 계산에 참여한 쿼리 매개변수 객체                                | Object  | 아니요   |
| Headers | 서명 계산에 참여한 헤더 매개변수 객체                               | Object  | 아니요   |

#### 반환값 설명

반환값은 하나의 문자열이며 2가지 방식으로 반환됩니다.

1. 서명 계산이 동기화 수행될 수 있는 경우(예를 들어, 인스턴스화를 통해 SecretId 및 SecretKey가 가져오기됨), 기본으로 서명을 포함한 url을 반환합니다.
2. 그렇지 않으면 서명이 포함되지 않은 url을 반환합니다.

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| - Url  | 계산하여 얻은 Url                                               | String |



## Bucket 조작

### Head Bucket

#### 기능 설명

Head Bucket 요청은 해당 버킷이 존재하는지, 접근 권한이 있는지를 확인할 수 있습니다. Head의 권한은 Read와 일치합니다.

#### 작업 방식 프로토타입

Head Bucket 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE'		/* 필수 */
};

cos.headBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ----------- | ------------------------------------------------------------ | ------- |
| err        | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| BucketExist | 버킷 존재 여부                                              | Boolean |
| BucketAuth  | 해당 버킷의 권한 소유 여부                                     | Boolean |

### Get Bucket

#### 기능 설명

Get Bucket 요청은 List Object 요청과 동일하며, 해당 버킷 아래의 부분 또는 모든 객체를 나열할 수 있습니다. 해당 요청을 시작하려면 쓰기 권한이 있어야 합니다.

#### 작업 방식 프로토타입

Get Bucket 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE',	/* 필수 */
	Prefix : 'STRING_VALUE',	/* 필수 아님 */
	Delimiter : 'STRING_VALUE', /* 필수 아님 */
	Marker : 'STRING_VALUE',	/* 필수 아님 */
	MaxKeys : 'STRING_VALUE',	/* 필수 아님 */
	EncodingType : 'STRING_VALUE',	/* 필수 아님 */
};

cos.getBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region       | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Prefix       | 접두사 매칭, 반환되는 객체 키 접두사 주소 지정에 사용합니다                       | String | 아니요   |
| Delimiter    | 구분 기호는 하나의 부호입니다. Prefix가 있을 경우, 해당 Prefix와 delimiter 사이에 동일한 경로를 같은 종류로 분류하고, Common Prefix로 정의합니다. 그런 다음 모든 Common Prefix를 나열합니다. Prefix가 없을 경우, 경로 시작점에서 시작합니다 | String | 아니요   |
| Marker       | 기본으로 UTF-8 이진 순서로 항목이 나열되며, 나열된 모든 항목은 marker에서 시작합니다   | String | 아니요   |
| MaxKeys      | 1회 최대 반환 항목 수, 기본값은 1000입니다                             | String | 아니요   |
| EncodingType | 반환값의 인코딩 방식을 규정합니다                                         | String | 아니요   |



#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| -------------- | ------------------------------------------------------------ | -------- |
| err            | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| CommonPrefixes | Prefix와 delimiter 사이의 동일한 경로를 같은 종류로 분류하고, Common Prefix로 정의합니다 | Array    |
| Prefix       | 접두사 매칭, 반환되는 객체 접두사 주소 지정에 사용합니다                       | String |
| Name         | 버킷 이름                                                  | String   |
| Prefix         | 객체 키의 접두사                                                 | String   |
| Marker       | 기본으로 UTF-8 이진 순서로 항목이 나열되며, 나열된 모든 항목은 marker에서 시작합니다   | String |
| MaxKeys      | 1회 최대 반환 항목 수                             | String |
| IsTruncated    | 반환 항목 잘라내기 여부, 'true' 또는 'false'                      | String   |
| NextMarker      | 반환 항목 잘라내기의 경우, 반환되는 NextMarker는 다음 항목의 시작점입니다   | String   |
| Encoding-Type  | 인코딩 유형, Delimiter, Marker, Prefix, NextMarker, Key에 작용합니다   | String   |
| Contents       | 메타데이터 정보                                                   | Array    |
| ETag           | 파일의 SHA-1 알고리즘 인증값                                      | String   |
| Size           | 파일 크기, 단위 Byte                                          | String   |
| Key            | 객체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   |
| LastModified   | 객체 마지막 수정 시간                                          | String   |
| Owner          | 버킷 소유자 정보                                            | Object   |
| ID             | 버킷 소유자 UID 정보                                     | String   |



### Put Bucket

#### 기능 설명

Put Bucket 요청은 지정 계정에서 한 개의 버킷을 생성할 수 있습니다.

#### 작업 방식 프로토타입

Put Bucket 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE',	/* 필수 */
	ACL : 'STRING_VALUE',	/* 필수 아님 */
	GrantRead : 'STRING_VALUE', /* 필수 아님 */
	GrantWrite : 'STRING_VALUE',	/* 필수 아님 */
	GrantFullControl : 'STRING_VALUE'	/* 필수 아님 */
};

cos.putBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region           | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| ACL              | 사용자 지정 가능한 파일 권한. 유효값: private, public-read, public-read-write, 기본값: private | String | 아니요   |
| GrantRead        | 권한을 부여받은 자에게 읽기 권한 부여, 형식은 x-cos-grant-read: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |
| GrantWrite       | 권한을 부여받은 자에게 쓰기 권한 부여, 형식은 x-cos-grant-write: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |
| GrantFullControl | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 x-cos-grant-full-control: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data     | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Location | 생성 성공 후, 버킷의 작업 주소                                | String |

### Delete Bucket

#### 기능 설명

Delete Bucket 요청은 지정 계정에서 버킷을 삭제할 수 있으며, 삭제 전 요청 버킷은 비어있어야 합니다.

#### 작업 방식 프로토타입

 Delete Bucket 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE'		/* 필수 */
};

cos.deleteBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                | 요청에서 오류 발생 시 반환되는 개체, 네트워크 오류 및 비즈니스 오류를 포함하며, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비어 있습니다 | Object |
| data                | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| DeleteBucketSuccess | 삭제 성공 여부                                                 | Boolean |

###  Get Bucket ACL

#### 기능 설명

API를 사용하여 Bucket의 ACL 리스트를 읽으며, 소유자만 작업 권한이 있습니다.

#### 작업 방식 프로토타입

Get Bucket ACL 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE'		/* 필수 */
};

cos.getBucketAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ----------------- | ------------------------------------------------------------ | ------ |
| err               | 요청에서 오류 발생 시 반환되는 개체, 네트워크 오류 및 비즈니스 오류를 포함하며, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비어 있습니다 | Object |
| data              | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Owner             | 리소스의 소유자                                             | Object |
| uin               | 사용자 QQ 번호                                                     | String |
| AccessControlList | 권한 받은 자 정보 및 권한 정보 | Object |
| Grant             | 구체적인 라이센싱 정보                                               | Array  |
| Permission        | 권한, 열거형 값: READ，WRITE，FULL_CONTROL                  | String |
| Grantee           | 권한 부여받은 자의 리소스 정보                                            | Object |
| uin               | 권한 부여받은 자의 QQ 번호 또는 'anonymous'                           | String |
| Subacount         | 서브 계정 QQ 계정                                               | String |

###  Put Bucket ACL

#### 기능 설명

API를 사용하여 버킷의 ACL 리스트를 씁니다. Put Bucket ACL은 덮어쓰기 작업이며, 새로운 ACL 입력은 기존 ACL을 덮어씁니다. 소유자에게만 작업 권한이 있습니다.

#### 작업 방식 프로토타입

Put Bucket ACL 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',			/* 필수 */
	Region : 'STRING_VALUE',			/* 필수 */
	ACL : 'STRING_VALUE',				/* 필수 아님 */
	GrantRead : 'STRING_VALUE', 		/* 필수 아님 */
	GrantWrite : 'STRING_VALUE',		/* 필수 아님 */
	GrantFullControl : 'STRING_VALUE'	/* 필수 아님 */
};

cos.putBucketAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region           | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| ACL              | 사용자 지정 가능한 파일 권한. 유효값: private, public-read, 기본값: private | String | 아니요   |
| GrantRead        | 권한을 부여받은 자에게 읽기 권한 부여, 형식은 x-cos-grant-read: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |
| GrantWrite       | 권한을 부여받은 자에게 쓰기 권한 부여, 형식은 x-cos-grant-write: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |
| GrantFullControl | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 x-cos-grant-full-control: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ------------------ | ------------------------------------------------------------ | ------- |
| err            | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data               | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| BucketGrantSuccess | 권한 부여 성공 여부                                                 | Boolean |

### Get Bucket CORS

#### 기능 설명

Get Bucket CORS는 CORS 읽기를 구현합니다.

#### 작업 방식 프로토타입

- Get Bucket CORS 호출 작업

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE'		/* 필수 */
};

cos.getBucketCors(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ------------- | ------------------------------------------------------------ | ------ |
| err            | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| CORSRule      | 구성 정보 집합                                                | Array  |
| AllowedMethod | 허용된 HTTP 작업, 열거형 값: Get, Put, Head, Post, Delete       | Array  |
| AllowedOrigin | 허용된 액세스 리소스, [ * ] 와일드카드 지원                            | Array  |
| AllowedHeader | OPTIONS 요청 발송 시 다음 요청에 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있는지 서버에 알립니다 | Array  |
| ExposeHeader  | 브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 정보 설정           | Array  |
| MaxAgeSeconds | OPTIONS 요청으로 얻은 결과의 유효기간 설정                            | String |
| ID            | 규칙 이름                                                     | String |

### Put Bucket CORS

#### 기능 설명

Put Bucket CORS는 CORS 읽기/쓰기를 구현합니다.

#### 작업 방식 프로토타입

Put Bucket CORS 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 필수 */
	Region : 'STRING_VALUE',		/* 필수 */
	CORSRules : [
		{
			ID : 'STRING_VALUE',	/* 필수 아님 */
			AllowedMethods: [ 		/* 필수 */
			  'STRING_VALUE',
			  ...
			],
			AllowedOrigins: [		 /* 필수 */
			  'STRING_VALUE',
			  ...
			],
			AllowedHeaders: [		/* 필수 아님 */
			  'STRING_VALUE',
			  ...
			],
			ExposeHeaders: [		/* 필수 아님 */
				'STRING_VALUE',
				...
			],
			MaxAgeSeconds: 'STRING_VALUE'	/* 필수 아님 */
		  },
		  ....
	]
};

cos.putBucketCors(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | 버킷 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region         | 버킷 소재 지역입니다. 열거형 값에 관한 자세한 내용은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| CORSRules       | CORS 규칙 집합                                                 | Array  | 아이요   |
| ID             | 규칙 이름                                                | string   | 아니요   |
| AllowedMethods | 허용된 HTTP 작업, 열거형 값: Get, Put, Head, Post, Delete       | Array  | 예   |
| AllowedOrigins | 허용된 액세스 리소스, [ * ] 와일드카드를 지원하며, 프로토콜, 포트 및 도메인 이름은 반드시 일치해야 합니다  | Array  | 예   |
| AllowedHeaders | OPTIONS 요청 발송 시 다음 요청에 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있는지 서버에 알리며, [ * ] 와일드카드를 지원합니다 | Array  | 아니요   |
| ExposeHeaders  | 브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 정보 설정           | Array  | 아니요   |
| MaxAgeSeconds  | OPTIONS 요청이 얻은 결과의 유효기간 설정                            | String | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| -------------------- | ------------------------------------------------------------ | ------- |
| err                  | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data                 | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| PutBucketCorsSucesss | Bucket CORS 설정 성공 여부                                                 | Boolean |

### Delete Bucket CORS

#### 기능 설명

Delete Bucket CORS는 CORS 삭제를 구현합니다.

#### 작업 방식 프로토타입

Delete Bucket CORS 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 필수 */
	Region : 'STRING_VALUE'			/* 필수 */
};

cos.deleteBucketCors(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형 |
| ----------------------- | ------------------------------------------------------------ | ------- |
| err                     | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 개체, 요청 오류 시 비어 있습니다                         | Object  |
| DeleteBucketCorsSuccess | 버킷 CORS 삭제 성공 여부                                    | Boolean |

### Get Bucket Location

#### 기능 설명

Get Bucket Location API는 버킷 소재 지역 정보를 획득하며, 버킷 소유자만 읽기 권한이 있습니다.

#### 작업 방식 프로토타입

Get Bucket Location 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 필수 */
	Region : 'STRING_VALUE'			/* 필수 */
};

cos.getBucketLocation(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형 |
| ------------------ | ------------------------------------------------------------ | ------ |
| err                | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data               | 요청 성공 시 반환되는 개체, 요청 오류 시 비어 있습니다                         | Object  |
| LocationConstraint | 버킷 소재 지역, 열거형 값: china-east, china-south, china-north, china-west, singapore | String |

### Get Bucket Tagging

#### 기능 설명

Get Bucket Tagging API는 지정한 버킷의 태그 획득을 구현합니다.

#### 작업 방식 프로토타입

Get Bucket Tagging 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE'		/* 필수 */
};

cos.getBucketTagging(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Tags   | 버킷의 태그 집합                                            | Array  |
| Key    | Tag의 유형 이름                                               | String |
| Value  | Tag의 값                                                     | String |

### Put Bucket Tagging

#### 기능 설명

Put Bucket Tagging API는 지정 버킷을 사용하여 태깅을 구현합니다.

#### 작업 매개변수 설명

 Put Bucket Tagging 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE',	/* 필수 */
	Tags :  [
		{
			Key : 'key1',		/* 필수 */
			Value : 'value1'	/* 필수 */
		},
		...
	]
};

cos.putBucketTagging(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Tags   | 버킷의 태그 집합                                            | Array  | 예   |
| Key    | Tag의 유형 이름                                               | String | 예   |
| Value  | Tag의 값                                                     | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형 |
| ----------------------- | ------------------------------------------------------------ | ------- |
| err                     | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 개체, 요청 오류 시 비어 있습니다                         | Object  |
| PutBucketTaggingSuccess | Tag 설정 성공 여부                                            | Boolean |

### Delete Bucket Tagging

#### 기능 설명

Delete Bucket Tagging API는 지정한 버킷의 태그를 삭제합니다.

#### 작업 방식 프로토타입

Delete Bucket Tagging 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 필수 */
	Region : 'STRING_VALUE'		/* 필수 */
};

cos.deleteBucketTagging(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형 |
| -------------------------- | ------------------------------------------------------------ | ------- |
| err                        | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data                       | 요청 성공 시 반환되는 개체, 요청 오류 시 비어 있습니다                         | Object  |
| DeleteBucketTaggingSuccess | 버킷 태그 삭젱 성공 여부                                     | Boolean |

## Object 작업

### Head Object

#### 기능 설명

Head Object 요청은 대응하는 Object의 메타데이터를 검색할 수 있으며 Head의 권한은 Get의 권한과 일치합니다.

#### 작업 방식 프로토타입

Head Object 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 필수 */
	Region : 'STRING_VALUE',		/* 필수 */
	Key : 'STRING_VALUE',			/* 필수 */
	IfModifiedSince : 'STRING_VALUE'	/* 필수 아님 */
};

cos.headObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region          | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Key            | 객체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| IfModifiedSince | Object가 지정된 시간 이후에 수정되면 Object 메타 정보가 반환됩니다                                     | string | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                | 요청에서 오류 발생 시 반환되는 개체, 네트워크 오류 및 비즈니스 오류를 포함하며, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비어 있습니다 | Object |
| data                | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| x-cos-object-type   | Object가 추가로 업로드될 수 있는지의 여부를 표시하는 데 사용합니다. 열거형 값: normal 또는 appendable | String  |
| x-cos-storage-class | Object의 스토리지 클래스, 열거형 값: Standard, Standard_IA              | String  |
| x-cos-meta- *       | 사용자 지정 메타데이터                                           | String  |
| NotModified         | 요청에 IfModifiedSince가 있고, 파일이 수정되지 않았으면, true입니다   | Boolean |

### Get Object

#### 기능 설명

Get Object 요청은 파일(Object)을 로컬로 다운로드 할 수 있습니다. 해당 조작은 대상 Object에 대한 읽기 권한이 있거나 또는 대상 Object가 모든 사람에게 읽기 권한을 개방해야 합니다(공개 읽기).

#### 작업 방식 프로토타입

Get Object 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Key : 'STRING_VALUE',							/* 필수 */
	ResponseContentType : 'STRING_VALUE',			/* 필수 아님 */
	ResponseContentLanguage : 'STRING_VALUE',		/* 필수 아님 */
	ResponseExpires : 'STRING_VALUE',				/* 필수 아님 */
	ResponseCacheControl : 'STRING_VALUE',			/* 필수 아님 */
	ResponseContentDisposition : 'STRING_VALUE',	/* 필수 아님 */
	ResponseContentEncoding : 'STRING_VALUE',		/* 필수 아님 */
	Range : 'STRING_VALUE',							/* 필수 아님 */
	IfModifiedSince : 'STRING_VALUE',				/* 필수 아님 */
	Output : 'STRING_VALUE' || 'WRITE_STRING'		/* 필수 */
};

cos.getObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket                     | 버킷 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region                     | 버킷 소재 지역입니다. 열거형 값에 관한 자세한 내용은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key                        | 객체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| ResponseContentType        | 반환 헤더 중의 Content-Type 매개변수를 설정합니다                                  | string      | 아니요   |
| ResponseContentLanguage    | 반환 헤더 중의 Content-Language 매개변수를 설정합니다                                | String               | 아니요   |
| ResponseExpires            | 반환 헤더 중의 Content-Expires 배개변수를 설정합니다                                 | String               | 아니요   |
| ResponseCacheControl       | 반환 헤더 중의 Cache-Control 매개변수를 설정합니다                                   | String                | 아니요   |
| ResponseContentDisposition | 반환 헤더 중의 Content-Disposition 매개변수를 설정합니다                             | String               | 아니요   |
| ResponseContentEncoding    | 반환 헤더 중의 Content-Encoding 매개변수를 설정합니다                                | String                | 아니요   |
| Range                      | RFC 2616에 정의된 지정 파일 다운로드 범위, 단위가 바이트(bytes)입니다     | String                | 아니요   |
| IfModifiedSince            | 파일 수정 시간이 지정한 시간보다 늦으면 파일 내용을 반환합니다                 | String               | 아니요   |
| Output                     | 출력해야 할 파일의 경로 또는 쓰기 스트림                               | String/WriteStream | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                | 요청에서 오류 발생 시 반환되는 개체, 네트워크 오류 및 비즈니스 오류를 포함하며, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비어 있습니다 | Object |
| data                | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| x-cos-object-type   | Object가 추가로 업로드될 수 있는지의 여부를 표시하는 데 사용합니다. 열거형 값: normal 또는 appendable | String  |
| x-cos-storage-class | Object의 스토리지 클래스, 열거형 값: Standard, Standard_IA              | String  |
| x-cos-meta- *       | 사용자 지정 메타데이터                                           | String  |
| NotModified         | 요청에 IfModifiedSince가 있고, 파일이 수정되지 않았으면, true입니다   | Boolean |

### Put Object

#### 기능 설명

Put Object 요청은 한 개의 파일(Object)을 지정 버킷으로 업로드할 수 있습니다.

> !

1. Key(파일 이름)는 `/`로 끝날 수 없습니다. 그렇지 않으면 폴더로 인식됩니다.
2. 현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 업로드 시 설정하지 마십시오. 기본으로 Bucket 권한은 승계됩니다.

#### 작업 방식 프로토타입

Put Object 호출:

```js
cos.putObject({
    Bucket : 'STRING_VALUE',                        /* 필수 */
    Region : 'STRING_VALUE',                        /* 필수 */
    Key : 'STRING_VALUE',                           /* 필수 */
    Body: fs.createReadStream('./a.zip'),           /* 필수 */
    onProgress: function (progressData) {
        console.log(progressData);
    },
}, function(err, data) {
    if(err) {
        console.log(err);
    } else {
        console.log(data);
    }
});
```

#### 작업 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------ | ------------------------------------------------------------ | -------------- | ---- |
| Bucket         | 버킷 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region         | 버킷 소재 지역입니다. 열거형 값에 관한 자세한 내용은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key            | 객체 키(Object의 이름), 버킷에서 객체의 유일한 식별자입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| CacheControl       | RFC 2616에 정의된 캐시 정책, Object 메타데이터로 저장됩니다          | String         | 아니요   |
| ContentDisposition | RFC 2616에 정의된 파일 이름, Object 메타데이터로 저장됩니다          | String         | 아니요   |
| ContentEncoding    | RFC 2616에 정의된 인코딩 형식, Object 메타데이터로 저장됩니다          | String         | 아니요   |
| ContentLength      | RFC 2616에 정의된 HTTP 요청 내용의 길이(바이트)입니다                  | String         | 아니요   |
| ContentType        | RFC 2616에 정의된 내용 유형(MIME), Object 메타데이터로 저장됩니다  | String         | 아니요   |
| Expect             | Expect: 100-continue 사용 시, 서버측에서 확인을 받기 전까지 요청 내용이 전송되지 않습니다 | String             | 아니요   |
| Expires            | RFC 2616에 정의된 만료 시간, Object 메타데이터로 저장됩니다          | String         | 아니요   |
| ContentSha1        | RFC 3174에 정의된 160-bit 콘텐츠 SHA-1 알고리즘 인증값              | String         | 아니요   |
| ACL              | 사용자 지정 가능한 파일 권한. 유효값: private, public-read         | String         | 아니요   |
| GrantRead          | 권한을 부여받은 자에게 읽기 권한 부여, 형식은 x-cos-grant-read: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String         | 아니요   |
| GrantWrite       | 권한을 부여받은 자에게 쓰기 권한 부여, 형식은 x-cos-grant-write: uin=" ",uin=" "입니다. <br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID”입니다. | String         | 아니요   |
| GrantFullControl | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 x-cos-grant-full-control: uin=" ",uin=" "입니다. <br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String         | 아니요   |
| x-cos-meta- *      | 사용자 지정 가능한 헤더 정보, Object 메타데이터로 반환됩니다. 크기 제한은 2K입니다. | String         | 아니요   |
| Body               | 입력 파일 경로 또는 파일 스트림                                         | String/Stream | 예   |
| onProgress         | 진행률 콜백 함수, 콜백은 객체이며 진행률 정보를 포함합니다                   | Function       | 아니요   |



#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| ETag   | 파일의 MD5 알고리즘 인증값을 반환합니다. ETag의 값은 Object의 내용이 변경되었는지 확인하는 데 사용할 수 있습니다 | String |

### Delete Object

#### 기능 설명

Delete Object 요청은 한 개의 파일(Object)을 삭제할 수 있습니다.

#### 작업 방식 프로토타입

Delete Object 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Key : 'STRING_VALUE'							/* 필수 */
};

cos.deleteObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key            | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                | 요청에서 오류 발생 시 반환되는 개체, 네트워크 오류 및 비즈니스 오류를 포함하며, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비어 있습니다 | Object |
| data                | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| DeleteObjectSuccess | 파일 삭제 성공 여부                                                 | Boolean |
| BucketNotFound      | 지정한 버킷을 찾지 못할 경우, true입니다                           | Boolean |

### Options Object

#### 기능 설명

Options Object 요청은 CORS의 사전 요청을 구현합니다. 즉, OPTIONS 요청을 서버에 보내서 크로스 도메인 작업을 진행할지 여부를 확인합니다.

#### 작업 방식 프로토타입

Options Object 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 필수 */
	Region : 'STRING_VALUE',		/* 필수 */
	Key : 'STRING_VALUE',			/* 필수 */
	Origin : 'STRING_VALUE', 		/* 필수 */
	AccessControlRequestMethod : 'STRING_VALUE', 		/* 필수 */
	AccessControlRequestHeaders : 'STRING_VALUE'		/* 필수 아님 */
};

cos.optionsObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region                      | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key            | 객체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| Origin                      | CORS의 요청 소스 도메인 이름 시뮬레이션                                   | String | 예   |
| AccessControlRequestMethod  | CORS 요청 시뮬레이션 HTTP 방법                                   | String | 예   |
| AccessControlRequestHeaders | CORS의 요청 헤더 시뮬레이션                                       | String | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형 |
| -------------------------- | ------------------------------------------------------------ | ------ |
| err            | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data                       | 요청 성공 시 반환되는 개체, 요청 오류 시 비어 있습니다                         | Object  |
| AccessControlAllowOrigin   | CORS 요청의 소스 도메인 이름을 시뮬레이트합니다. 소스가 허용되지 않을 경우, 이 헤더는 반환되지 않습니다 | String |
| AccessControlAllowMethods  | CORS HTTP 요청 방식을 시뮬레이션합니다. 요청 방법이 허용되지 않을 경우, 이 헤더는 반환되지 않습니다                                   | String |
| AccessControlAllowHeaders  | CORS 요청의 헤더를 시뮬레이션합니다. 어떠한 요청 헤더 시뮬레이션도 허용되지 않을 경우, 이 헤더는 반환되지 않습니다 | String |
| AccessControlExposeHeaders | CORS 요청에 지원되는 반환 헤더이며, 쉼표로 구분됩니다                                 | String |
| AccessControlMaxAge        | OPTIONS 요청으로 얻은 결과의 유효기간 설정                               | String |

### Get Object ACL

#### 기능 설명

Get Object ACL API는 API를 사용하여 Object의 ACL 리스트를 읽는 것을 구현하며, 소유자만 작업 권한이 있습니다.

#### 작업 방식 프로토타입

Get Object ACL 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Key : 'STRING_VALUE'							/* 필수 */
};

cos.getObjectAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key            | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형 |
| ----------------- | ------------------------------------------------------------ | ------ |
| err               | 요청에서 오류 발생 시 반환되는 개체, 네트워크 오류 및 비즈니스 오류를 포함하며, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비어 있습니다 | Object |
| data              | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Owner             | 리소스의 소유자                                             | Object |
| uin               | 사용자 QQ 번호                                                     | String |
| AccessControlList | 권한 받은 자 정보 및 권한 정보 | Object |
| Grant             | 구체적인 라이센싱 정보                                               | Array  |
| Permission        | 권한, 열거형 값: READ，WRITE，FULL_CONTROL                  | String |
| Grantee           | 권한 부여받은 자의 리소스 정보                                            | Object |
| uin               | 권한 부여받은 자의 QQ 번호 또는 'anonymous'                           | String |
| Subacount         | 서브 계정 QQ 계정                                               | String |

### Put Object ACL

#### 기능 설명

Put Object ACL은 API를 사용하여 Object의 ACL 리스트를 씁니다. 현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 버킷 권한은 승계됩니다.

#### 작업 방식 프로토타입

 Put Object ACL 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',			/* 필수 */
	Region : 'STRING_VALUE',			/* 필수 */
	Key : 'STRING_VALUE',				/* 필수 */
	ACL : 'STRING_VALUE',				/* 필수 아님 */
	GrantRead : 'STRING_VALUE', 		/* 필수 아님 */
	GrantWrite : 'STRING_VALUE',		/* 필수 아님 */
	GrantFullControl : 'STRING_VALUE'	/* 필수 아님 */
};

cos.putObjectAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region           | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key              | 객체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| ACL              | 사용자 지정 가능한 파일 권한. 유효값: private, public-read, public-read-write, 기본값: private | String | 아니요   |
| GrantRead        | 권한을 부여받은 자에게 읽기 권한 부여, 형식은 x-cos-grant-read: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |
| GrantWrite       | 권한을 부여받은 자에게 쓰기 권한 부여, 형식은 x-cos-grant-write: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID”입니다. | String | 아니요   |
| GrantFullControl | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 x-cos-grant-full-control: uin=" ",uin=" "입니다. <br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", 루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |

### Delete Multiple Object

#### 기능 설명

Delete Multiple Object 요청은 파일 배치 삭제를 할 수 있습니다. 최대 1회 1000개 파일 삭제를 지원합니다. 반환 결과에 대해 COS는 Verbose 및 Quiet의 두 가지 모드를 제공합니다. Verbose 모드는 각 객체의 삭제 결과를 반환하며, Quiet 모드는 오류가 발생한 객체 정보만 반환합니다.

#### 작업 방식 프로토타입

 Delete Multiple Object 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Quiet : 'BOOLEAN_VALUE',						/* 필수 아님 */
	Objects :  [
	    {
	        Key : 'STRING_VALUE'					/* 필수 */
        }
    ]
};

cos.deleteMultipleObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 항목 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region  | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Quiet   | 부울값이며, 이 값은 Quiet 모드 시작 여부를 결정합니다. 값이 True라면 Quiet 모드 시작, False라면 Verbose 모드 시작을 의미합니다. 기본값은 False입니다 | Boolean | 아니요   |
| Objects | 삭제할 파일 리스트                                             | Array   | 아니요   |
| Key            | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형 |
| ------- | ------------------------------------------------------------ | ------ |
| err     | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Deleted | 이번 삭제 성공한 Object의 정보                              | Array  |
| Key            | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String |
| Error   | 이번 삭제 실패한 Object의 정보                               | Array  |
| Key            | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String |
| Code           | 삭제 실패의 오류 코드                                             | String |
| Message | 삭제 오류 메시지                                                 | String |

## 멀티파트 업로드 작업

### Initiate Multipart Upload

#### 기능 설명

Initiate Multipart Upload 요청은 멀티파트 업로드를 초기화합니다. 해당 요청을 성공적으로 실행하면 후속 Upload Part 요청에 사용되는 Upload ID가 반환됩니다.

#### 작업 방식 프로토타입

 Initiate Multipart Upload 호출:

```js
cos.multipartInit({
    Bucket : 'STRING_VALUE',						/* 필수 */
    Region : 'STRING_VALUE',						/* 필수 */
    Key : 'STRING_VALUE',							/* 필수 */
}, function(err, data) {
    if(err) {
        console.log(err);
    } else {
        console.log(data);
    }
});
```

#### 작업 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region             | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key                | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| CacheControl       | RFC 2616에서 정의한 캐시 정책이며, 객체 메타데이터로 저장           | String | 아니요   |
| ContentDisposition | RFC 2616에서 정의한 파일 이름이며, 객체 메타데이터로 저장           | String | 아니요   |
| ContentEncoding    | RFC 2616에서 정의한 인코딩 형식이며, 객체 메타데이터로 저장          | String | 아니요   |
| ContentType        | RFC 2616에서 정의한 내용 유형(MIME)이며, 객체 메타데이터로 저장  | String | 아니요   |
| Expires            | RFC 2616에서 정의한 기한초과 시간이며, 객체 메타데이터로 저장          | String | 아니요   |
| ACL              | 사용자 지정 가능한 파일 권한. 유효값: private, public-read         | String | 아니요   |
| GrantRead          | 권한을 받은 자에게 읽기 권한 부여, 형식은 x-cos-grant-read: uin=" ",uin=" "입니다.<br>서브 계정 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |
| GrantWrite         | 권한을 받은 지에게 쓰기 권한 부여, 형식은 x-cos-grant-write: uin=" ",uin=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID”입니다. | String | 아니요   |
| GrantFullControl | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 x-cos-grant-full-control: uin=" ",uin=" "입니다. <br>서브 계정에 권한을 부여해야 할 경우, uin="RootAcountID/SubAccountID", <br>루트 계정에 권한을 부여해야 할 경우, uin="RootAcountID"입니다. | String | 아니요   |
| StorageClass       | 객체의 스토리지 클래스를 설정합니다. 열거형 값: Standard, Standard_IA, 기본값: Standard(현재는 화남 지역만 지원함) | String  | 아니요   |
| x-cos-meta- *      | 사용자 지정 가능한 헤더 정보, 객체 메타데이터로 반환됩니다. 크기 제한은 2K입니다 | String | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data     | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Bucket   | 멀티파트 업로드의 타겟 버킷                                        | String |
| key | Object 이름                                                | String |
| UploadId | 후속 업로드에서 사용하는 ID                                             | string |

### Upload Part

#### 기능 설명

Upload Part 요청은 초기화 후 멀티파트 업로드를 구현하며, 파트 수량은 1에서 10000까지 지원합니다. 파트의 크기는 1MB~5GB입니다. 각 Upload Part 요청 시 partNumber 및 uploadID가 있어야 하며, partNumber는 파트의 번호로서 비순차적 업로드를 지원합니다.

#### 작업 방식 프로토타입

Upload Part 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Key : 'STRING_VALUE',							/* 필수 */
	ContentLength : 'STRING_VALUE',					/* 필수 */
	Expect : 'STRING_VALUE',						/* 필수 아님 */
	ContentSha1 : 'STRING_VALUE',					/* 필수 아님 */
	PartNumber : 'STRING_VALUE',					/* 필수 */
	UploadId : 'STRING_VALUE',						/* 필수 */
};

cos.multipartUpload(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름        | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket        | 버킷 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region        | 버킷 소재 지역입니다. 열거형 값에 관한 자세한 내용은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key            | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| ContentLength | RFC 2616에 정의된 HTTP 요청 내용의 길이(바이트)입니다                  | String | 아니요   |
| Expect             | Expect=@ 100-continue 사용 시, 서버측에서 확인을 받기 전까지 요청 내용이 전송되지 않습니다 | String             | 아니요   |
| ContentSha1   | RFC 3174에 정의된 160-bit 콘텐츠 SHA-1 알고리즘 인증값              | String | 아니요   |
| PartNumber    | 파트의 번호                                                   | String | 예   |
| UploadId      | 업로드 작업 번호                                                 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data       | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| ETag   | 파트의 ETag 값이며, sha1 알고리즘 인증값                               | String |

### Complete Multipart Upload

#### 기능 설명

Complete Multipart Upload는 전체 멀티파트 업로드를 구현할 수 있습니다. Upload Parts를 사용하여 모든 파트를 업로드한 후, 이 API를 사용하여 업로드를 완료할 수 있습니다. 이 API 사용 시 본문에 각 파트의 PartNumber 및 ETag를 제공하여 파트의 정확성을 인증해야 합니다.

#### 작업 방식 프로토타입

Complete Multipart Upload 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Key : 'STRING_VALUE',							/* 필수 */
	UploadId : 'STRING_VALUE',						/* 필수 */
	Parts : [
		{
			PartNumber : 'STRING_VALUE',			/* 필수 */
			ETag : 'STRING_VALUE'					/* 필수 */
		},
		...
	]
};

cos.multipartComplete(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket     | 버킷 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region     | 버킷 소재 지역입니다. 열거형 값에 관한 자세한 내용은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key        | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| UploadId   | 업로드 태스크 번호                                                 | String | 예   |
| Parts      | 파트의 ETag 정보                                              | Array  | 예   |
| PartNumber | 파트의 번호                                                   | String | 예   |
| ETag       | 파트의 ETag 값, sha1 인증값이며, 인증값 앞뒤에 큰 따옴표를 추가해야 합니다. 예, "3a0f1fd698c235af9cf098cb74aa25bc" | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data     | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Location | 생성된 Object의 공중망 액세스 도메인 이름                                 | String |
| Bucket   | 멀티파트 업로드의 대상 버킷                                        | String |
| key | Object 이름                                                | String |
| ETag     | 병합 후 파일의 MD5 알고리즘 인증값                                      | String   |

### List Parts

#### 기능 설명

List Parts는 특정 멀티파트 업로드에서 이미 업로드된 파트를 조회하는 데 사용됩니다.

#### 작업 방식 프로토타입

List Parts 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Key : 'STRING_VALUE',							/* 필수 */
	UploadId : 'STRING_VALUE',						/* 필수 */
	EncodingType : 'STRING_VALUE',					/* 필수 아님 */
	MaxParts : 'STRING_VALUE',						/* 필수 아님 */
	PartNumberMarker : 'STRING_VALUE'				/* 필수 아님 */
};

cos.multipartListPart(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region           | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key              | 객체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| UploadId         | 업로드 태스크 번호                                                 | String | 예   |
| EncodingType     | 반환값의 인코딩 방식을 지정합니다                                         | String | 아니요   |
| MaxParts         | 1회에 반환하는 최대 항목 수, 기본값은 1000                             | String | 아니요   |
| PartNumberMarker | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 열거 항목은 marker부터 시작합니다  | String | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름               | 매개변수 설명                                                     | 유형   |
| -------------------- | ------------------------------------------------------------ | ------ |
| err                  | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data                  | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Bucket               | 멀티파트 업로드의 대상 버킷                                        | String |
| Encoding-type        | 반환값의 인코딩 방식을 지정합니다                                         | String |
| Key                  | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String |
| UploadID             | 이번 멀티파트 업로드의 ID                                        | String |
| Initiator            | 해당 업로드 개시자의 정보이며, 서브 노드에는 UID가 포함됩니다                 | Object |
| UID                  | 개발자 APPID                                                 | String |
| Owner                | 해당 파트의 소유자 정보를 나타내는 데 사용되며, 서브 노드에는 UID가 포함됩니다                 | Object |
| UID                  | 소유자 QQ 번호                                                    | String |
| StorageClass         | 파트의 스토리지 클래스, 열거형 값: Standard，Standard_IA    | String      |
| - PartNumberMarker     | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 열거 항목은 marker부터 시작합니다  | String |
| NextPartNumberMarker | 반환 항목이 잘리면 NextMarker를 반환하며 다음 항목이 시작점이 됩니다   | String |
| - MaxParts             | 1회에 반환하는 최대 항목 수                                       | String |
| IsTruncated    | 반환 항목의 잘라내기 여부, 'true' 또는 'false'                      | String   |
| Part                 | 멀티파트 정보 그룹                                                 | Array  |
| PartNumber           | 멀티파트 번호                                                     | String |
| LastModified         | 파트 최후 수정 시간                                               | String |
| Etag                 | 멀티파트의 SHA-1 알고리즘 인증값                                        | String |
| Size                 | 멀티파트 크기, 단위 Byte                                            | String |

### Abort Multipart Upload

#### 기능 설명

Abort Multipart Upload는 멀티파트 업로드를 취소하고 이미 업로드된 파트를 삭제하는 데 사용됩니다. Abort Multipart Upload 호출 시, 이 Upload Parts 업로드 파트를 사용 중일 때 요청이 있으면 Upload Parts는 실패를 반환합니다.

#### 작업 방식 프로토타입

Abort Multipart Upload 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Key : 'STRING_VALUE',							/* 필수 */
	UploadId : 'STRING_VALUE'						/* 필수 */
};

cos.multipartAbort(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | Bucket 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region   | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key            | 개체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [개체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| UploadId      | 업로드 작업 번호                                                 | String | 예   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err            | 요청에서 오류 발생 시 반환되는 개체, 네트워크 오류 및 비즈니스 오류를 포함하며, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비어 있습니다 | Object |
| data       | 요청 성공 시 반환되는 개체, 요청 오류 시 비어 있습니다                         | Object |
| MultipartAbortSuccess | Multipart Abort 성공 여부                                     | Boolean |

### List Multipart Uploads

#### 기능 설명

List Multiparts Uploads는 진행 중인 멀티파트 업로드를 조회하는 데 사용됩니다. 1회 최대 1000개의 진행 중인 멀티파트 업로드를 나열할 수 있습니다.

#### 작업 방식 프로토타입

List Multipart Uploads 호출:

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 필수 */
	Region : 'STRING_VALUE',						/* 필수 */
	Delimiter : 'STRING_VALUE',						/* 필수 아님 */
	EncodingType : 'STRING_VALUE',					/* 필수 아님 */
	Prefix : 'STRING_VALUE',						/* 필수 아님 */
	MaxUploads : 'STRING_VALUE',					/* 필수 아님 */
	KeyMarker : 'STRING_VALUE',						/* 필수 아님 */
	UploadIdMarker : 'STRING_VALUE'					/* 필수 아님 */
};

cos.multipartList(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | 버킷 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region         | 버킷 소재 지역입니다. 열거형 값에 관한 자세한 내용은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Delimiter      | 구분 기호는 하나의 부호입니다. Prefix가 있을 경우, 해당 Prefix와 delimiter 사이에 동일한 경로를 같은 종류로 분류하고, Common Prefix로 정의합니다. 그런 다음 모든 Common Prefix를 나열합니다. Prefix가 없을 경우, 경로 시작점에서 시작합니다 | String | 아니요   |
| EncodingType   | 반환값의 인코딩 방식을 규정합니다                                         | String | 아니요   |
| Prefix         | 접두사 매칭, 반환되는 객체 키 접두사 주소 지정에 사용합니다                       | String | 아니요   |
| MaxUploads     | 1회에 반환하는 최대 항목 수, 기본값은 1000                             | String | 아니요   |
| KeyMarker      | upload-id-marker와 함께 사용합니다.<br><li>upload-id-marker가 지정되지 않았을 때, <br>ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열됩니다.<br> <li>upload-id-marker가 지정되었을 때, <br>ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열되고, <br>ObjectName 알파벳 순서가 key-marker와 같고 UploadID가 upload-id-marker 뒤에 있는 항목을 나열합니다. | String | 아니요   |
| UploadIdMarker | key-marker와 함께 사용합니다.<br><li>key-marker가 지정되지 않았을 때, <br>upload-id-marker는 무시됩니다. <br><li>key-marker가 지정되었을 때, <br>ObjectName 알파벳 순서가 key-marker보다 큰 항목을 나열하고, <br>ObjectName 알파벳 순서가 key-marker와 같고 동시에 UploadID가 upload-id-marker보다 큰 항목을 나열합니다 |String | 아니요   |

</li>

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형 |
| ------------------ | ------------------------------------------------------------ | ------ |
| err                | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data               | 요청 성공 시 반환되는 개체, 요청 오류 시 비어 있습니다                         | Object  |
| Bucket             | 멀티파트 업로드의 대상 버킷                                        | String |
| Encoding-type        | 반환값의 인코딩 방식을 규정합니다                                         | String |
| KeyMarker      | 해당 key 값으로 시작되는 항목을 나열합니다                                      | String |
| UploadIdMarker     | 해당 UploadId 값으로 시작하는 항목을 나열합니다                                 | String |
| NextKeyMarker      | 반환 항목 잘라내기의 경우, 반환되는 NextKeyMarker는 다음 항목의 시작점입니다 | String |
| NextUploadIdMarker | 반환 항목 잘라내기의 경우, 반환되는 UploadId는 다음 항목의 시작점입니다     | String |
| IsTruncated    | 반환 항목의 잘라내기 여부, 'true' 또는 'false'                      | String   |
| delimiter          | 구분 기호는 하나의 부호입니다.Prefix가 있을 경우, 해당 Prefix와 delimiter 사이에 동일한 경로를 같은 종류로 분류하고, 정의는 Common Prefix입니다. 그런 다음 모든 Common Prefix르르 나열합니다.Prefix가 없을 경우, 경로 시작점에서 시작합니다 | String |
| CommonPrefixs      | Prefix와 delimiter 사이의 동일한 경로를 같은 종류로 분류하고, 정의는 Common Prefix입니다 | Array  |
| Prefix       | 접두사 매칭, 반환되는 개체 접두사 주소 지정에 사용합니다                       | String |
| Upload             | Upload의 정보 그룹                                            | Array  |
| Key            | 개체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [개체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   |
| UploadID             | 이번 멀티파트 업로드의 ID 표시                                        | String |
| StorageClass         | 파트의 스토리지 클래스, 열거형값: Standard，Standard_IA        | String |
| Initiator            | 해당 업로드 발신자를 나타내는 데 사용되는 정보이며, 서브 노드에는 UID가 포함됩니다                 | Object |
| UID                  | 개발자 APPID                                                 | String |
| Owner                | 해당 멀티파트의 소유자를 나타내는 데 사용되는 정보이며, 서브 노드에는 UID가 포함됩니다                 | Object |
| UID                  | 소유자 qq                | String |
| Initiated          | 멀티파트 업로드의 시작 시간                                            | String |

### Slice Upload File

#### 기능 설명

Slice Upload File은 파일의 멀티파트 업로드를 구현하는 데 사용합니다.

#### 작업 방식 프로토타입

Slice Upload File 호출:

```js
var params = {
	Bucket: 'STRING_VALUE',	/* 필수 */
	Region: 'STRING_VALUE',	/* 필수 */
	Key: 'STRING_VALUE',	/* 필수 */
	FilePath: 'STRING_VALUE',	/* 필수 */
	SliceSize: 'STRING_VALUE',	/* 필수 아님 */
	AsyncLimit: 'NUMBER_VALUE',	/* 필수 아님 */
    onHashProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    },
};

cos.sliceUploadFile(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 작업 매개변수 설명

| 매개 변수 이름             | 매개 변수 설명                                                     | 유형   | 필수 여부 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket         | Bucket 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String | 예   |
| Region         | Bucket 소재 지역입니다. 열거값에 관한 자세한 내용은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)을 참조하십시오 | String | 예   |
| Key            | 개체 키(Object의 이름), 버킷에서 개체의 유일한 ID입니다. 더 자세한 내용은 [개체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| FilePath       | 로컬 파일 경로                                                 | String   | 예   |
| SliceSize      | 파트 크기                                                     | String   | 아니요   |
| AsyncLimit     | 파트의 동시 업로드 수                                                 | String   | 아니요   |
| onHashProgress | 파일 sha1 값 계산의 진행률 콜백 함수, 콜백은 객체이며 진행률 정보를 포함합니다 | Function | 아니요   |
| onProgress     | 진행률 콜백 함수, 콜백은 객체이며 진행률 정보를 포함합니다                   | Function | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data     | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Location | 생성된 Object의 공중망 액세스 도메인 이름                                 | String |
| Bucket   | 멀티파트 업로드의 대상 버킷                                        | String |
| key | Object 이름                                                | String |
| ETag     | 병합 후 파일의 SHA-1 알고리즘 인증값                                | String   |

#### 진행률 콜백 매개변수

| 매개변수 이름     | 매개변수 설명           | 유형   |
| ---------- | ------------------ | ------ |
| SliceSize  | 파트 크기           | String |
| PartNumber | 업로드 성공한 파트 번호 | Number |
| FileSize   | 파일 총 크기         | Number |

### Slice Copy File

#### 기능 설명

Slice Copy File은 하나의 파일을 소스 경로에서 타겟 경로로 복사하는 것을 구현하는 데 사용합니다. 복사 과정에서 파일 메타 속성과 ACL은 수정될 수 있습니다. 사용자는 이 API를 통해 파일 이동, 파일 이름 바꾸기, 파일 속성 수정과 복제본 생성을 구현할 수 있습니다.

#### 작업 방식 프로토타입

Slice Copy File 작업 호출:

```js
cos.sliceCopyFile({
    Bucket: 'STRING_VALUE',                               /* 필수 */
    Region: 'STRING_VALUE',                               /* 필수 */
    Key: 'STRING_VALUE',                                  /* 필수 */
    CopySource: 'STRING_VALUE', 			  /* 필수 */
    SliceSize: 'NUMBER_VALUE',                            /* 필수 아님 */
    onProgress:function (progressData) {                  /* 필수 아님 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});

```

#### 작업 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket     | 버킷 이름입니다. 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String   | 예   |
| Region     | 버킷 소재 지역입니다. 열거형 값에 관한 자세한 내용은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String   | 예   |
| Key        | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 예   |
| CopySource | 소스 파일 URL 경로이며, versionid 서브리소스를 통해 역대 버전을 지정할 수 있습니다       | String   | 예   |
| ChunkSize  | 멀티파트 복사 시 각 파트의 크기 바이트수, 기본값은 1048576(1MB)           | Number   | 아니요   |
| SliceSize  | 멀티파트 복사를 하는 파일 크기, 기본값 5G                            | Number   | 아니요   |
| onProgress | 진행률 콜백 함수, 콜백은 객체이며 진행률 정보를 포함합니다                   | Function | 아니요   |

#### 콜백 함수 설명

```js
function(err, data) { ... }
```

#### 콜백 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 요청에서 오류 발생 시 반환되는 객체, 네트워크 오류 및 비즈니스 오류를 포함하며, 해결 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청 성공 시 비워둡니다 | Object |
| data     | 요청 성공 시 반환되는 객체, 요청 오류 시 비워둡니다                         | Object |
| Location | 생성된 Object의 공중망 액세스 도메인 이름                                 | String |
| Bucket   | 멀티파트 업로드의 대상 버킷                                        | String |
| Key      | 객체 키(Object의 이름), 버킷에서 객체의 유일한 ID입니다. 더 자세한 내용은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String |
| ETag     | 병합 후 파일의 MD5 알고리즘 인증값                                      | String   |
