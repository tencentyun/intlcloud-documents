## 다운로드 및 설치

#### 관련 리소스

- COS 서비스의 XML Java SDK 소스 코드 다운로드 주소: [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5)
- SDK 고속 다운로드 주소: [XML Java SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip)
- 예시 Demo 다운로드 주소: [COS XML Go SDK 예시](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example)
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/Java)를 참조하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-go-sdk-v5/blob/master/CHANGELOG.md)를 참조하십시오.

## 환경 준비


[COS 콘솔](https://console.cloud.tencent.com/cos/bucket)에서 버킷을 생성합니다. 요구사항에 따라 버킷 권한을 개인 읽기/쓰기 또는 공개 읽기/개인 쓰기로 설정할 수 있습니다. 자세한 단계에 관한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)과 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)을 참조하십시오.
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.

   ![cors](https://main.qcloudimg.com/raw/eb73177a2302ad976be301254bcd9630.png)

>- 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭에 대한 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참조하십시오.

#### SDK 설치





```html
<script src="https://unpkg.com/cos-js-sdk-v5/dist/cos-js-sdk-v5.min.js"></script>
```







```js

```

## 사용하기

## 임시 키 획득





### 초기화





```html
<input id="fileSelector" type="file">

<script>
var Bucket = 'examplebucket-1250000000';



var cos = new COS({
    var getAuthorization = function (options, callback) {
        
        
            
            
        
            
            
            
                SecretId: credentials.tmpSecretId,
                SecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                
                
                
            });
        });
    }
});




</script>
```

### 설정 항목

#### 사용 예시





[//]: # (.cssg-snippet-global-init-sts)
```js

var cos = new COS({
    
    var getAuthorization = function (options, callback) {
        
        
        규격과 제한에 대한 자세한 사항은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518) 문서를 참고하십시오.
        
            
        
            
            
            
                SecretId: credentials.tmpSecretId,
                SecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                
                
                
            });
        });
    }
});
```



[//]: # (.cssg-snippet-global-init-sts)
```js

var cos = new COS({
    
    var getAuthorization = function (options, callback) {
        
        $.ajax({
            
            
            
            
                
            },
            dataType: 'json',
            success: function (json) {
                
                
                
                    SecretId: credentials.tmpSecretId,
                    SecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    
                    
                    
                    
                });
            }
        });
    }
});
```



[//]: # (.cssg-snippet-global-init-sts)
```js
var cos = new COS({
    
    var getAuthorization = function (options, callback) {
        
        
        
            Method: options.Method,
            
        
            
            
                
                
            });
        });
    },
    
    
    
    
});
```



[//]: # (.cssg-snippet-global-init)
```js
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.
var cos = new COS({
    'secretId'  => $secretId ,
    SecretKey=SECRET_KEY,
});
```



| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |





| ChunkSize              | 블록 복사 시 블록의 바이트 수 기본값은 1048576(1MB)입니다.          | Number   | 아니오   |





| Protocol               | 요청 시 사용하는 프로토콜. 옵션 항목으로 `https:`와 `http:`가 있습니다. 기본적으로 현재 페이지가 `http:`인 경우 `http:`를 사용하고, 아닌 경우 `https:`를 사용합니다. | String   | 아니요   |
| Domain                 | 버킷 및 객체 작업 API 호출 시 요청 도메인을 사용자 정의합니다. `"{Bucket}.cos.{Region}.myqcloud.com" `과 같은 템플릿을 사용할 수 있으며, API 호출 시 매개변수로 전달하는 Bucket 및 Region으로 변경할 수 있습니다. | String   | 아니요   |








```
var getAuthorization = function (options, callback) {
```



| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | -------- |

| Bucket             | 이름 생성 포맷이 BucketName-APPID인 버킷 이름. 여기에 입력되는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String | 예   |
| Region                     | 버킷이 위치한 리전. 열거 값은 [리전과 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 참조 | String   | 예   |




| 매개변수 이름                     | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |








```
var getAuthorization = function (options, callback) {
```



| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ---------- | ------------------------------------------------------------ | -------- |



| - - Key                   | 객체 키(Object의 이름). 객체는 버킷의 고유 식별자. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324) 참조 | String      |








| 매개변수 이름                     | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |













### 객체 업로드



[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    
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
    
    Prefix: 'a/',           /* 옵션 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

### 객체 다운로드



[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    
    Key: 'exampleobject',              /* 필수 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

### 객체 삭제

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* 필수 */
    
    Key: 'exampleobject'                            /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```
