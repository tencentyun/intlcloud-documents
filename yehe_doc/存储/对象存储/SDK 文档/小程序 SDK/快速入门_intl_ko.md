## 다운로드 및 설치

#### 관련 리소스

- COS의 XML Go SDK 소스 코드 다운로드 주소: [XML Go SDK](https://github.com/tencentyun/cos-go-sdk-v5)
- SDK 고속 다운로드 주소: [XML Java SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip)
- 예시 Demo 다운로드 주소: [COS XML Go SDK 예시](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example)
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/Go)를 참조하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-go-sdk-v5/blob/master/CHANGELOG.md)를 참조하십시오.

#### 환경 종속


1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후, 링크 도용 방지 설정 기능을 활성화하여 화이트리스트를 선택합니다. 자세한 작업 가이드는 [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/436/13319)을 참조하십시오.
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.

>- 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭에 대한 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참조하십시오.

#### SDK 설치



- 수동 설치



```js

```





```plaintext

```



## 사용하기











   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com


### 초기화

```js

```

```js
var cos = new COS({
    
    var getAuthorization = function (options, callback) {
        
        
            
            data: {
                
                
            },
            dataType: 'json',
            
                
                
                
                
                    SecretId: credentials.tmpSecretId,
                    SecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    
                    
                    
                });
            }
        });
    }
});



```

### 설정 항목

#### 사용 예시





```js
var cos = new COS({
    
    var getAuthorization = function (options, callback) {
        
        
        규격과 제한에 대한 자세한 사항은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518) 문서를 참고하십시오.
        
            
            data: {
                
            },
            
                
                
                
                
                    SecretId: credentials.tmpSecretId,
                    SecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    
                    
                    
                });
            }
        });
    }
});
```
>?임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.



```js
var cos = new COS({
    
    var getAuthorization = function (options, callback) {
        
        
            
            
            
                
                
                
                
                    SecretId: credentials.tmpSecretId,
                    SecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken,
                    
                    
                    
                    
                });
            }
        });
    }
});
```

>?임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.



```js
var cos = new COS({
    
    var getAuthorization = function (options, callback) {
        
        
        
            
            
            
                
                
                
                    
                    
                });
            }
        });
    },
});
```



```js
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.
var cos = new COS({
    'secretId'  => $secretId ,
    SecretKey=SECRET_KEY,
});
```



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



| - - Key                   | 객체 키(Object의 이름). 객체는 버킷의 고유 식별자. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324) 참조 | String      |









| ----------------- | ------------------------------------------------------------ | ------ | ---- |













###버킷 생성하기

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```



### 버킷 리스트 조회

```js
cos.getService(function(err, data) {
    
});
```

### 객체 업로드



```js


    
    
    
    success: function (json) {
        
        
        cos.postObject({
            Bucket: 'examplebucket-1250000000',
            Region: 'ap-beijing',
            
            FilePath: filePath1,
            onProgress: function (info) {
                console.log(JSON.stringify(info));
            }
        }, function (err, data) {
            console.log(err || data);
        });
    }
});
```

### 객체 리스트 조회

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    
}, function (err, data) {
    console.log(err || data.Contents);
});
```

### 객체 다운로드



```js
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    'Key': 'exampleobject',
}, function (err, data) {
    console.log(err || data.Body);
});
```

### 객체 삭제

```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: 'picture.jpg',
}, function (err, data) {
    console.log(err || data);
});
```
