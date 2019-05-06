> 본문은 JavaScript SDK API에 대해 상세히 소개합니다.

JavaScript SDK github 주소: [tencentyun/cos-js-sdk-v5](https://github.com/tencentyun/cos-js-sdk-v5).

아래 글에서 코드에 나타나는 COS는 SDK의 클래스명을 표시하고 cos는 SDK의 인스턴스를 나타냅니다.

아래 글에서 나타나는 SecretId, SecretKey, Bucket, Region 등 이름의 의미 및 획득 방식은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

아래 글에서 매개변수 이름 앞의 `-`는 "서브 매개변수"를 의미합니다.



## 생성자

### new COS({})

script 태그에 의해 직접적으로 참조될 때, SDK가 전역 변수명 COS를 점용합니다. 해당 생성자를 통해 SDK 인스턴스를 생성할 수 있습니다.

#### 사용 사례

COS SDK 인스턴스 하나를 생성합니다. COS SDK는 다음 몇 가지 형식의 생성을 지원합니다.

- 형식1(추천): 백 엔드는 임시 키를 획득해서 프론트 엔드에 주고 프론트 엔드는 서명을 컴퓨팅합니다.
```js
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버측 JS와 PHP 예시: https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // 서버측 기타 언어는 COS STS SDK 참조: https://github.com/tencentyun/qcloud-cos-sts-sdk
        // STS 상세 문서 가이드: https://cloud.tencent.com/document/product/436/14048
        $.get('http://example.com/server/sts.php', {
            bucket: options.Bucket,
            region: options.Region,
        }, function (data) {
            callback({
                TmpSecretId: data.TmpSecretId,
                TmpSecretKey: data.TmpSecretKey,
                XCosSecurityToken: data.XCosSecurityToken,
                ExpiredTime: data.ExpiredTime, // SDK는 ExpiredTime 시간 전에 다시 getAuthorization을 호출하지 않습니다
            });
        });
    }
});
```

- 형식 2(추천): 제어 권한 세분화. 백 엔드는 임시 키를 획득해서 프론트 엔드에 주며, 프론트 엔드는 동일하게 요청 시에만 임시 키를 반복 사용하고, 백 엔드는 Scope를 통해 제어 권한을 세분화할 수 있습니다.
```js
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버측 예시: https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
        $.ajax({
            method: 'POST',
            url: 'http://example.com/sts-scope.php',
            data: JSON.stringify(options.Scope),
            beforeSend: function () {
                xhr.setRequestHeader('Content-Type', 'application/json');
            },
            dataType: 'json',
            success: function (data) {
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken, // sessionToken을 제공해야 합니다
                    ExpiredTime: data.expiredTime,
                    ScopeLimit: true, // 제어 권한 세분화는 true로 설정해야 하며, 동일 요청일 때에만 키를 반복 사용하도록 제한합니다
                });
            }
        });
    }
});
```

- 형식3(비추천): 프론트 엔드가 요청할 때마다 먼저 getAuthorization을 통해 서명을 획득해야 하며, 백 엔드는 고정 키 또는 임시 키로 서명을 계산해서 프론트 엔드에 반환합니다. 이 형식의 멀티파트 업로드 권한은 제어하기 쉽지 않아서 이 형식의 사용은 권장하지 않습니다.
```
var cos = new COS({
    // 필수 매개변수
    getAuthorization: function (options, callback) {
        // 서버측의 서명 획득은 해당 언어의 COS SDK 참조: https://cloud.tencent.com/document/product/436/6474
        // 주의: 이는 보안 리스크가 있으며 백 엔드는 method, pathname을 통해 엄격하게 권한을 제어해야 합니다(예: put / 불허 등)
        $.get('http://example.com/server/auth.php', {
            method: options.Method,
            pathname: '/' + options.Key,
        }, function (data) {
            callback({
                Authorization: data.authorization,
                // XCosSecurityToken: data.sessionToken, // 임시 키를 사용할 경우 sessionToken을 XCosSecurityToken에 전달해야 합니다
            });
        });
    },
    // 선택 가능한 매개변수
    FileParallelLimit: 3,    // 파일 업로드 동시 발생수 제어
    ChunkParallelLimit: 3,   // 개별 파일에서 멀티파트 업로드 동시 발생수 제어
    ProgressInterval: 1000,  // 업로드의 onProgress 콜백 간격 제어
});
```

- 형식 4(비추천): 프론트 엔드가 고정 키로 서명을 계산하며, 이 형식은 프론트 엔드 디버깅에 적용되고, 이 형식을 사용할 경우 키가 유출되지 않도록 하십시오.
```
var cos = new COS({
    SecretId: 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    SecretKey: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
});
```

#### 생성자 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형     | 필수 항목 여부 |
| ------------------ | ------------------------------------------------------------ | -------- | ---- |
| SecretId           | 사용자의 SecretId                                              | String   | 아니요   |
| SecretKey          | 사용자의 SecretKey, 키가 유출되지 않도록 프론트 엔드 디버깅 시에만 사용하는 것을 권장합니다       | String   | 아니요   |
| FileParallelLimit  | 동일 인스턴스에서 업로드한 파일 동시 발생수, 기본값 3                        | Number   | 아니요   |
| ChunkParallelLimit | 동일 업로드 파일의 멀티파트 동시 발생수, 기본값 3                          | Number   | 아니요   |
| ChunkSize          | 멀티파트 업로드 시 각 파트의 크기 바이트수, 기본값 1048576(1MB)            | Number   | 아니요   |
| ProgressInterval   | 업로드 진행률의 콜백 방식 onProgress의 콜백 빈도, 단위 ms, 기본값 1000 | Number   | 아니요   |
| Protocol           | 사용자 지정의 요청 프로토콜, `https:`, `http:` 선택 가능. 기본적으로 현재 페이지가 `http:`일 때 `http:`를 사용하도록 판단하고, 그렇지 않으면 `https:` 사용 | String   | 아니요   |
| getAthorization    | 서명을 획득하는 콜백 방식, SecretId, SecretKey가 없을 경우 이 매개변수는 필수 선택 | Function | 아니요   |

#### getAuthorization의 콜백 함수 설명(형식1 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization의 콜백 매개변수 설명:

| 매개변수 이름   | 매개변수 설명                                                     | 유형     |
| -------- | ------------------------------------------------------------ | -------- |
| options  | 임시 키를 획득하는 데 필요한 매개변수 객체                                   | Function |
| - Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String   |
| - Region | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String   |
| callback | 임시 키를 획득한 후의 포스트백 방식                                 | Function |

임시 키를 획득한 후에 callback이 하나의 객체를 포스트백하며, 포스트백 객체의 속성 리스트는 다음과 같습니다.

| 속성 이름            | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId       | 획득한 임시 키의 tmpSecretId                             | String | 예   |
| TmpSecretKey      | 획득한 임시 키의 tmpSecretKey                            | String | 아니요   |
| XCosSecurityToken | 획득한 임시 키의 sessionToken, header의 x-cos-security-token 필드에 해당 | String | 아니요   |
| ExpiredTime       | 획득한 임시 키의 expiredTime, 타임아웃 시간                   | String | 아니요   |

#### getAuthorization 콜백 함수 설명(형식2 사용)

```
getAuthorization: function(options, callback) { ... }
```

getAuthorization의 콜백 매개변수 설명:

| 매개변수 이름    | 매개변수 설명                                                     | 유형     | 필수 항목 여부 |
| --------- | ------------------------------------------------------------ | -------- | ---- |
| options   | 서명을 획득하는 데 필요한 매개변수 객체                                       | Function | 아니요   |
| - Method  | 현재 요청 방식                                            | Function | 아니요   |
| - Key     | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID이며, 더 많은 내용은 [객체 키 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | String   | 아니요   |
| - Query   | 현재 요청의 쿼리 매개변수 객체, {key: 'val'}의 형식               | Object   | 아니요   |
| - Headers | 현재 요청의 헤더 매개변수 객체, {key: 'val'}의 형식              | Function | 아니요   |
| callback  | 임시 키를 획득한 후의 콜백                                     | Function | 아니요   |

getAuthorization 계산이 끝난 후에 callback이 하나의 서명 문자열 또는 하나의 객체를 포스트백합니다
서명 문자열을 포스트백할 때 포스트백한 문자열의 유형은 요청에 사용해야 하는 인증 헤더의 자격 증명 필드 Authorization입니다.
객체를 포스트백할 때 포스트백 객체 속성 리스트는 다음과 같습니다.

| 속성 이름            | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | 획득한 임시 키                                         | String | 예   |
| XCosSecurityToken | 획득한 임시 키의 sessionToken, header의 x-cos-security-token 필드에 해당 | String | 아니요   |

#### 인증 자격 증명 획득

인스턴스 자체 인증의 자격 증명은 인스턴스화할 때 전달한 매개변수를 통해 획득 방식을 제어할 수 있으며, 3가지 획득 방식이 있습니다.

1. 인스턴스화할 때 SecretId, SecretKey를 전달하고, 요청할 때마다 서명을 인스턴스 내부에서 계산합니다.
2. 인스턴스화할 때 getAuthorization 콜백을 전달하고, 요청할 때마다 이 콜백을 통해 서명을 계산하여 인스턴스에 반환합니다.
3. 인스턴스화할 때 getSTS 콜백을 전달하고, 요청할 때마다 임시키를 이 콜백을 통해 인스턴스로 반환하며, 인스턴스 내부는 임시 키를 사용하여 서명을 계산합니다.



## 정적 방식

### COS.getAuthorization

COS XML API의 요청에서 사설 리소스 조작은 인증 자격 증명 Authorization이 필요하며, 현재 요청이 유효한지 판단하는 데 사용합니다.

인증 자격 증명 사용 방식은 2가지가 있습니다.

1. header 매개변수에 놓고 사용하며, 필드명: authorization
2. url 매개변수에 놓고 사용하며, 필드명: sign

COS.getAuthorization 방식은 인증 자격 증명(Authorization) 계산에 사용하며 서명 정보의 요청 유효성을 검증하는 데 사용합니다.

> !이 방식은 프론트 엔드 디버깅 시에만 사용을 추천하며, 키가 유출될 리스크가 있어서 프로젝트 런칭은 프론트 엔드 서명 계산 방식을 추천하지 않습니다.

#### 사용 사례

파일 다운로드 인증 자격 증명 획득:

```
var Authorization = COS.getAuthorization({
    SecretId: 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    SecretKey: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    Method: 'get',
    Key: 'a.jpg',
    Expires: 60,
    Query: {},
    Headers: {}
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId  | 사용자의 SecretId                                              | String | 예   |
| SecretKey | 사용자의 SecretKey                                             | String | 예   |
| Method    | 조작 방식, 예를 들면 get, post, delete, head 등 HTTP 방식           | String | 예   |
| Key       | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID이며, **파일에 대한 조작 요청일 경우 파일 이름이고 필수 입력 매개변수**입니다. Bucket에 대한 조작일 경우 비어있습니다 | String | 아니요   |
| Expires   | 서명 타임아웃 시간(초), 기본값 900                                      | Number | 아니요   |
| Query     | 요청의 쿼리 매개변수 객체                                        | Object | 아니요   |
| Headers   | 요청의 헤더 매개변수 객체                                       | Object | 아니요   |

#### 반환값 설명

반환값은 계산으로 얻은 인증 자격 증명 문자열 authorization입니다.



## 도구 방법

### Get Object Url

#### 사용 사례

예시1: 서명이 없는 Object Url을 획득합니다.

```
var url = cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
});
```

예시2: 서명이 있는 Object Url을 획득합니다.

```
var url = cos.getObjectUrl({
    Key: '1.jpg'
});
```

예시3: 서명 프로세스가 비동기화로 획득할 경우 콜백을 통해 서명이 있는 Url을 획득해야 합니다.

```
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

예시4: 사전 서명 Put Object 회득하여 Url을 업로드합니다.

```
cos.getObjectUrl({
    Method: 'PUT',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    console.log(err || data.Url);
});
```

예시5: 파일 Url을 획득하고 파일을 다운로드합니다.

```
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (!err) {
        var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // 강제 다운로드의 매개변수 보완
        window.open(downloadUrl); // 여기에는 새 창에서 url을 엽니다. 현재 창에서 열어야 할 경우 숨겨진 iframe으로 다운로드하거나 앵커 태그 다운로드 속성으로 다운로드를 도울 수 있습니다
    }
});
```

#### 매개변수 설명

| 매개변수 이름  | 매개변수 설명                                                     | 유형    | 필수 항목 여부 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region  | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Key     | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID이며, **파일에 대한 조작 요청일 경우 파일 이름이고 필수 입력 매개변수**입니다. 버킷에 대한 조작일 경우 비어있습니다 | String  | 예   |
| Sign    | 서명이 있는 Url 반환 여부                                       | Boolean | 아니요   |
| Method  | 조작 방식, 예를 들면 get, post, delete, head 등 HTTP 방식, 기본값은 get | String  | 아니요   |
| Query   | 서명 계산에 참여한 쿼리 매개변수 객체                                | Object  | 아니요   |
| Headers | 서명 계산에 참여한 헤더 매개변수 객체                               | Object  | 아니요   |

#### 반환값 설명

반환값은 하나의 문자열이며 2가지 방식으로 반환됩니다.

1. 서명 계산이 동기화로 계산할 수 있을 경우(예: 인스턴스화 과정에서 SecretId와 SecretKey 전달) 서명이 있는 url을 기본으로 반환합니다.
2. 그렇지 않으면 서명이 없는 url을 반환합니다.

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류 코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| data   | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - Url  | 계산하여 얻은 Url                                               | String |

### 브라우저로 파일 다운로드

브라우저 파일 다운로드는 먼저 cos.getObjectUrl을 통해 url을 획득한 후에 자체 다운로드를 호출합니다. 다음 다운로드 사례를 참조하십시오.

브라우저 다운로드 과정은 실제로는 브라우저가 직접 Get Object 요청을 보내는 것이며, 구체적인 매개변수는 cos.getObject 방식을 참조하면 됩니다.

#### 사용 사례

예시1: 파일 url을 획득하고 파일을 다운로드합니다.

```
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (!err) {
        var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // 강제 다운로드의 매개변수 보완
        window.open(downloadUrl); // 여기에는 새 창에서 url을 엽니다. 현재 창에서 열어야 할 경우 숨겨진 iframe으로 다운로드하거나 앵커 태그 다운로드 속성으로 다운로드를 도울 수 있습니다
    }
});
```

예시2: 숨겨진 iframe을 통해 다운로드합니다.

```
<iframe id="downloadTarget" style="width:0;height:0;" frameborder="0"></iframe>
<a id="downloadLink" href="javascript:void(0)">다운로드</a>
<script>
document.getElementById('downloadLink').onclick = function () {
    document.getElementById('downloadTarget').src = downloadUrl; // 예시1에서 획득한 다운로드 url
};
</script>
```

예시3: 숨겨진 앵커 태그의 download 속성을 통해 다운로드합니다.

> !download 속성은 낮은 버전의 브라우저와 호환되지 않습니다.

```
<iframe id="downloadTarget" style="width:0;height:0;" frameborder="0"></iframe>
<!-- 예시1의 downloadUrl을 다음 앵커 태그의 href 매개변수에 넣습니다 -->
<a id="downloadLink" href="{downloadUrl}" download="1.jpg">다운로드</a>
```



## Bucket 작업

### Head Bucket



Head Bucket 요청은 해당 버킷의 존재 여부, 접근 권한 유무를 확인할 수 있습니다. Head의 권한은 Read와 일치합니다. 해당 버킷이 존재할 경우 HTTP 상태 코드 200을 반환합니다. 해당 Bucket에 접근 권한이 없을 경우 HTTP 상태 코드 403을 반환합니다. 해당 Bucket이 존재하지 않을 경우 HTTP 상태 코드 404를 반환합니다. 더 자세한 내용은 [Head Bucket API 설명](https://cloud.tencent.com/document/product/436/7735)을 참조하십시오.

#### 사용 사례

```
cos.headBucket({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',     /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Get Bucket



Get Bucket 요청은 List Object 요청과 동등하며, 해당 Bucket의 일부 또는 전체 객체를 열거할 수 있습니다. 이 API 호출자는 Bucket에 대해 Read 권한이 필요합니다. 더 자세한 사항은 [Get Bucket API 설명](https://cloud.tencent.com/document/product/436/7734)을 참조하십시오.

#### 사용 사례

예시1: 디렉터리 a의 모든 파일을 열거합니다.

```
cos.getBucket({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',     /* 필수 */
    Prefix: 'a/',           /* 필수 아님 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

반환값 형식:

```
{
    "Name": "test-1250000000",
    "Prefix": "",
    "Marker": "a/",
    "MaxKeys": "1000",
    "Delimiter": "",
    "IsTruncated": "false",
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

예시2: 디렉토리 a의 파일을 열거하며 심도 있게 순회(traversal)하지 않습니다.

```
cos.getBucket({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Prefix: 'a/',              /* 필수 아님 */
    Delimiter: '/',            /* 필수 아님 */
}, function(err, data) {
    console.log(err || data.CommonPrefix);
});
```

반환값 형식:

```
{
    "Name": "test-1250000000",
    "Prefix": "a/",
    "Marker": "",
    "MaxKeys": "1000",
    "Delimiter": "/",
    "IsTruncated": "false",
    "CommonPrefixes": [{
        "Prefix": "a/1/"
    }],
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region       | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Prefix       | 접두사 매칭이며, 반환하는 파일 접두사 주소를 지정하는 데 사용합니다                         | String | 아니요   |
| Delimiter    | 구분자는 하나의 구분 기호이며, 일반적으로 "/"을 전달하고, Prefix가 있을 경우 Prefix~delimiter 간의 동일한 경로를 같은 유형으로 분류되고, Common Prefix로 정의한 후에 모든 Common Prefix를 열거합니다. Prefix가 없을 경우 경로 시작점에서 시작합니다 | String | 아니요   |
| Marker       | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 열거 항목은 marker부터 시작합니다  | String | 아니요   |
| MaxKeys      | 1회에 반환하는 최대 항목 수, 기본값 1000                             | String | 아니요   |
| EncodingType | 반환값의 인코딩 방식을 지정합니다. 선택가능한 값 url                            | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름           | 매개변수 설명                                                     | 유형        |
| ---------------- | ------------------------------------------------------------ | ----------- |
| err              | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 작업 에러가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode     | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers        | 요청이 반환하는 헤더 정보                                           | Object      |
| data             | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - headers        | 요청이 반환하는 헤더 정보                                           | Object      |
| - statusCode     | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - CommonPrefixes | Prefix~delimiter 간의 동일한 경로를 같은 유형으로 분류되고, Common Prefix로 정의합니다 | ObjectArray |
| - - Prefix       | 단일 Common의 접두사                                           | String      |
| - - Name         |  Bucket 정보 설명                                           | String      |
| - Prefix         | 접두사 매칭이며, 반환하는 파일 접두사 주소를 지정하는 데 사용합니다                         | String      |
| - Marker         | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 열거 항목은 marker부터 시작합니다  | String      |
| - MaxKeys        | 1회 응답 요청 내에 반환 결화의 최대 항목 수                       | String      |
| - IsTruncated    | 응답 요청 항목이 잘리는지 여부. 문자열. 'True' 또는 'False'          | String      |
| - NextMarker     | 반환 항목이 잘리면 NextMarker를 반환하며 다음 항목의 시작점이 됩니다     | String      |
| - Encoding-Type  | 반환값의 인코딩 방식이며 Delimiter, Marker, Prefix, NextMarker, Key에 작용합니다 | String      |
| - Contents       | 메타데이터 정보                                                   | ObjectArray |
| - - ETag         | 파일의 MD-5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다** | String      |
| - - Size         | 파일 크기, 단위는 바이트                                    | String      |
| - - Key          | 객체 이름                                                   | String      |
| - - LastModified | 객체가 마지막에 수정된 시간. 예를 들어 2017-06-23T12:33:27.000Z       | String      |
| - - Owner        | 버킷 소유자 정보                                            | Object      |
| - ID             | 버킷의 AppID                                              | String      |
| - StorageClass   | Object의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA             | String      |


### List Object Versions

List Object Versions API는 해당 버킷의 일부 또는 전체 객체의 버전을 열거할 수 있습니다. 이 API 호출자는 버킷에 대해 읽기 권한이 있어야 합니다.

#### 사용 사례

예시1: 디렉터리 a의 모든 파일 버전을 열거합니다.

```
cos.listObjectVersions({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',     /* 필수 */
    Prefix: 'a/',           /* 필수 아님 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

반환값 형식:

```
{
    "Name": "test-1250000000",
    "Prefix": "",
    "KeyMarker": "",
    "VersionIdMarker": "",
    "MaxKeys": "1000",
    "IsTruncated": "false",
    "DeleteMarkers": [{
        "Key": "0001.txt",
        "VersionId": "MTg0NDY3NDI1MzM4MzI5OTg5MjM",
        "IsLatest": "false",
        "LastModified": "2018-10-18T15:29:12.000Z",
        "Owner": {"UID": "1250000000"}
    }],
    "Versions": [{
        "Key": "0001.txt",
        "VersionId": "MTg0NDY3NDI1MzM4MzI5OTI2NzU",
        "IsLatest": "true",
        "LastModified": "2018-10-18T15:29:18.000Z",
        "ETag": "\"5a8dd3ad0756a93ded72b823b19dd877\"",
        "Size": "6",
        "StorageClass": "STANDARD",
        "Owner": {"UID": "1250000000"}
    }, {
        "Key": "0001.txt",
        "VersionId": "MTg0NDY3NDI1MzM4MzMwMTk3NzQ",
        "IsLatest": "false",
        "LastModified": "2018-10-18T15:28:51.000Z",
        "ETag": "\"5a8dd3ad0756a93ded72b823b19dd877\"",
        "Size": "6",
        "StorageClass": "STANDARD",
        "Owner": {"UID": "1250000000"}
    }],
    "statusCode": 200,
    "headers": {}
}
```

예시2: 디렉토리 a의 파일을 열거하며 심도 있게 순회(traversal)하지 않습니다.

```
cos.listObjectVersions({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Prefix: '',              /* 필수 아님 */
    Delimiter: '/',            /* 필수 아님 */
}, function(err, data) {
    if (err) {
        console.log(err);
    } else {
        console.log(data.CommonPrefix);
        console.log(data.Conents);
    }
});
```

반환값 형식:

```
{
    "Name": "test-1250000000",
    "Prefix": "1mb.zip",
    "KeyMarker": "",
    "VersionIdMarker": "",
    "MaxKeys": "1000",
    "IsTruncated": "false",
    "DeleteMarkers": [{
        "Key": "1mb.zip",
        "VersionId": "MTg0NDY3NDI1MzM4NzM3NTU1NDE",
        "IsLatest": "true",
        "LastModified": "2018-10-18T04:09:56.000Z",
        "Owner": {"UID": "1250000000"}
    }],
    "Versions": [{
        "Key": "1mb.zip",
        "VersionId": "MTg0NDY3NDI1MzM5Mjg1ODk4OTI",
        "IsLatest": "false",
        "LastModified": "2018-10-17T12:56:01.000Z",
        "ETag": "\"b6d81b360a5672d80c27430f39153e2c\"",
        "Size": "1048576",
        "StorageClass": "STANDARD",
        "Owner": {"UID": "1250000000"}
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region          | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Prefix          | 접두사 매칭이며, 반환하는 파일 접두사 주소를 지정하는 데 사용합니다                         | String | 아니요   |
| Delimiter       | 구분자는 하나의 구분 기호이며, 일반적으로 "/"을 전달하고, Prefix가 있을 경우 Prefix~delimiter 간의 동일한 경로를 같은 유형으로 분류되고, Common Prefix로 정의한 후에 모든 Common Prefix를 열거합니다. Prefix가 없을 경우 경로 시작점에서 시작합니다 | String | 아니요   |
| KeyMarker       | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 Object 열거 항목은 KeyMarker부터 시작합니다 | String | 아니요   |
| VersionIdMarker | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 VersionId 열거 항목은 VersionIdMarker부터 시작합니다 | String | 아니요   |
| MaxKeys         | 1회에 반환하는 최대 항목 수, 기본값 1000                             | String | 아니요   |
| EncodingType    | 반환값의 인코딩 방식을 지정합니다. 선택가능한 값 url                            | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 작업 에러가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode      | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers         | 요청이 반환하는 헤더 정보                                           | Object      |
| data              | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - headers         | 요청이 반환하는 헤더 정보                                           | Object      |
| - statusCode      | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - CommonPrefixes  | Prefix~delimiter 간의 동일한 경로를 같은 유형으로 분류되고, Common Prefix로 정의합니다 | ObjectArray |
| - - Prefix        | 단일 Common의 접두사                                           | String      |
| - - Name          |  Bucket 정보 설명                                           | String      |
| - Prefix          | 접두사 매칭이며, 반환하는 파일 접두사 주소를 지정하는 데 사용합니다                         | String      |
| KeyMarker       | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 Object 열거 항목은 KeyMarker부터 시작합니다 | String      |
| VersionIdMarker | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 VersionId 열거 항목은 VersionIdMarker부터 시작합니다 | String      |
| - MaxKeys         | 1회 응답 요청 내에 반환 결화의 최대 항목 수                       | String      |
| - IsTruncated     | 응답 요청 항목이 잘리는지 여부. 문자열. 'True' 또는 'False'          | String      |
| - NextMarker      | 반환 항목이 잘리면 NextMarker를 반환하며 다음 항목이 시작점이 됩니다     | String      |
| - Encoding-Type   | 반환값의 인코딩 방식이며 Delimiter, Marker, Prefix, NextMarker, Key에 작용합니다 | String      |
| - DeleteMarkers   | 버킷이 여러 버전을 사용하는 경우, 삭제 조작은 기본적으로 DeleteMarker 마크 하나를 추가합니다 | ObjectArray |
| - - ETag          | 파일의 MD-5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다** | String      |
| - - Size          | 파일 크기, 단위는 바이트                                    | String      |
| - - Key           | 객체 이름                                                   | String      |
| - - IsLatest      | 최신 버전 여부, 열거형 값: "true", "false"                        | String      |
| - - LastModified  | 객체가 마지막에 수정된 시간. 예를 들어 2017-06-23T12:33:27.000Z       | String      |
| - - Owner         | 버킷 소유자 정보                                            | Object      |
| - - - ID          | 버킷의 AppID                                              | String      |
| - Versions        | 메타데이터 정보                                                   | ObjectArray |
| - - ETag          | 파일의 MD-5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다 ** | String      |
| - - Size          | 파일 크기, 단위는 바이트                                    | String      |
| - - Key           | 객체 이름                                                   | String      |
| - - IsLatest      | 최신 버전 여부, 열거형 값: "true", "false"                        | String      |
| - - LastModified  | 객체가 마지막에 수정된 시간. 예를 들어 2017-06-23T12:33:27.000Z       | String      |
| - - StorageClass  | Object의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA             | String      |
| - - Owner         | 버킷 소유자 정보                                            | Object      |
| - - - ID          | 버킷의 AppID                                              | String      |

### Delete Bucket



Delete Bucket API 요청은 지정 계정에서 버킷을 삭제할 수 있고, 삭제하기 전에 버킷 내의 내용을 비우도록 요구하며, 버킷 내의 정보를 삭제해야만 버킷 자체를 삭제할 수 있습니다. 삭제에 성공할 경우 반환하는 HTTP 상태 코드가 200 또는 204임에 주의하십시오. 더 자세한 사항은 [Delete Bucket API 설명](https://cloud.tencent.com/document/product/436/7732)을 참조하십시오.

#### 사용 사례

```
cos.deleteBucket({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou'     /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

###  Get Bucket ACL



Get Bucket ACL API는 버킷의 ACL(access control list), 즉 버킷의 접근 권한 제어 리스트를 획득하는 데 사용합니다. 이 API는 버킷의 소유자만 조작할 권한이 있습니다. 더 자세한 사항은 [Get Bucket ACL API 설명](https://cloud.tencent.com/document/product/436/7733)을 참조하십시오.

#### 사용 사례

```
cos.getBucketAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou'     /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 반환 결과 예시

```
{
    "GrantFullControl": "",
    "GrantWrite": "",
    "GrantRead": "",
    "GrantReadAcp": "id=\"qcs::cam::uin/10002:uin/10002\"",
    "GrantWriteAcp": "id=\"qcs::cam::uin/10002:uin/10002\"",
    "ACL": "private",
    "Owner": {
        "ID": "qcs::cam::uin/10001:uin/10001",
        "DisplayName": "qcs::cam::uin/10001:uin/10001"
    },
    "Grants": [{
        "Grantee": {
            "ID": "qcs::cam::uin/10002:uin/10002",
            "DisplayName": "qcs::cam::uin/10002:uin/10002"
        },
        "Permission": "READ"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형        |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err                | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 작업 에러가 포함됩니다. 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다. | Object      |
| - statusCode       | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers          | 요청이 반환하는 헤더 정보                                           | Object      |
| data               | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다                 | Object      |
| - statusCode       | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers          | 요청이 반환하는 헤더 정보                                           | Object      |
| - ACL              | 버킷 소유자 정보                                            | Object      |
| - GrantRead        | 권한을 부여받은 자의 읽기 권한                                         | String      |
| - GrantWrite       | 권한을 부여받은 자의 쓰기 권한                                         | String      |
| - GrantReadAcp     | 권한을 부여받은 자의 Acl과 Policy 읽기 권한                            | String      |
| - GrantWriteAcp    | 권한을 부여받은 자의 Acl과 Policy 쓰기 권한                              | String      |
| - GrantFullControl | 권한을 부여받은 자에게 읽기/쓰기 권한 부여                                         | String      |
| - Owner            | 버킷 소유자 정보                                            | Object      |
| - - DisplayName    | Bucket 소유자 이름                                          | String      |
| - - ID             | Bucket 소유자 ID，<br>형식: qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> <br>루트 계정일 경우 &lt;OwnerUin>과 &lt;SubUin>은 동일 값입니다 | String      |
| - Grants           | 권한을 부여받은 자의 정보와 권한 정보 리스트                                   | ObjectArray |
| - - Permission     | 권한을 부여받은 자에게 부여한 권한 정보, 열거형 값: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      |
| - - Grantee        |  권한을 부여받은 자의 정보. type 유형은 RootAccount, Subaccount일 수 있습니다. <br>type 유형이 RootAccount일 경우 ID에 지정하는 것은 루트 계정입니다. <br>type 유형이 Subaccount일 경우 ID에 지정하는 것은 서브 계정입니다 | Object      |
| - - - DisplayName  | 사용자 이름                                                   | String      |
| - - - ID           | 사용자 ID, <br>루트 계정일 경우 형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin> <br>또는 qcs::cam::anyone:anyone(모든 사용자를 의미)입니다<br>서브 계정일 경우 형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>입니다 | String      |

###  Put Bucket ACL



Put Bucket ACL API는 버킷의 ACL 표를 쓰기 하는 데 사용하며, Header:"x-cos-acl","x-cos-grant-read","x-cos-grant-write","x-cos-grant-full-control"을 통해 ACL 정보를 전달하거나 Body를 통해 XML 형식으로 ACL 정보를 전달할 수 있습니다. 더 자세한 사항은 [Put Bucket ACL API 설명](https://cloud.tencent.com/document/product/436/7737)을 참조하십시오.

#### 사용 사례

버킷 공개 읽기 설정:

```
cos.putBucketAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    ACL: 'public-read'
}, function(err, data) {
    console.log(err || data);
});
```

어떤 사용자에게 버킷 읽기/쓰기 권한 부여:

```
cos.putBucketAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    GrantFullControl: 'id="qcs::cam::uin/1001:uin/1001",id="qcs::cam::uin/1002:uin/1002"' // 1001은 uin입니다
}, function(err, data) {
    console.log(err || data);
});
```

어떤 사용자에게 버킷 읽기/쓰기 권한 부여:

```
cos.putBucketAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    GrantFullControl: 'id="qcs::cam::uin/1001:uin/1001",id="qcs::cam::uin/1002:uin/1002"' // 1001은 uin입니다
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicy를 통해 버킷 권한 수정:

```
cos.putBucketAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy에는 소유자가 있어야 합니다
            "ID": 'qcs::cam::uin/459000000:uin/459000000' // 459000000은 버킷 소유자의 QQ 번호입니다
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/10002:uin/10002", // 10002는 QQ 번호입니다
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름              | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region              | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| ACL                 | Object의 ACL 속성을 정의합니다. 유효값: private, public-read, public-read-write, 기본값: private | String      | 아니요   |
| GrantRead           | 권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고, <br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| GrantWrite          | 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| GrantReadAcp        | 권한을 부여받은 자에게 Acl과 Policy의 읽기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| GrantWriteAcp       | 권한을 부여받은 자에게 Acl과 Policy의 쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| GrantFullControl    | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| AccessControlPolicy | CORS 구성의 모든 정보 리스트                           | Object      | 아니요   |
| - Owner             | 버킷 소유자를 표시하는 객체                                       | Object      | 아니요   |
| - - ID              | 사용자 ID를 나타내는 문자열, 형식 예시, qcs::cam::uin/1001:uin/1001, 1001은 uin입니다 | Object      | 아니요   |
| - Grants            |  CORS 구성의 모든 정보 리스트                           | Object      | 아니요   |
| - - Permission      |  CORS 구성의 모든 정보 리스트, 선택 가능 값 READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      | 아니요   |
| - - Grantee         |  CORS 공유 구성의 모든 정보 리스트                           | ObjectArray | 아니요   |
| - - - ID            | 사용자 ID를 나타내는 문자열, 형식 예시, qcs::cam::uin/1001:uin/1001, 1001은 uin입니다 | String      | 아니요   |
| - - - DisplayName   | 사용자 이름을 표시하는 문자열, 일반작으로 ID와 일치하는 문자열 입력           | String      | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함됩니다. 요청에 성공하면 비워둡니다. [오류코드 문서](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Get Bucket CORS



Get Bucket CORS API는 버킷 소유자가 버킷에서 CORS의 정보 구성 획득을 구현합니다. CORS는 W3C 표준이며, 전체 명칭은 "크로스 도메인 리소스 공유"(Cross-origin Resource Sharing)입니다. 기본으로 버킷의 소유자는 직접 이 API를 사용할 권한이 있으며, 해당 권한을 역시 다른 사용자에게 부여할 수 있습니다. 더 자세한 사항은 [Get Bucket CORS API 설명](https://cloud.tencent.com/document/product/436/8274)을 참조하십시오.

#### 사용 사례

```
cos.getBucketCors({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 반환 결과 예시

```
{
    "CORSRules": [{
        "MaxAgeSeconds": "5",
        "AllowedOrigins": ["*"],
        "AllowedHeaders": ["*"],
        "AllowedMethods": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "ExposeHeaders": ["ETag", "Content-Length", "x-cos-acl", "x-cos-version-id", "x-cos-request-id", "x-cos-delete-marker", "x-cos-server-side-encryption"]
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형        |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err                | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함됩니다. 요청에 성공하면 비워둡니다. [오류코드 문서](https://cloud.tencent.com/document/product/436/7730) | Object      |
| data               | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - CORSRules        |  CORS 구성의 모든 정보 리스트                           | ObjectArray |
| - - AllowedMethods | 허용하는 HTTP 조작, 열거형 값: GET, PUT, HEAD, POST, DELETE       | StringArray |
| - - AllowedOrigins | 허용하는 접근 출처, 와일드카드 * 지원, 형식은 프로토콜://도메인 이름[:포트]입니다. 예: `http://www.qq.com` | StringArray |
| - - AllowedHeaders | OPTIONS 요청을 발송하면 서버측에 그 다음 요청에 사용 가능한 사용자 지정 HTTP 요청 헤더를 알려줍니다. 와일드카드 *를 지원합니다 | StringArray |
| - - ExposeHeaders  | 브라우저가 서버측에서 수신할 수 있는 사용자 지정 헤더 정보를 설정합니다           | StringArray |
| - - MaxAgeSeconds  | OPTIONS 크로스 도메인 정보 캐시 시간(초)을 설정합니다                                | String      |
| - - ID             | 구성 규칙의 ID                                                | String      |


### Put Bucket CORS

> !
> 1. 프론트 엔드에서 CORS 구성을 수정해야 할 경우 해당 버킷 자체가 크로스 도메인을 지원해야 합니다. 콘솔에서 CORS를 구성할 수 있습니다. 자세한 사항은 [개발 환경](https://cloud.tencent.com/document/product/436/13318)을 참조하십시오.
> 2. CORS 구성을 수정할 경우 현재 오리진에서의 크로스 도메인 요청에 영향을 미치지 않도록 주의하십시오.


Put Bucket CORS API는 버킷의 CORS 권한 설정을 요청하는 데 사용합니다. XML 형식의 구성 파일을 가져와서 구성을 구현할 수 있으며, 파일 크기는 64KB로 제한합니다. 기본적으로 버킷의 소유자는 직접 이 API를 사용할 권한이 있으며, 해당 권한을 다른 사용자에게 부여할 수도 있습니다. 더 자세한 사항은 [Put Bucket CORS API 설명](https://cloud.tencent.com/document/product/436/8279)을 참조하십시오.

#### 사용 사례

```
cos.putBucketCors({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    CORSRules: [{
        "AllowedOrigin": ["*"],
        "AllowedMethod": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "AllowedHeader": ["*"],
        "ExposeHeader": ["ETag", "x-cos-acl", "x-cos-version-id", "x-cos-delete-marker", "x-cos-server-side-encryption"],
        "MaxAgeSeconds": "5"
    }]
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ---------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket           | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region           | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| CORSRules        | CORS 구성의 모든 정보 리스트                           | ObjectArray | 아니요   |
| - ID             | 구성 규칙의 ID, 선택 입력 항목                                        | String      | 아니요   |
| - AllowedMethods | 허용하는 HTTP 조작, 열거형 값: GET, PUT, HEAD, POST, DELETE       | StringArray | 예   |
| - AllowedOrigins | 허용하는 접근 출처, 와일드카드 * 지원, 형식은 프로토콜://도메인 이름[:포트]입니다. 예: `http://www.qq.com` | StringArray | 예   |
| - AllowedHeaders | OPTIONS 요청을 발송하면 서버측에 그 다음 요청에 사용 가능한 사용자 지정 HTTP 요청 헤더를 알려줍니다. 와일드카드 *를 지원합니다 | StringArray | 아니요   |
| - ExposeHeaders  | 브라우저가 서버측에서 수신할 수 있는 사용자 지정 헤더 정보를 설정합니다           | StringArray | 아니요   |
| - MaxAgeSeconds  | OPTIONS 요청이 얻는 결과의 유효기간을 설정합니다                            | String      | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함됩니다. 요청에 성공하면 비워둡니다. [오류코드 문서](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Delete Bucket CORS

> !
> 1. 현재 버킷의 CORS 구성 정보를 삭제하면 모든 크로스 도메인 요청이 실패되니 신중하게 조작하십시오.
> 2. 브라우저측에서 이 방법을 사용하는 것을 추천하지 않습니다.



Delete Bucket CORS API 요청은 CORS 구성 정보의 삭제를 구현합니다. 더 자세한 사항은 [Delete Bucket CORS API 설명](https://cloud.tencent.com/document/product/436/8283)을 참조하십시오.

#### 사용 사례

```
cos.deleteBucketCors({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |


### Get Bucket Location

Get Bucket Location API는 버킷이 있는 지역 정보를 획득하는 데 사용합니다. 해당 GET 조작은 location 서브 리소스를 사용하여 버킷이 있는 지역 정보를 반환하고, 버킷 소유자에게만 이 API의 조작 권한을 갖게 됩니다. 더 자세한 사항은 [Get Bucket Location API 설명](https://cloud.tencent.com/document/product/436/8275)을 참조하십시오.

#### 사용 사례

```
cos.getBucketLocation({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름               | 매개변수 설명                                                     | 유형   |
| -------------------- | ------------------------------------------------------------ | ------ |
| err                  | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode         | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers            | 요청이 반환하는 헤더 정보                                           | Object |
| data                 | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode         | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers            | 요청이 반환하는 헤더 정보                                           | Object |
| - LocationConstraint | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String |

### Get Bucket Tagging

Get Bucket Tagging API는 버킷의 Tagging 태그 정보 획득을 구현합니다. 더 자세한 사항은 [Get Bucket Tagging API 설명](https://cloud.tencent.com/document/product/436/8276)을 참조하십시오.

#### 사용 사례

```
cos.getBucketTagging({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 반환 결과 예시

```
{
    "Tags": [
        {"Key": "k1", "Value": "v1"},
        {"Key": "k2", "Value": "v2"}
    ],
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형        |
| ------------ | ------------------------------------------------------------ | ----------- |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object      |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object      |
| - Tags       | 태그 정보                                                     | ObjectArray |
| - - Key      | 태그 이름                                                       | String      |
| - - Value    | 태그 값                                                       | String      |

### Put Bucket Tagging

Put Bucket Tagging API는 버킷의 Tagging 태그 정보 설정을 구현합니다. 더 자세한 사항은 [Put Bucket Tagging API 설명](https://cloud.tencent.com/document/product/436/8276)을 참조하십시오.

#### 사용 사례

```
cos.putBucketTagging({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Tagging: {
        "Tags": [
            {"Key": "k1", "Value": "v1"},
            {"Key": "k2", "Value": "v2"}
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket    | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region    | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| Tagging   | 태그 정보                                                     | Object      | 예   |
| - Tags    | 태그 정보                                                     | ObjectArray | 예   |
| - - Key   | 태그 이름                                                       | String      | 예   |
| - - Value | 태그값                                                       | String      | 예   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |



### Delete Bucket Tagging

Delete Bucket Tagging API는 버킷의 Tagging 태그 정보 삭제를 구현합니다. 더 자세한 사항은 [Delete Bucket Tagging API 설명](https://cloud.tencent.com/document/product/436/8276)을 참조하십시오.

#### 사용 사례

```
cos.deleteBucketTagging({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Get Bucket Policy

Get Bucket Policy API는 버킷 권한 정책 획득을 구현합니다. 더 자세한 사항은 [Get Bucket Policy API 설명](https://cloud.tencent.com/document/product/436/8276)을 참조하십시오.

#### 사용 사례

```
cos.getBucketPolicy({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 반환 결과 예시

```
{
    "Policy": {
        "version": "2.0",
        "Statement": [{
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/10001:uin/10001"]
            },
            "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:test-1250000000/*"],
            "Sid": "costs-1539833197000000307620-46518-39"
        }]
    },
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름          | 매개변수 설명                                                     | 유형        |
| --------------- | ------------------------------------------------------------ | ----------- |
| err             | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| data            | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - Policy        | 권한 정책, [접근 관리 정책 구문](https://cloud.tencent.com/document/product/436/12469#.E8.AE.BF.E9.97.AE.E7.AE.A1.E7.90.86.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) 참조 | Object      |
| - - version     | 버전번호, 2.0으로 고정                                             | ObjectArray |
| - - statement   | 권한 정책 수명 리스트                                             | ObjectArray |
| - - - effect    | 효력, 열거형 값: allow, deny                                    | String      |
| - - - principal | 신분 정보                                                     | ObjectArray |
| - - - - qcs     | 신분 정보 식별 문자열, 형식: qcs::cam::uin/10001:uin/10002, 그 중에서 10001은 루트 계정, 10002는 서브 계정 | String      |
| - - - action    | 정책 효력 발생에 관한 Action 리스트, 와일드카드 * 지원                     | StringArray |
| - - - resource  | 관련된 리소스 식별 문자열 리스트, 형식: qcs::cos:&ltRegion>:uid/&ltAppId>:&ltShortBucketName>/\*, 예: qcs::cos:ap-guangzhou:uid/1250000000:test/\*" | StringArray |
| - - - condition | 허용 또는 사용 금지된 리소스 리스트, 문자열                               | ObjectArray |



### Put Bucket Policy

Put Bucket Policy API는 버킷 권한 정책 규칙 설정을 구현합니다. 더 자세한 사항은 [Put Bucket Policy API 설명](https://cloud.tencent.com/document/product/436/8282)을 참조하십시오.

#### 사용 사례

```
cos.putBucketPolicy({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Policy: {
        "version": "2.0",
        "Statement": [{
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/10001:uin/10001"]
            },
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:test-1250000000/*"],
        }]
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름        | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket        | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region        | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| Policy        | 권한 정책, [접근 관리 정책 구문](https://cloud.tencent.com/document/product/436/12469#.E8.AE.BF.E9.97.AE.E7.AE.A1.E7.90.86.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) 참조 | Object      | 예   |
| - version     | 버전번호, 2.0으로 고정                                             | ObjectArray | 예   |
| - statement   | 권한 정책 수명 리스트                                             | ObjectArray | 예   |
| - - effect    | 효력, 열거형 값: allow, deny                                    | String      | 예   |
| - - principal | 신분 정보                                                     | ObjectArray | 예   |
| - - - qcs     | 신분 정보 식별 문자열, 형식: qcs::cam::uin/10001:uin/10002, 그 중에서 10001은 루트 계정, 10002는 서브 계정 | String      | 예   |
| - - action    | 정책 효력 발생에 관한 Action 리스트, 와일드카드 * 지원                     | StringArray | 예   |
| - - resource  | 관련된 리소스 식별 문자열 리스트, 형식: qcs::cos:&ltRegion>:uid/&ltAppId>:&ltShortBucketName>/\*, 예: qcs::cos:ap-guangzhou:uid/1250000000:test/\*" | StringArray | 예   |
| - - condition | 허용 또는 사용 금지된 리소스 리스트, 문자열                               | ObjectArray | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |



### Delete Bucket Policy

Delete Bucket Policy API는 버킷의 권한 정책을 삭제에 사용합니다. 더 자세한 사항은 [Delete Bucket Policy API 설명](https://cloud.tencent.com/document/product/436/8285)을 참조하십시오.

#### 사용 사례

```
cos.deleteBucketPolicy({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |



### Get Bucket Lifecycle

Get Bucket Lifecycle API는 버킷의 수명 주기 규칙을 획득하는 데 사용합니다. 더 자세한 사항은 [Get Bucket Lifecycle API 설명](https://cloud.tencent.com/document/product/436/8278)을 참조하십시오.

#### 사용 사례

```
cos.getBucketLifecycle({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 반환 결과 예시

```
{
    "Rules": [{
        "ID": "1",
        "Filter": "",
        "Status": "Enabled",
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }, {
        "ID": "2",
        "Filter": {
            "Prefix": "dir/"
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }, {
        "ID": "3",
        "Filter": "",
        "Status": "Enabled",
        "Expiration": {
            "Days": "180"
        }
    }, {
        "ID": "4",
        "Filter": "",
        "Status": "Enabled",
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름                             | 매개변수 설명                                                     | 유형        |
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err                                | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| - statusCode                       | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers                          | 요청이 반환하는 헤더 정보                                           | Object      |
| data                               | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - statusCode                       | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers                          | 요청이 반환하는 헤더 정보                                           | Object      |
| - Rules                            | 요청이 반환하는 헤더 정보                                           | ObjectArray |
| - - ID                             | 규칙의 유일한 식별 ID                                            | String      |
| - - Status                         | 규칙의 활성화 상태, 열거형 값: Enabled, Disabled                    | String      |
| - - Filter                         | 필터링 조건 지정                                                 | String      |
| - - - Prefix                       | 규칙에 매칭시켜야 하는 객체 접두사                                   | String      |
| - - Transition                     | 객체를 보관 클래스로 전환함을 표시                                           | Object      |
| - - - Days                         | 규칙 적용 일수, 파일 업로드 시간에 따라 계산하고, 정수여야 합니다             | Object      |
| - - - StorageClass                 | 전환할 객체 스토리지 클래스 표시, 열거형 값: STANDARD, STANDARD_IA, 기본값: STANDARD | Object      |
| - - Expiration                     | 객체 삭제                                           | Object      |
| - - - Days                         | 규칙 적용 일수, 파일 업로드 시간에 따라 계산하고, 정수여야 합니다             | Object      |
| - - AbortIncompleteMultipartUpload | 조각 삭제                                                 | Object      |
| - - - Days                         | 규칙 적용 일수, 파일 업로드 시간에 따라 계산하고, 정수여야 합니다             | Object      |


### Put Bucket Lifecycle
[Put Bucket Lifecycle API](https://cloud.tencent.com/document/product/436/8280)는 버킷의 생명 주기 규칙을 설정할 수 있습니다.

#### 사용 사례

예시1: 업로드 30일 후에 저빈도 스토리지로 보관합니다.

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Rules: [{
        "ID": "1",
        "Status": "Enabled",
        "Filter": {},
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

예시2: 디렉토리 접두사 `dir/`을 지정하고, 업로드 90일 후에 보관 스토리지로 저장합니다.

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Rules: [{
        "ID": "2",
        "Filter": {
            "Prefix": "dir/",
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

예시3: 업로드 180일 후에 파일을 삭제합니다.

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Rules: [{
        "ID": "3",
        "Status": "Enabled",
        "Filter": {},
        "Expiration": {
            "Days": "180"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

예시4: 업로드 30일 후에 조각을 삭제합니다.

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Rules: [{
        "ID": "4",
        "Status": "Enabled",
        "Filter": {},
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                             | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ---------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                             | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region                             | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| LifecycleConfiguration             | 생명 주기 규칙 지정                                             | Object      | 예   |
| - Rules                            | 요청이 반환하는 헤더 정보                                           | ObjectArray | 예   |
| - - ID                             | 규칙의 유일한 식별 ID                                            | String      | 예   |
| - - Status                         | 규칙의 활성화 상태, 열거형 값: Enabled, Disabled                    | String      | 예   |
| - - Filter                         | 필터링 조건 지정                                                 | String      | 예   |
| - - - Prefix                       | 규칙에 매칭시켜야 하는 객체 접두사                                   | String      | 아니요   |
| - - Transition                     | 객체에 대한 분류 작업                                           | Object      | 아니요   |
| - - - Days                         | 규칙 적용 일수, 파일 업로드 시간에 따라 계산하고, 정수이어야 합니다             | Object      | 예   |
| - - - StorageClass                 | 객체 스토리지에 대한 COS 클래스, 열거형 값: STANDARD, STANDARD_IA, 기본값: STANDARD | Object      | 아니요   |
| - - Expiration                     | 객체 삭제                                           | Object      | 아니요   |
| - - - Days                         | 규칙 적용 일수, 파일 업로드 시간에 따라 계산하고, 정수이어야 합니다             | Object      | 예   |
| - - AbortIncompleteMultipartUpload | 조각 삭제                                                 | Object      | 아니요   |
| - - - Days                         | 규칙 적용 일수, 파일 업로드 시간에 따라 계산하고, 정수이어야 합니다             | Object      | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |


### Delete Bucket Lifecycle

[Delete Bucket Lifecycle API](https://cloud.tencent.com/document/product/436/8284)는 버킷의 생명 주기 규칙을 삭제할 수 있습니다.

#### 사용 사례

```
cos.deleteBucketLifecycle({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Get Bucket Versioning

Get Bucket Versioning API는 버킷의 다중 버전 구성을 획득할 수 있습니다.

#### 사용 사례

```
cos.getBucketVersioning({
    Bucket: 'test-1250000000',  /* 필수 */
    Region: 'ap-guangzhou',     /* 필수 */
}, function (err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름                    | 매개변수 설명                                                     | 유형   |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err                       | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode              | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers                 | 요청이 반환하는 헤더 정보                                           | Object |
| data                      | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode              | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers                 | 요청이 반환하는 헤더 정보                                           | Object |
| - VersioningConfiguration | 버킷의 다중 버전 구성 정보                                       | Object |
| - - Status                | 다중 버전 사용 여부 상태, 열거형 값: 비어 있음, Enabled, Suspended         | String |

### Put Bucket Versioning

Put Bucket Versioning API는 버킷의 다중 버전 구성을 시작 또는 일시 중지할 수 있습니다.

#### 사용 사례

```
cos.putBucketVersioning({
    Bucket: 'test-1250000000',  /* 필수 */
    Region: 'ap-guangzhou',     /* 필수 */
    VersioningConfiguration: {
        Status: "Enabled"
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                  | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ----------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                  | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region                  | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| VersioningConfiguration | 버킷의 다중 버전 구성 정보 정의                                   | Object | 예   |
| - Status                | 다중 버전 활성화 여부, 열거형 값: Enabled, Suspended, Enabled는 활성화, Suspended는 일시 중지 | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Get Bucket Replication

Get Bucket Replication API는 버킷의 크로스 지역 복사 규칙 획득을 구현합니다.

#### 사용 사례

```
cos.getBucketReplication({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 반환 결과 예시

```
{
    "ReplicationConfiguration": {
        "Role": "qcs::cam::uin/459000000:uin/459000000",
        "Rules": {
            "ID": "1",
            "Status": "Enabled",
            "Prefix": "sync/",
            "Destination": {
                "Bucket": "qcs:id/0:cos:ap-chengdu:appid/1250000000:backup",
                "StorageClass": "Standard"
            }
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름                     | 매개변수 설명                                                     | 유형        |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err                        | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| data                       | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - ReplicationConfiguration | 크로스 지역 복사 규칙                                               | Object      |
| - - Role                   | 복사 과정에서 사용하는 역할, 형식: qcs::cam::uin/10001:uin/10002, 그 중에서 10001은 루트 계정, 10002는 서브 계정 | Object      |
| - - Rules                  | 복사의 구체적인 규칙 리스트                                             | ObjectArray |
| - - - ID                   | 태스크 ID                                                  | String      |
| - - - Status               | 규칙 상태, 열거형 값: Enabled, Disabled                          | String      |
| - - - Prefix               | 복사할 객체 접두사                                         | String      |
| - - - Destination          | 복사할 객체 접두사                                         | Object      |
| - - - - Bucket             | 복사 대상 버킷, 형식: qcs:id/0:cos:&lt;Region>:appid/&lt;AppId>:&lt;ShortBucketName>, 예: qcs:id/0:cos:ap-guangzhou:appid/1250000000:backup | Object      |
| - - - - StorageClass       | 복사 후의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA, 기본값: STANDARD | Object      |


### Put Bucket Replication

Put Bucket Replication API는 버킷의 크로스 지역 복사 규칙 설정을 구현합니다.

#### 사용 사례

```
cos.putBucketReplication({
    Bucket: 'test-1250000000',  /* 필수 */
    Region: 'ap-guangzhou',     /* 필수 */
    ReplicationConfiguration: { /* 필수 */
        Role: "qcs::cam::uin/459000000:uin/459000000",
        Rules: [{
            ID: "1",
            Status: "Enabled",
            Prefix: "sync/",
            Destination: {
                Bucket: "qcs:id/0:cos:ap-chengdu:appid/1250000000:backup",
                StorageClass: "Standard",
            }
        }]
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                   | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ------------------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                   | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region                   | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| ReplicationConfiguration | 크로스 지역 복사 규칙 정의                                           | Object      | 예   |
| - Role                   | 복사 과정에서 사용하는 역할, 형식: qcs::cam::uin/10001:uin/10002, 그 중에서 10001은 루트 계정, 10002는 서브 계정 | Object      | 아니요   |
| - Rules                  | 복사의 구체적인 규칙 리스트                                             | ObjectArray | 예   |
| - - ID                   | 태스크 ID                                                  | String      | 아니요   |
| - - Status               | 규칙상태, 열거형 값: Enabled, Disabled                          | String      | 예   |
| - - Prefix               | 복사할 Object 접두사                                         | String      | 아니요   |
| - - Destination          | 복사할 Object 접두사                                         | Object      | 예   |
| - - - Bucket             | 복사 대상 버킷, 형식: qcs:id/0:cos:&lt;Region>:appid/&lt;AppId>:&lt;ShortBucketName>, 예: qcs:id/0:cos:ap-guangzhou:appid/1250000000:backup | Object      | 예   |
| - - - StorageClass       | 복사 후의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA, 기본값: STANDARD | Object      | 아니요   |


#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Delete Bucket Replication

Delete Bucket Replication API는 버킷의 크로스 지역 복사 규칙을 삭제하는 데 사용합니다.

#### 사용 사례

```
cos.deleteBucketReplication({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |



## Object 조작

### Head Object

Head Object API 요청은 해당 객체의 메타 정보 데이터를 획득할 수 있으며, Head의 권한은 Get의 권한과 일치합니다.

#### 사용 사례

```
cos.headObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',               /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region          | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Key             | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |
| IfModifiedSince | 객체가 지정시간 후에 수정되면 해당 객체의 메타데이터를 반환하며, 그렇지 않으면 304를 반환합니다 | String | 아니요   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함됩니다. 요청에 성공하면 비워둡니다. [오류코드 문서](https://cloud.tencent.com/document/product/436/7730) | Object  |
| - statusCode          | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number  |
| - headers             | 요청이 반환하는 헤더 정보                                           | Object  |
| data                  | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object  |
| - statusCode          | 요청이 반환하는 200, 304 등과 같은 HTTP 상태 코드, 지정시간 후에 수정되지 않으면 304를 반환합니다 | Number  |
| - headers             | 요청이 반환하는 헤더 정보                                           | Object  |
| - x-cos-object-type   | 객체를 추가 업로드할 수 있는지 여부를 표시하며, 열거형 값: normal, appendable | String  |
| - x-cos-storage-class | 객체의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA             | String  |
| - x-cos-meta- *       | 사용자 지정의 메타                                            | String  |
| - NotModified         | 객체가 지정시간 후에 수정되지 않었는지 여부                              | Boolean |

### Get Object

Get Object API 요청은 버킷 내의 지정 파일의 내용을 획득할 수 있으며, 획득한 파일 내용이 문자열 형식입니다.

이 조작은 요청자가 대상 객체에 대해 읽기 권한을 갖거나 대상 객체가 모든 사람에게 읽기 권한을 개방(공개 읽기)해야 합니다.

> !이 API는 파일 다운로드에 적용하지 않으며, 파일 다운로드는 cos.getObjectUrl을 통해 url을 획득한 후에 스스로 다운로드할 수 있습니다. 세부 사항은 앞글의 cos.getObjectUrl API를 참조하십시오.

#### 사용 사례

```
cos.getObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Range를 통해 파일 내용 범위 획득:
```
cos.getObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    Range: 'bytes=1-3',        /* 필수 아님 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                     | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region                     | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key                        | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |
| ResponseContentType        | 응답 헤더의 Content-Type 매개변수 설정                           | String | 아니요   |
| ResponseContentLanguage    | 반환 헤더의 Content-Language 매개변수 설정                       | String | 아니요   |
| ResponseExpires            | 반환 헤더의 Content-Expires 매개변수 설정                        | String | 아니요   |
| ResponseCacheControl       | 반환 헤더의 Cache-Control 매개변수 설정                          | String | 아니요   |
| ResponseContentDisposition | 반환 헤더의 Content-Disposition 매개변수 설정                    | String | 아니요   |
| ResponseContentEncoding    | 반환 헤더의 Content-Encoding 매개변수 설정                       | String | 아니요   |
| Range                      | RFC 2616에서 정의한 지정 파일 다운로드 범위이며, 단위는 바이트고, 예 Renge: 'bytes=1-3' | String | 아니요   |
| IfModifiedSince            | 객체가 지정 시간 후에 수정되면 해당 객체 메타 정보를 반환하며, 그렇지 않으면 304를 반환합니다 | String | 아니요   |
| IfUnmodifiedSince          | 파일 수정 시간이 지정 시간보다 빠르거나 같을 경우에만 파일 내용을 반환합니다. 그렇지 않으면 412 (precondition failed)를 반환합니다 | String | 아니요   |
| IfMatch                    | ETag와 지정한 내용이 일치할 경우에만 파일을 반환합니다. 그렇지 않으면 412(precondition failed)를 반환합니다 | String | 아니요   |
| IfNoneMatch                | ETag와 지정한 내용이 불일치해야만 파일을 반환합니다. 그렇지 않으면 304(not modified)를 반환합니다 | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object  |
| - statusCode          | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number  |
| - headers             | 요청이 반환하는 헤더 정보                                           | Object  |
| data                  | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object  |
| - statusCode          | 요청이 반환하는 200, 304, 403, 404 등과 같은 HTTP 상태 코드               | Number  |
| - headers             | 요청이 반환하는 헤더 정보                                           | Object  |
| - x-cos-object-type   | 객체를 추가 업로드할 수 있는지 여부를 표시하며, 열거형 값: normal, appendable | String  |
| - x-cos-storage-class | 객체의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA, <br>**주의: 해당 헤드를 반환하지 않으면 파일 스토리지 클래스가 STANDARD(표준 스토리지)임을 나타냅니다** | String  |
| - x-cos-meta- *       | 사용자 지정의 메타데이터                                           | String  |
| - NotModified         | 요청 시에 IfModifiedSince가 있을 경우 해당 속성을 반환하고, 파일이 수정되지 않은 경우 true이며 그렇지 않으면 false입니다 | Boolean |
| - Body                | 반환하는 파일 내용, 기본으로 String 형식입니다                           | String  |

### Put Object

Put Object API 요청은 로컬 파일(객체)을 지정 버킷에 업로드할 수 있습니다. 이 조작을 하려면 요청자가 버킷에 대해 쓰기 권한이 있어야 합니다.

> !
> 1. Key(파일명)는 `/`로 끝나선 안 되며, 그렇지 않으면 폴더로 식별됩니다.
> 2. 현재 접근 정책 항목을 1000개로 제한하고, 객체 ACL 제어가 필요하지 않을 경우 업로드 시에 설정하지 말고, 기본으로 버킷 권한 상속입니다.
> 3. 업로드 후에 같은 `key`로 예비 서명 링크를 사용할 수 있습니다. 다운로드 시 `GET` 방식을 지정하고(구체적인 API 설명은 아래 참조) 다른 포트로 공유해서 다운로드합니다. 단, 파일이 비공개 읽기 권한일 경우 예비 서명 링크는 일정한 유효기간만 있다는 점에 주의하십시오.

#### 사용 사례

```
cos.putObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    StorageClass: 'STANDARD',
    Body: file, // 파일 객체 업로드
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

문자열을 파일 내용으로 업로드:
```
cos.putObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

문자열을 파일 내용으로 업로드:
```
cos.putObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

디렉터리 생성:
```
cos.putObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: 'a/',              /* 필수 */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형             | 필수 항목 여부 |
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket                 | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String           | 예   |
| Region                     | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String           | 예   |
| Key                    | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String           | 예   |
| CacheControl           | RFC 2616에서 정의한 캐시 정책이며, 객체 메타데이터로 저장           | String           | 아니요   |
| ContentDisposition     | RFC 2616에서 정의한 파일 이름이며, 객체 메타데이터로 저장           | String           | 아니요   |
| ContentEncoding        | RFC 2616에서 정의한 인코딩 형식이며, 객체 메타데이터로 저장           | String           | 아니요   |
| ContentLength          | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)                   | String           | 아니요   |
| ContentType            | RFC 2616에서 정의한 내용 유형(MIME)이며, 객체 메타데이터로 저장   | String           | 아니요   |
| Expect                 | Expect: 100-continue를 사용했을 때 서버측으로부터의 확인을 받아야만 요청 내용을 발송합니다 | String           | 아니요   |
| Expires                | RFC 2616에서 정의한 기한초과 시간이며, 객체 메타데이터로 저장           | String           | 아니요   |
| ACL                    | 객체의 ACL 속성을 정의합니다. 유효값: private, public-read, public-read-write, 기본값: private | String           | 아니요   |
| GrantRead              | 권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고, <br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String           | 아니요   |
| GrantWrite             | 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며, <br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고, <br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String           | 아니요   |
| GrantFullControl       | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며, <br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고, <br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String           | 아니요   |
| StorageClass           | 객체의 스토리지 클래스 설정, 열거형 값: STANDARD, STANDARD_IA, 기본값: STANDARD | String           | 아니요   |
| x-cos-meta- *          | 사용자 지정 가능한 헤더 정보이며, 객체 메타데이터로 반환합니다. 크기는 2K로 제한 | String           | 아니요   |
| Body                   | 업로드 파일의 내용이며 `문자열`, `File 객체` 또는 `Blob 객체`일 수 있습니다  | String\File\Blob | 예   |
| onProgress             | 진행률의 콜백 함수이며, 진행률 콜백 응답 객체(progressData) 속성은 다음과 같습니다     | Function         | 아니요   |
| - progressData.loaded  | 이미 다운로드한 파일 부분 크기이며, 단위는 바이트입니다                | Number           | 아니요   |
| - progressData.total   | 전체 파일의 크기이며, 단위는 바이트입니다                        | Number           | 아니요   |
| - progressData.speed   | 파일의 다운로드 속도이며, 단위는 바이트/초입니다                   | Number           | 아니요   |
| - progressData.percent | 파일 다운로드의 백분율이며, 소수 형식으로 표시됩니다. 예를 들어, 50% 다운로드일 경우 0.5       | Number           | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| - ETag       | 파일의 MD5 알고리즘 검증값을 반환합니다. ETag의 값은 객체가 업로드 과정에서 손상되었는지를 검사하는 데 사용할 수 있습니다.<br>**주의: 여기서 ETag 값 문자열 전후에 큰따옴표가 있습니다. 예 `"09cba091df696af91549de27b8e7d0f6"`** | String |

### Delete Object

Delete Object API 요청은 COS의 버킷에서 하나의 파일(Object)을 삭제할 수 있습니다. 해당 작업은 요청자가 버킷에 대한 쓰기 권한이 있어야 합니다.

#### 사용 사례

```
cos.deleteObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg'                            /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 앱력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key    | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 204, 403, 404 등과 같은 HTTP 상태 코드, **삭제에 성공하거나 파일이 존재하지 않으면 204 또는 200을 반환하고 지정한 버킷을 찾을 수 없으면 404를 반환합니다** | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Options Object

Options Object API는 객체 CORS 구성의 사전 요청(Preflight)을 구현합니다. 즉, 크로스 도메인 요청을 보내기 전에 하나의 OPTIONS 요청을 보내고 COS에 특정 소스 도메인, HTTP 방식과 헤더 정보 등을 전달하고 크로스 도메인 요청을 보낼 수 있는지 여부를 결정합니다. CORS 구성이 존재하지 않을 경우, 요청은 403 Forbidden을 반환합니다.
**Put Bucket CORS API를 통해 버킷에 CORS 지원을 활성화할 수 있습니다.**

#### 사용 사례

```
cos.optionsObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    Origin: 'https://www.qq.com',      /* 필수 */
    AccessControlRequestMethod: 'PUT', /* 필수 */
    AccessControlRequestHeaders: 'origin,accept,content-type' /* 필수 아님 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region                      | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key                         | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |
| Origin                      | CORS의 요청 소스 도메인 이름 시뮬레이션                                   | String | 예   |
| AccessControlRequestMethod  | CORS의 요청 HTTP 방식 시뮬레이션                                 | String | 예   |
| AccessControlRequestHeaders | CORS의 요청 헤더 시뮬레이션                                       | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형    |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err                          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object  |
| - statusCode                 | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number  |
| - headers                    | 요청이 반환하는 헤더 정보                                           | Object  |
| data                         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object  |
| - headers                    | 요청이 반환하는 헤더 정보                                           | Object  |
| - statusCode                 | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number  |
| - AccessControlAllowOrigin   | CORS의 요청 소스 도메인 이름을 시뮬레이션하고, 쉼표로 구분합니다. 리소스가 허용되지 않을 경우 이 헤더는 반환하지 않습니다. 예: \* | String  |
| - AccessControlAllowMethods  | CORS의 요청 HTTP 방식을 시뮬레이션하고, 쉼표로 구분합니다. 요청 방식이 허용되지 않을 경우 이 헤더는 반환하지 않습니다. 예: PUT, GET, POST, DELETE, HEAD | String  |
| - AccessControlAllowHeaders  | CORS의 요청 헤더를 시뮬레이션하고, 쉼표로 구분합니다. 어떤 요청 헤더의 시뮬레이션이 허용되지 않을 경우 이 헤더는 해당 요청 헤더를 반환하지 않습니다. 예: accept, content-type, origin, authorization | String  |
| - AccessControlExposeHeaders | CORS 요청에 지원되는 반환 헤더이며, 쉼표로 구분합니다. 예: ETag                 | String  |
| - AccessControlMaxAge        | OPTIONS 요청이 결과를 얻는 유효기간을 설정합니다. 예: 3600                | String  |
| - OptionsForbidden           | OPTIONS 요청이 금지된 여부이며, 반환하는 HTTP 상태 코드가 403일 경우 true | Boolean |

### Get Object ACL

Get Object ACL API는 하나의 버킷에서 어느 객체의 접근 권한을 획득하는 데 사용합니다. 버킷의 소유자만 이 조작을 할 권한이 있습니다.

#### 사용 사례

```
cos.getObjectAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region | 버킷 소재 지역. 열거형 값은 [버킷 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key    | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| - statusCode      | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers         | 요청이 반환하는 헤더 정보                                           | Object      |
| data              | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - statusCode      | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers         | 요청이 반환하는 헤더 정보                                           | Object      |
| - ACL             | 객체의 ACL 속성입니다. 열거형 값: private, public-read, public-read-write, default | Object      |
| - Owner           | 리소스의 소유자 표시                                             | Object      |
| - - ID            | 객체 소유자 ID, 형식: qcs::cam::uin/&lt;OwnerUin>:uin/lt;SubUin> <br>루트 계정일 경우 &lt;OwnerUin>과 &lt;SubUin>은 동일 값입니다 | String      |
| - - DisplayName   | 객체 소유자의 이름                                          | String      |
| - Grants          | 권한을 부여받은 자의 정보와 권한 정보 리스트                                   | ObjectArray |
| - - Permission    | 권한을 부여받은 자에게 부여한 권한 정보, 열거형 값: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      |
| - - Grantee       | 권한을 부여받은 자의 정보. type 유형은 RootAccount, Subaccount일 수 있습니다. type 유형이 RootAccount일 경우 권한 부여받은 자 ID는 루트 계정입니다. type 유형이 Subaccount일 경우 권한 부여받은 자 ID는 서브 계정입니다 | Object      |
| - - - DisplayName | 사용자 이름                                                   | String      |
| - - - ID          | 사용자 ID, 루트 계정일 경우 형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin> <br>또는 qcs::cam::anyone:anyone(모든 사용자를 의미)입니다. 서브 계정일 경우 <br>형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>입니다 | String      |

### Put Object ACL

Put Object ACL API는 하나의 버킷에서 어느 객체에 대해 ACL 표 구성을 진행하는 데 사용합니다.

>!현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 Bucket 권한은 상속됩니다.

#### 사용 사례

```
cos.putObjectAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    ACL: 'public-read',        /* 필수 아님 */
}, function(err, data) {
    console.log(err || data);
});
```

사용자에게 파일 읽기/쓰기 권한 부여:
```
cos.putObjectAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    GrantFullControl: 'id="qcs::cam::uin/1001:uin/1001",id="qcs::cam::uin/1002:uin/1002"' // 1001은 uin입니다
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicy를 통해 버킷 권한 수정:
```
cos.putObjectAcl({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy에는 소유자가 있어야 합니다
            "ID": 'qcs::cam::uin/459000000:uin/459000000' // 459000000은 버킷 소유자의 QQ 번호입니다
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/10002:uin/10002", // 10002는 QQ 번호입니다
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름              | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region              | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| Key                 | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String      | 예   |
| ACL                 | Object의 ACL 속성을 정의합니다. 유효값: private, public-read, public-read-write, default, 기본값: private. default를 전달할 경우 파일 권한을 지우고, 권한 상속으로 복구 | String      | 아니요   |
| GrantRead           | 권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고, <br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| GrantWrite          | 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| GrantFullControl    | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. <br>형식은 id=" ",id=" "입니다. 서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며, <br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고, <br>예를 들어: 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String      | 아니요   |
| AccessControlPolicy | 객체의 ACL JSON 정의 형식                                  | Object      |      |
| - Owner             | 리소스 소유자 식별                                             | Object      |      |
| - - ID              | 객체 소유자 ID, 형식: qcs::cam::uin/&lt;OwnerUin>:uin/lt;SubUin> <br>루트 계정일 경우 &lt;OwnerUin>과 &lt;SubUin>은 동일 값입니다 | String      |      |
| - - DisplayName     | 객체 소유자의 이름                                          | String      |      |
| - Grants            | 권한을 부여받은 자의 정보와 권한 정보 리스트                                   | ObjectArray |      |
| - - Permission      | 권한을 부여받은 자에게 부여한 권한 정보, 열거형 값: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      |      |
| - - Grantee         | 권한을 부여받은 자의 정보. type 유형은 RootAccount, Subaccount일 수 있습니다. type 유형이 RootAccount일 경우 권한 부여받은 자 ID는 루트 계정입니다. type 유형이 Subaccount일 경우 권한 부여받은 자 ID는 서브 계정입니다 | Object      |      |
| - - - DisplayName   | 사용자 이름                                                   | String      |      |
| - - - ID            | 사용자 ID, 루트 계정일 경우 형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin> <br>또는 qcs::cam::anyone:anyone(모든 사용자를 의)입니다. 서브 계정일 경우 <br>형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>입니다 | String      |      |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 204, 403, 404 등과 같은 HTTP 상태 코드               | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### Delete Multiple Object

Delete Multiple Object API 요청은 지정 버킷에서 객체 일괄 삭제를 구현하며, 1회 요청은 최대 1000개 객체 일괄 삭제를 지원합니다. 응답 결과에 대해 COS는 Verbose와 Quiet 2가지 모드를 제공합니다. Verbose 모드는 각 객체의 삭제 결과를 반환합니다. Quiet 모드는 오류로 보고된 객체 정보만 반환합니다.

#### 사용 사례

다중 파일 반환:

```
cos.deleteMultipleObject({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Objects: [
        {Key: '1.jpg'},
        {Key: '2.zip'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름      | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket      | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region      | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| Quiet       | 부울값, 이 값은 Quiet 모드 작동 여부를 결정합니다. 값이 true이면 Quiet 모드가 작동되고, 값이 false이면 Verbose 모드가 작동되며, 기본값은 false입니다 | Boolean     | 아니요   |
| Objects     | 삭제하려는 파일 리스트                                             | ObjectArray | 예   |
| - Key       | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String      | 예   |
| - VersionId | 삭제하려는 Object 또는 DeleteMarker 버전 ID                      | String      |      |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err                       | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| - statusCode | 요청이 반환하는 200, 204, 403, 404 등과 같은 HTTP 상태 코드               | Number      |
| - headers                 | 요청이 반환하는 헤더 정보                                           | Object      |
| data                      | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - statusCode | 요청이 반환하는 200, 204, 403, 404 등과 같은 HTTP 상태 코드               | Number      |
| - headers                 | 요청이 반환하는 헤더 정보                                           | Object      |
| - Deleted                 |  이번 삭제에 성공한 Object 정보                               | ObjectArray |
| - - Key                   | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String      |
| - - VersionId             | 매개변수가 VersionId를 전달한 경우 반환값에도 VersionId가 포함되며 방금 조작한 Object 또는 DeleteMarker 버전을 표시합니다 | String      |
| - - DeleteMarker          | 다중 버전을 사용하고 매개변수에 VersionId가 없을 경우 이번 삭제는 파일 내용을 지우지 않으며, 하나의 DeleteMarker만 추가해서 볼 수 있는 파일이 이미 삭제됨을 뜻합니다. 열거형 값: true, false | String      |
| - - DeleteMarkerVersionId | 반환한 DeleteMarker가 true일 경우 새로 추가한 DeleteMarker의 VersionId를 반환합니다 | String      |
| - Error                   |  이번 삭제에 실패한 객체 정보                               | ObjectArray |
| - - Key                   | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String      |
| - - Code                  | 삭제 실패의 오류 코드                                             | String      |
| - - Message               | 삭제 오류 메시지                                                 | String      |

### Put Object Copy

Put Object Copy 요청은 1개 파일을 소스 경로에서 타겟 경로로 복사하는 것을 구현합니다. 권장 파일 크기는 1MB ~ 5GB이고 5GB가 넘는 파일은 멀티파트 업로드(Upload - Copy)를 사용하십시오. 복사 과정에서 파일 메타 속성과 ACL은 수정될 수 있습니다. 사용자는 이 API를 통해 파일 복사, 파일 속성 수정(소스 파일과 타겟 파일의 속성은 동일), 파일 이동 또는 이름 바꾸기(먼저 복사한 후에 별도로 삭제 API 호출)를 할 수 있습니다.

#### 사용 사례

```
cos.putObjectCopy({
    Bucket: 'test-1250000000',                               /* 필수 */
    Region: 'ap-guangzhou',                                  /* 필수 */
    Key: '1.jpg',                                            /* 필수 */
    CopySource: 'test1-1250000000.cos.ap-guangzhou.myqcloud.com/2.jpg', /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region                      | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key                         | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |
| CopySource                  | 소스 파일 URL 경로이며, versionid 서브 리소스를 통해 역대 버전을 지정할 수 있습니다       | String | 예   |
| ACL                         | Object의 ACL 속성을 정의합니다. 유효값: private, public-read, public-read-write, 기본값: private | String | 아니요   |
| GrantRead                   | 권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String | 아니요   |
| GrantWrite                  | 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다. <br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String | 아니요   |
| GrantFullControl            | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String | 아니요   |
| MetadataDirective           | 메타데이터 복사 여부, 열거형 값: Copy, Replaced, 기본값은 Copy입니다. Copy로 표기할 경우 헤더에서 사용자 메타데이터 메시지를 무시하고 바로 복사합니다. Replaced로 표기할 경우 헤더 메시지에 따라 메타데이터를 수정합니다. **타겟 경로와 소스 경로가 일치할 경우, 즉 사용자가 메타데이터 수정을 시도하면 반드시 Replaced여야 합니다** | String | 아니요   |
| CopySourceIfModifiedSince   | 객체가 지정시간 이후에 수정된 경우 조작을 실행하고, 그렇지 않으면 412를 반환합니다. **CopySourceIfNoneMatch와 함께 사용할 수 있고, 다른 조건과 함께 사용하면 충돌을 반환합니다** | String | 아니요   |
| CopySourceIfUnmodifiedSince | 객체가 지정시간 이후에 수정되지 않으면 조작을 실행하고, 그렇지 않으면 412를 반환합니다. **CopySourceIfMatch와 함께 사용할 수 있고, 다른 조건과 함께 사용하면 충돌을 반환합니다** | String | 아니요   |
| CopySourceIfMatch           | 객체의 Etag가 주어진 것과 일치할 경우 조작을 실행하고 그렇지 않으면 412를 반환합니다. **CopySourceIfUnmodifiedSince와 함께 사용할 수 있고, 다른 조건과 함께 사용하면 충돌을 반환합니다** | String | 아니요   |
| CopySourceIfNoneMatch       | 객체의 Etag가 주어진 것과 일치하지 않을 경우 조작을 실행하고 그렇지 않으면 412를 반환합니다. **CopySourceIfModifiedSince와 함께 사용할 수 있고, 다른 조건과 함께 사용하면 충돌을 반환합니다** | String | 아니요   |
| StorageClass                | 스토리지 클래스, 열거형 값: Standard, Standard_IA, 기본값: Standard | String | 아니요   |
| x-cos-meta- *               | 기타 사용자 지정의 파일 헤더                                         | String | 아니요   |
| CacheControl                | 모든 캐시 메커니즘이 전체 요청/응답 링크에서 복종해야 하는 명령을 지정합니다            | String | 아니요   |
| ContentDisposition          | MIME 프로토콜의 확장, MIME 프로토콜은 MIME 사용자 에이전트가 첨부된 파일을 어떻게 표시하는지 알려줍니다 | String | 아니요   |
| ContentEncoding             | HTTP에서 「본문 전송에 사용하는 인코딩 형식」에 대해 협상하는 1쌍의 헤더 필드 | String | 아니요   |
| ContentType                 | RFC 2616에서 정의한 HTTP 요청 내용 유형(MIME), 예를 들어, `text/plain` | String | 아니요   |
| Expect                      | 요청의 특정 서버 행동                                       | String | 아니요   |
| Expires                     | 응답 기한초과의 날짜와 시간                                         | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode   | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers      | 요청이 반환하는 헤더 정보                                           | Object |
| data           | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode   | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers      | 요청이 반환하는 헤더 정보                                           | Object |
| - ETag         | 파일의 MD-5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다** | String |
| - LastModified | 객체가 마지막에 수정된 시간, 예를 들어 2017-06-23T12:33:27.000Z       | String |



## 멀티파트 업로드 작업

### Initiate Multipart Upload

Initiate Multipart Upload 요청은 멀티파트 업로드 초기화를 구현하며, 이 요청 실행에 성공한 후에 Upload ID를 반환해서 후속 Upload Part 요청에 사용합니다

#### 사용 사례

```
cos.multipartInit({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region             | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key                | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |
| CacheControl       | RFC 2616에서 정의한 캐시 정책이며, 객체 메타데이터로 저장           | String | 아니요   |
| ContentDisposition | RFC 2616에서 정의한 파일 이름이며, 객체 메타데이터로 저장           | String | 아니요   |
| ContentEncoding    | RFC 2616에서 정의한 인코딩 형식이며, 객체 메타데이터로 저장          | String | 아니요   |
| ContentType        | RFC 2616에서 정의한 내용 유형(MIME)이며, 객체 메타데이터로 저장  | String | 아니요   |
| Expires            | RFC 2616에서 정의한 기한초과 시간이며, 객체 메타데이터로 저장          | String | 아니요   |
| ACL                | 객체의 ACL 속성을 정의합니다. 유효값: private, public-read, public-read-write, 기본값: private | String | 아니요   |
| GrantRead          | 권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고, <br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String | 아니요   |
| GrantWrite         | 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String | 아니요   |
| GrantFullControl   | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식은 id=" ",id=" "입니다.<br>서브 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"이며,<br>루트 계정에 권한을 부여해야 할 경우 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"이고,<br>예를 들어, 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'입니다 | String | 아니요   |
| StorageClass       | 객체의 스토리지 클래스 설정, 열거형 값: STANDARD, STANDARD_IA, 기본값: STANDARD | String | 아니요   |
| x-cos-meta- *      | 사용자 지정 가능한 헤더 정보이며, 객체 메타데이터로 반환합니다. 크기는 2K로 제한 | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| data     | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| Bucket   | 멀티파트 업로드의 타겟 버킷                                        | String |
| Key      | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String |
| UploadId | 후속 업로드에서 사용하는 ID                                        | String |

### Upload Part

Upload Part API 요청은 초기화 이후의 멀티파트 업로드를 구현하고, 지원하는 파트 수는 1 ~ 10000이며, 파트 크기는 1MB ~ 5GB입니다.
Initiate Multipart Upload API로 멀티파트 업로드를 초기화하면 하나의 uploadId를 얻게 되며, 이 ID는 이 멀티파트 데이터를 유일하게 식별할 뿐만 아니라 전체 파일 내에서 이 멀티파트 데이터의 상대적인 위치를 식별합니다. Upload Part를 요청할 때마다 partNumber와 uploadId를 가져야 하며, partNumber는 멀티파트의 번호이고 비순차적 업로드를 지원합니다.
전달한 uploadId와 partNumber는 모두 같을 경우 나중에 전달한 멀티파트는 이전에 전달한 멀티파트를 덮어씁니다. uploadId가 존재하지 않을 경우 404 오류, NoSuchUpload를 반환합니다.

#### 사용 사례

```
cos.multipartUpload({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',       /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름        | 매개변수 설명                                                     | 유형             | 필수 항목 여부 |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket        | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String           | 예   |
| Region        | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String           | 예   |
| Key           | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String           | 예   |
| ContentLength | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)                  | String           | 네   |
| PartNumber    | 멀티파트의 번호                                                   | String           | 예   |
| UploadId      | 업로드 태스크 번호                                                 | String           | 예   |
| Body          | 업로드 멀티파트 파일의 내용이며, `문자열`, `File 객체` 또는 `Blob 객체`일 수 있습니다 | String\File\Blob | 예   |
| Expect        | `Expect: 100-continue`를 사용했을 때 서버측으로부터의 확인을 받아야만 요청 내용을 발송합니다 | String           | 아니요   |
| ContentMD5    | RFC 1864에서 정의한 Base64로 인코딩된 128-bit 내용 MD5 검증값입니다. 이 헤더는 파일 내용에 변화가 발생했는지를 검증에 사용합니다 | String           | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| - ETag       | 파일의 MD-5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다** | String |

### Complete Multipart Upload

Complete Multipart Upload API 요청은 전체 멀티파트 업로드 완성을 구현합니다. Upload Parts를 사용해서 모든 멀티파트를 업로드한 후에는 해당 API를 호출하여 전체 파일의 멀티파트 업로드를 완료해야 합니다. 해당 API를 사용할 경우 멀티파트의 정확성을 검증하도록 요청 본문에서 각 멀티파트의 PartNumber와 ETag를 제시해야 합니다.
멀티파트 업로드가 끝난 후에 합병해야 하고 합병하는 데 몇 분의 시간이 필요하기 때문에 멀티파트를 합병하기 시작할 때 COS가 즉시 200의 상태 코드를 반환합니다. 합병 과정에서 합병이 완료될 때까지 COS는 주기적으로 스페이스 정보를 반환해서 연결이 활성화되도록 유지하고, COS는 본문에서 합병된 후의 멀티파트 내용을 반환합니다.

- 업로드 멀티파트 크기가 1MB보다 작을 경우 해당 API를 호출하면 400 EntityTooSmall을 반환합니다.
- 업로드 멀티파트 번호가 연속되지 않을 경우 해당 API를 호출하면 400 InvalidPart를 반환합니다.
- 요청 본문 중의 멀티파트 정보가 번호 오름차순으로 배열되지 않을 경우 해당 API를 호출하면 400 InvalidPartOrder를 반환합니다.
- UploadId가 존재하지 않을 경우 해당 API를 호출하면 404 NoSuchUpload를 반환합니다.

#### 사용 사례

```
cos.multipartComplete({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.zip',              /* 필수 */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f472941c0fb8c6b7f3528a2', /* 필수 */
    Parts: [
        {PartNumber: '1', ETag: '"0cce40bdbaf2fa0ff204c20fc965dd3f"'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형        | 필수 항목 여부 |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket       | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String      | 예   |
| Region       | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String      | 예   |
| Key          | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String      | 예   |
| UploadId     | 업로드 태스크 번호                                                 | String      | 예   |
| Parts        | 이번 멀티파트 업로드에서 파트의 정보 리스트                           | ObjectArray | 예   |
| - PartNumber | 멀티파트의 번호                                                   | String      | 예   |
| - ETag       | 각 멀티파트의 MD5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다** | String      | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| - Location   | 생성한 객체의 공중망 접근 도메인 이름                                 | String |
| - Bucket     | 멀티파트 업로드의 대상 버킷                                        | String |
| - Key        | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String |
| - ETag       | 합병된 이후 파일의 MD5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다** | String |

### List Parts

List Parts는 특정 멀티파트 업로드에서 이미 업로드한 파트 조회에 사용하며, 즉 지정 UploadId에 속한 모든 이미 업로드에 성공한 멀티파트를 나열합니다.

#### 사용 사례

```
cos.multipartListPart({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.jpg',              /* 필수 */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f47294ec0fb8c6b7f3528a2',                      /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region           | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key              | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |
| UploadId         | 이번 멀티파트 업로드 ID를 식별합니다. Initiate Multipart Upload API로 멀티파트 업로드를 초기화하면 하나의 uploadId를 얻게 되며, 이 ID는 이 멀티파트 데이터를 유일하게 식별할 뿐만 아니라 전체 파일 내에서 이 멀티파트 데이터의 상대적인 위치를 식별합니다. | String | 예   |
| EncodingType     | 반환값의 인코딩 방식을 지정합니다                                         | String | 아니요   |
| MaxParts         | 1회에 반환하는 최대 항목 수, 기본값은 1000                            | String | 아니요   |
| PartNumberMarker | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 열거 항목은 marker부터 시작합니다  | String | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름                 | 매개변수 설명                                                     | 유형        |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err                    | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| - statusCode           | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers              | 요청이 반환하는 헤더 정보                                           | Object      |
| data                   | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - statusCode           | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers              | 요청이 반환하는 헤더 정보                                           | Object      |
| - Bucket               | 멀티파트 업로드의 타겟 버킷                                        | String      |
| Encoding-type        | 반환값의 인코딩 방식을 지정합니다                                         | String      |
| - Key                  | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String      |
| - UploadId             | 이번 멀티파트 업로드의 ID 식별                                        | String      |
| - Initiator            | 이번 업로드 개시자의 정보                                 | Object      |
| - - DisplayName        | 업로드 개시자 이름                                             | String      |
| - - ID                 | 업로드 개시자 ID, 형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>입니다 <br>루트 계정일 경우 &lt;OwnerUin>과 &lt;SubUin>은 동일 값입니다 | String      |
| - Owner                | 멀티파트 소유자의 정보                                 | Object      |
| - - DisplayName        | 버킷 소유자 이름                                          | String      |
| - - ID                 | 버킷 소유자 ID, 일반적으로 사용자의 UIN입니다                           | String      |
| - StorageClass         | 멀티파트의 스토리지 클래스, 열거형 값: Standard，Standard_IA    | String      |
| - PartNumberMarker     | 기본적으로 UTF-8 2진법 순서로 항목을 열거합니다. 모든 열거 항목은 marker부터 시작합니다  | String      |
| - NextPartNumberMarker | 반환 항목이 잘리면 NextMarker를 반환하며 다음 항목이 시작점이 됩니다   | String      |
| - MaxParts             | 1회에 반환하는 최대 항목 수                                       | String      |
| - IsTruncated          | 반환 항목이 잘리는지 여부, 'true' 또는 'false'                      | String      |
| - Part                 | 멀티파트 정보 리스트                                                 | ObjectArray |
| - - PartNumber         | 파트의 번호                                                     | String      |
| - - LastModified       | 파트 마지막 수정시간                                               | String      |
| - - ETag               | 파트의 MD5 알고리즘 검증값                                          | String      |
| - - Size               | 파트 크기, 단위는 바이트                                            | String      |

### Abort Multipart Upload

Abort Multipart Upload는 하나의 멀티파트 업로드를 중단하고 이미 업로드한 파트를 삭제하는 것을 구현합니다. Abort Multipart Upload를 호출하면 이 Upload Parts 업로드 멀티파트가 사용 중인 경우 Upload Parts는 실패를 반환합니다. 해당 UploadId가 존재하지 않으면 404 NoSuchUpload를 반환합니다.

**이미 업로드했지만 중지하지 않은 파티션은 저장 공간을 차지하고 비용이 발생하기 때문에 즉시 멀티파트 업로드를 완료하거나 멀티파트 업로드를 중단하도록 권장합니다.**

#### 사용 사례

```
cos.multipartAbort({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.zip',                           /* 필수 */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f47294ec0fb8c6b7f3528a2'                       /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket   | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String | 예   |
| Region   | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String | 예   |
| Key      | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String | 예   |
| UploadId | 이번 멀티파트 업로드를 식별하는 ID. Initiate Multipart Upload API로 멀티파트 업로드를 초기화하면 하나의 uploadId를 얻게 되며, 이 ID는 이 멀티파트 데이터를 유일하게 식별할 뿐만 아니라 전체 파일 내에서 이 멀티파트 데이터의 상대적인 위치를 식별합니다. | String | 예   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |

### List Multipart Uploads

List Multiparts Uploads는 진행 중인 멀티파트 업로드 조회에 사용합니다. 진행 중인 멀티파트 업로드는 1회에 최대 1000개를 나열합니다.

#### 사용 사례

접두사가 1.zip인 완료되지 않은 UploadId 리스트 획득

```
cos.multipartList({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Prefix: '1.zip',                        /* 필수 아님 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String  | 예   |
| Region       | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String  | 예   |
| Delimiter    | 구분자는 하나의 부호이며, 객체 이름에 포함되 지정 접두사부터 처음 delimiter 문자열까지의 객체를 한 그룹으로 분류하며, common prefix입니다. prefix가 없을 경우 경로 시작지점부터 시작합니다 | String | 아니요   |
| EncodingType | 반환값의 인코딩 형식을 규정하고, 유효한 값: url                            | String | 아니요   |
| Prefix       | 반환하는 Object key는 Prefix를 접두사로 해야 한다고 규정합니다. prefix를 사용해서 조회할 경우 반환하는 key에는 여전히 Prefix가 포함되어 있다는 점에 주의하십시오 | String | 아니요   |
| MaxUploads   | 최대 반환하는 멀티파트 수량을 설정합니다. 유효한 값은 1~1000이며 기본값은 1000   | String | 아니요   |
| KeyMarker    | upload-id-marker와 함께 사용하고, <br> <li> upload-id-marker가 지정되지 않을 경우, <br>ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열되고, <br><li>upload-id-marker가 지정될 경우, <br>ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열되며, <br>ObjectName 알파벳 순서가 key-marker와 같고 UploadID가 upload-id-marker 뒤에 있는 항목이 나열됩니다. | String | 아니요   |
| UploadIdMarker | key-marker와 함께 사용하고, <br><li> key-marker가 지정되지 않을 경우, <br>upload-id-marker는 무시되고, <br><li>key-marker가 지정될 경우, <br>ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열되며, <br>ObjectName 알파벳 순서가 key-marker와 같고 UploadID가 upload-id-marker 뒤에 있는 항목이 나열됩니다. | String | 아니요 |</li>


#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름               | 매개변수 설명                                                     | 유형        |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err                  | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object      |
| - statusCode         | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers            | 요청이 반환하는 헤더 정보                                           | Object      |
| data                 | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object      |
| - statusCode         | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number      |
| - headers            | 요청이 반환하는 헤더 정보                                           | Object      |
| - Bucket             | 멀티파트 업로드의 타겟 버킷                                        | String      |
| - Encoding-Type      | 반환값의 인코딩 형식을 규정하고, 유효한 값: url                            | String      |
| - KeyMarker          | 나열 항목은 해당 키 값부터 시작                                      | String      |
| - UploadIdMarker     | 나열 항목은 해당 UploadId 값부터 시작                                 | String      |
| - NextKeyMarker      | 반환 항목이 잘리면 NextKeyMarker를 반환하며 다음 항목이 시작점이 됩니다 | String      |
| - NextUploadIdMarker | 반환 항목이 잘리면 UploadId를 반환하며 다음 항목이 시작점이 됩니다     | String      |
| - MaxUploads         | 최대 반환하는 멀티파트 수량을 설정하며, 유효한 값은 1~1000입니다          | String      |
| - IsTruncated        | 반환 항목이 잘리는지 여부, 'true' 또는 'false'                      | String      |
| - Delimiter          | 구분 기호는 하나의 부호이며, 객체 이름에 포함된 지정 접두사부터 처음 delimiter 문자열까지의 객체를 한 그룹으로 분류하며, common prefix로 합니다. prefix가 없을 경우 경로 시작지점부터 시작합니다 | String      |
| - Prefix             | 반환하는 Object key는 Prefix를 접두사로 해야 한다고 한정합니다. prefix를 사용해서 조회할 경우 반환하는 key에는 여전히 Prefix가 포함되어 있다는 점에 주의하십시오 | String      |
| - CommonPrefixs      | prefix ~ delimiter 간의 동일한 경로를 같은 유형으로 분류되고, Common Prefix로 정의합니다 | ObjectArray |
| - - Prefix           | 구체적인 CommonPrefixs 표시                                     | String      |
| - Upload             | Upload의 정보 집합                                            | ObjectArray |
| - - Key              | Object의 이름                                                | String      |
| - - UploadId         | 이번 멀티파트 업로드의 ID                                        | String      |
| - StorageClass       | 멀티파트의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA        | String      |
| - Initiator          | 이번 업로드 개시자의 정보                                 | Object      |
| - - DisplayName      | 업로드 개시자 이름                                             | String      |
| - - ID               | 업로드 개시자 ID, 형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> 루트 계정일 경우 &lt;OwnerUin>과 &lt;SubUin>은 동일 값입니다 | String      |
| - Owner              | 멀티파트 소유자의 정보                                 | Object      |
| - - DisplayName      | 버킷 소유자 이름                                          | String      |
| - - ID               | 버킷 소유자 ID, 형식은 qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> 루트 계정일 경우 &lt;OwnerUin>과 &lt;SubUin>은 동일 값입니다 | String      |
| - Initiated          | 멀티파트 업로드의 시작 시간                                           | String      |



## 멀티파트 업로드/복사 태스크

이 유형의 방식은 위의 기존 방식징에 대한 캡슐화로서 멀티파트 업로드/복사의 전체 프로세스를 구현했으며, 동시 발생 멀티파트 업로드/복사를 지원하고, 중단점 업로드 재개, 업로드 작업의 취소, 일시중지와 재시작 등을 지원합니다.

### Slice Upload File

Slice Upload File은 파일의 멀티파트 업로드를 구현하는 데 사용합니다.

#### 사용 사례

```
cos.sliceUploadFile({
    Bucket: 'test-1250000000', /* 필수 */
    Region: 'ap-guangzhou',    /* 필수 */
    Key: '1.zip',              /* 필수 */
    Body: file,                /* 필수 */
    TaskReady: function(taskId) {                   /* 필수 아님 */
        console.log(taskId);
    },
    onHashProgress: function (progressData) {       /* 필수 아님 */
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) {           /* 필수 아님 */
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형      | 필수 항목 여부 |
| ---------------------- | ------------------------------------------------------------ | --------- | ---- |
| Bucket                 | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String    | 예   |
| Region                 | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String    | 예   |
| Key                    | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String    | 예   |
| Body                   | 업로드 파일의 내용이며 File 객체 또는 Blob 객체일 수 있습니다           | File\Blob | 예   |
| SliceSize              | 멀티파트 크기                                                     | String    | 아니요   |
| AsyncLimit             | 동시 업로드된 파트의 수량                                                 | String    | 아니요   |
| StorageClass           | 객체의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA             | String    | 아니요   |
| TaskReady              | 업로드 태스크 생성 시의 콜백 함수이며 하나의 taskId를 반환하고, 업로드 태스크를 유일하게 식별합니다. 업로드 태스크의 취소(cancelTask), 중지(pauseTask)와 재시작(restartTask)에 사용할 수 있습니다 | Function  | 아니요   |
| - taskId               | 업로드 태스크의 번호                                               | String    | 아니요   |
| onHashProgress         | 파일 MD5값을 계산하는 진행률 콜백 함수이고, 콜백 매개변수는 진행률 객체 progressData입니다 | Function  | 아니요   |
| - progressData.loaded  | 이미 검증한 파일 부분 크기, 단위는 바이트                | Number    | 아니요   |
| - progressData.total   | 전체 파일의 크기, 단위는 바이트                        | Number    | 아니요   |
| - progressData.speed   | 파일의 검증 속도, 단위는 바이트/초                   | Number    | 아니요   |
| - progressData.percent | 파일 검증의 백분율이며, 소수 형식으로 표시하고 예를 들어, 50% 다운로드일 경우 0.5    | Number    | 아니요   |
| onProgress             | 업로드 파일의 진행률 콜백 함수이고, 콜백 매개변수는 진행률객체 progressData입니다      | Function  | 아니요   |
| - progressData.loaded  | 이미 업로드한 파일 부분 크기, 단위는 바이트                | Number    | 아니요   |
| - progressData.total   | 전체 파일의 크기, 단위는 바이트                        | Number    | 아니요   |
| - progressData.speed   | 파일의 업로드 속도, 단위는 바이트/초                   | Number    | 아니요   |
| - progressData.percent | 파일 업로드의 백분율이며, 소수 형식으로 표시하고 예를 들어, 50% 다운로드일 경우 0.5    | Number    | 아니요   |


#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| - Location   | 생성한 객체의 공중망 접근 도메인 이름                                 | String |
| - Bucket     | 멀티파트 업로드의 대상 버킷                                        | String |
| - Key        | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String |
| - ETag       | 합병된 이후 파일의 MD5 알고리즘 검증값, 예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **전후에 큰따옴표가 있어야 합니다** | String |

### Cancel Task

taskId에 따라 멀티파트 업로드 태스크를 취소합니다.

#### 사용 사례

```
var taskId = 'xxxxx';                   /* 필수 */
cos.cancelTask(taskId);
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 태스크의 번호이며, sliceUploadFile 방식을 호출했을 때 그 TaskReady 콜백은 해당 업로드 태스크의 taskId를 반환합니다 | String | 예   |

### Pause Task

taskId에 따라 멀티파트 업로드 태스크를 일시중지합니다.

#### 사용 사례

```
var taskId = 'xxxxx';                   /* 필수 */
cos.pauseTask(taskId);
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 태스크의 번호이며, sliceUploadFile 방식을 호출했을 때 그 TaskReady 콜백은 해당 업로드 태스크의 taskId를 반환합니다 | String | 예   |

### Restart Task

taskId에 따라 업로드 태스크를 다시 시작하며, 사용자가 수동으로 중지(pauseTask 호출하여 중지)하거나 업로드 오류로 인해 중지된 업로드 태스크를 시작하는 데 사용합니다.

#### 사용 사례

```
var taskId = 'xxxxx';                   /* 필수 */
cos.restartTask(taskId);
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 항목 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 태스크의 번호이며, sliceUploadFile 방식을 호출했을 때 그 TaskReady 콜백은 해당 업로드 태스크의 taskId를 반환합니다 | String | 예   |

### Slice Copy File

Slice Copy File은 멀티파트 복사를 통해 하나의 파일을 소스 경로에서 타겟 경로로 복사하는 것을 구현하는 데 사용합니다. 복사 과정에서 파일 메타 속성과 ACL은 수정될 수 있습니다. 사용자는 이 API를 통해 파일 이동, 파일 이름 바꾸기, 파일 속성 수정과 복제본 생성을 구현할 수 있습니다.

#### 작업 방식 프로토타입

Slice Copy File 작업 호출:

```
cos.sliceCopyFile({
    Bucket: 'test-1250000000',                               /* 필수 */
    Region: 'ap-guangzhou',                                  /* 필수 */
    Key: '1.zip',                                            /* 필수 */
    CopySource: 'test1.cos.ap-guangzhou.myqcloud.com/2.zip', /* 필수 */
    onProgress:function (progressData) {                     /* 필수 아님 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### 작업 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 항목 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | 버킷 이름. 명명 규칙은 {name}-{appid}이며, 이곳에 입력한 버킷 이름은 반드시 이 형식이어야 합니다 | String   | 예   |
| Region                 | 버킷 소재 지역. 열거형 값은 [Bucket 지역 정보](https://cloud.tencent.com/document/product/436/6224)를 참조하십시오 | String   | 예   |
| Key                    | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String   | 예   |
| CopySource             | 소스 파일 URL 경로이며, versionid 서브리소스를 통해 역대 버전을 지정할 수 있습니다       | String   | 예   |
| ChunkSize              | 멀티파트 복사 시 각 파트의 크기 바이트수, 기본값은 1048576(1MB)           | Number   | 아니요   |
| SliceSize              | 멀티파트 복사를 하는 파일 크기, 기본값 5G                            | Number   | 아니요   |
| onProgress             | 업로드 파일의 진행률 콜백 함수이고, 콜백 매개변수는 진행률 객체 progressData입니다      | Function | 아니요   |
| - progressData.loaded  | 이미 업로드한 파일 부분 크기, 단위는 바이트                | Number   | 아니요   |
| - progressData.total   | 전체 파일의 크기, 단위는 바이트                        | Number   | 아니요   |
| - progressData.speed   | 파일의 업로드 속도, 단위는 바이트/초                   | Number   | 아니요   |
| - progressData.percent | 파일 업로드의 백분율이며, 소수 형식으로 표시하고 예를 들어, 50% 다운로드일 경우 0.5    | Number   | 아니요   |

#### 콜백 함수 설명

```shell
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청에 오류가 발생했을 때 반환하는 객체이며 네트워크 오류와 비즈니스 오류가 포함되고, 처리 조치는 [오류코드 문서](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오. 요청에 성공하면 비워둡니다 | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| data         | 요청에 성공하면 반환하는 객체이며, 요청에 오류가 발생하면 비워둡니다               | Object |
| - statusCode | 요청이 반환하는 200, 403, 404 등과 같은 HTTP 상태 코드                    | Number |
| - headers    | 요청이 반환하는 헤더 정보                                           | Object |
| - Location   | 생성한 객체의 공중망 접근 도메인 이름                                 | String |
| - Bucket     | 멀티파트 업로드의 대상 버킷                                        | String |
| - Key        | 객체 키(객체 이름), 버킷에서 객체의 유일한 ID입니다. [객체 키 설명](https://cloud.tencent.com/document/product/436/13324) | String |
| - ETag       | 합병된 이후 파일의 MD5 알고리즘 검증값, 예 "22ca88419e2ed4721c23807c678adbe4c08a7880", 전후에 큰따옴표가 있어야 합니다 | String |
