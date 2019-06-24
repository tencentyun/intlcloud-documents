## 개발 준비
### SDK 획득

COS 서비스의 XML JS SDK 리소스 github 주소: [tencentyun/cos-nodejs-sdk-v5](https://github.com/tencentyun/cos-nodejs-sdk-v5).

데모 예시 Demo 다운로드 주소: [XML Node.js SDK Demo](https://github.com/tencentyun/cos-nodejs-sdk-v5/tree/master/demo).

### npm 가져오기
개발 전에 먼저 환경 의존을 설치해야 합니다. [npm 주소](https://www.npmjs.com/package/cos-nodejs-sdk-v5).

```
npm i cos-nodejs-sdk-v5 --save
```

### 개발 환경

1. SDK를 사용하려면 실행 환경에 nodejs 및 npm이 포함되어야 하며, nodejs 버전은 7.0 이상을 권장합니다.
2. npm 설치 후, npm 의존 패키지를 설치하고, SDK의 압축 풀기 디렉터리에서 `npm install`을 실행해야 합니다.
3. [콘솔 키 관리](https://console.cloud.tencent.com/capi)에서 프로젝트의 SecretId와 SecretKey를 획득합니다.

>?문서에서 나오는 SecretId, SecretKey, Bucket 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

## 시작 가이드

2. [COS 콘솔](https://console.cloud.tencent.com/cos4)에서 버킷을 생성하고, Bucket(버켓 이름)과 [Region](https://cloud.tencent.com/document/product/436/6224)(지역 이름)을 얻습니다.
2. [콘솔 키 관리](https://console.cloud.tencent.com/capi)에서 프로젝트 SecretId와 SecretKey를 획득합니다.
3. 초기화의 방식은 두 가지가 있습니다. 영구 키 사용 초기화 및 임시 키 사용 초기화입니다.
 - 영구 키를 사용하여 초기화
SecretId, SecretKey, Bucket 및 Region을 실제 개발 환경에서의 값으로 수정하고 파일 업로드를 테스트합니다. 아래 예제 코드를 참조하십시오.
```javascript
// 모듈 가져오기
var COS = require('cos-nodejs-sdk-v5');
// 영구 키를 사용하여 인스턴스 생성
var cos = new COS({
    SecretId: 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    SecretKey: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
});
// 멀티파트 업로드
cos.sliceUploadFile({
    Bucket: 'test-1250000000',
    Region: 'ap-guangzhou',
    Key: '1.zip',
    FilePath: './1.zip'
}, function (err, data) {
    console.log(err, data);
});
```

 - 임시 키를 사용하여 초기화
	임시 키 생성 및 사용은 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오. Node.js SDK는 임시 키 가져오기를 통한 초기화를 지원하며, 다음의 예제 코드를 참조하십시오.
```
// 임시 키를 사용하여 인스턴스 생성
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 비동기 서명 획득
        $.get('../server/sts.php', {
            bucket: options.Bucket,
            region: options.Region,
        }, function (data) {
            callback({
                 TmpSecretId: data.credentials.tmpSecretId,
                 TmpSecretKey: data.credentials.tmpSecretKey,
                 XCosSecurityToken: data.credentials.sessionToken,
                 ExpiredTime: data.expiredTime
            });
        });
    }
});
```

## 관련 문서

1. 더 많은 예시는 [XML Node.js SDK 데모](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/demo/)를 참조하십시오.
2. 전체 API 문서는 [XML Node.js SDK API 문서](https://cloud.tencent.com/document/product/436/12264)를 참조하십시오.
