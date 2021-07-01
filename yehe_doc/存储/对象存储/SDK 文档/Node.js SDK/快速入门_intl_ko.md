## 다운로드 및 설치

#### 관련 리소스


- SDK 고속 다운로드 주소: [XML Java SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip)
- 예시 Demo 다운로드 주소: [COS XML Go SDK 예시](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example)
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/iOS)를 참조하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-go-sdk-v5/blob/master/CHANGELOG.md)를 참조하십시오.

#### 환경 종속


1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 버킷을 생성하여 Bucket(버킷 이름)과 Region(리전 이름)을 획득합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참조하십시오.
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.

>- 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭에 대한 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참조하십시오.

#### SDK 설치



```bash

```

## 사용하기

### 초기화



>APPID, secretID, secretKey는 [API Keys](https://console.cloud.tencent.com/cam/capi) 페이지에서 받을 수 있습니다.


[//]: # (.cssg-snippet-global-init)
```js
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.

var cos = new COS({
    'secretId'  => $secretId ,
    SecretKey=SECRET_KEY,
});
```



>?임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.

[//]: # (.cssg-snippet-global-init-sts)
```js


var cos = new COS({
    var getAuthorization = function (options, callback) {
        
        
            
            data: {
                
            }
        
            try{
                
                
            } catch (e) {}
            
            
                
                
                
                
            });
        });
    }
});
```



### 설정 항목



| 매개변수 이름                     | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |





| ChunkSize              | 블록 복사 시 블록의 바이트 수 기본값은 1048576(1MB)입니다.          | Number   | 아니오   |





| Protocol               | 요청 시 사용하는 프로토콜. 옵션 항목으로 `https:`와 `http:`가 있습니다. 기본적으로 현재 페이지가 `http:`인 경우 `http:`를 사용하고, 아닌 경우 `https:`를 사용합니다. | String   | 아니요   |

| Domain                 | 버킷 및 객체 작업 API 호출 시 요청 도메인을 사용자 정의합니다. `"{Bucket}.cos.{Region}.myqcloud.com" `과 같은 템플릿을 사용할 수 있으며, API 호출 시 매개변수로 전달하는 Bucket 및 Region으로 변경할 수 있습니다. | String   | 아니요   |












```
var getAuthorization = function (options, callback) {
```



| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | -------- |

| Bucket       | 버킷의 이름 생성 규칙은 BucketName-APPID이며, 여기에 입력되는 버킷 이름은 반드시 포맷을 따라야 합니다. | String | 예   |
| Region                     | 버킷이 위치한 리전. 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 참조 | String   | 예   |





| ----------------- | ------------------------------------------------------------ | ------ | ---- |








```
var getAuthorization = function (options, callback) {
```



| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ---------- | ------------------------------------------------------------ | -------- |



| - Key                  | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String      |










| ----------------- | ------------------------------------------------------------ | ------ | ---- |











###버킷 생성하기

[//]: # (.cssg-snippet-put-bucket)
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

### 버킷 리스트 조회

[//]: # (.cssg-snippet-get-service)
```js
cos.getService(function(err, data) {
    
});
```

### 객체 업로드



[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    StorageClass: 'STANDARD',
    
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

### 객체 리스트 조회

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',     /* 필수 */
    Prefix: 'a/',           /* 선택 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### 객체 다운로드

[//]: # (.cssg-snippet-get-object-stream)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject',              /* 필수 */
    Output: fs.createWriteStream('./exampleobject'),
}, function(err, data) {
    console.log(err || data);
});
```

### 객체 삭제

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'exampleobject'                            /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```
