## 개발 준비

### SDK 획득

COS 서비스의 XML JS SDK 리소스 github 주소: [tencentyun/cos-js-sdk-v5](https://github.com/tencentyun/cos-js-sdk-v5).

데모 다운로드 주소: [XML JS SDK Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo).

### 개발 준비

1. JS SDK는 ajax 파일 업로드와 파일 md5값 계산을 지원할 수 있도록 브라우저가 기본적인 HTML5 특성을 지원해야 합니다.
2. [COS 콘솔](https://console.cloud.tencent.com/cos4)에서 버킷을 생성하고, Bucket(버켓 이름)과 [Region](https://cloud.tencent.com/document/product/436/6224)(지역 이름)을 얻습니다.
3. [콘솔 키 관리](https://console.cloud.tencent.com/capi)에서 프로젝트 SecretId와 SecretKey를 획득합니다.
4. CORS 규칙을 구성합니다. 예시는 다음 그림과 같습니다.
![cors](//mc.qcloudimg.com/static/img/2e7791e9274ce3ebf8b25bbeafcd7b45/image.png)


>?문서에서 나오는 SecretId, SecretKey, Bucket 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.
    
## 시작 가이드		
### 임시 키 획득

키를 프론트 엔드에 놓으면 SecretId와 SecretKey가 노출되기 때문에 영구적인 키에 관련 작업을 백 엔드에서 수행하고, 프론트 엔드는 ajax를 통해 백 엔드에서 하나의 임시 키를 획득합니다. 정식으로 배포할 때 백 엔드에 자신의 사이트 권한을 추가해서 검사합니다. 구체적인 내용은 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048) 문서를 참조하십시오.

### 업로드 예시

1. test.html을 생성하고 다음 코드를 입력한 후에 안에 있는 Bucket과 Region을 수정합니다.
2. 백엔드의 임시 키 서비스를 배포하고, getAuthorization 안의 키 서비스 주소를 수정합니다.
3. test.html을 Web 서버에 놓은 후에 브라우저에서 페이지에 접속하고 파일 업로드를 테스트합니다.

test.html 파일 예제 코드는 다음과 같습니다. 
```
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'test-1250000000';
var Region = 'ap-guangzhou';

// 인스턴스 초기화
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 임시 키 비동기화 획득
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

// 수신자 파일 선택
document.getElementById('file-selector').onchange = function () {
    
    var file = this.files[0];
    if (!file) return;

    // 멀티파트 업로드 파일
    cos.sliceUploadFile({
        Bucket: Bucket,
        Region: Region,
        Key: file.name,
        Body: file,
    }, function (err, data) {
        console.log(err, data);
    });

};
</script>
```


## webpack 도입 방식

webpack 패킹의 시나리오를 지원하며 npm 도입을 모듈로 할 수 있으며 코드는 다음과 같습니다.
```shell
npm i cos-js-sdk-v5 --save
```

## 기타 파일과 예시

1. 더 많은 예시는 [XML JavaScript SDK 데모](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo)를 참조하십시오.
2. 완전한 API 문서는 [XML JavaScript SDK API 문서](https://cloud.tencent.com/document/product/436/12260)를 참조하십시오.

