## 소개
본 문서에서는 SDK를 사용하지 않고 미니프로그램을 통해 직접 COS(Cloud Object Storage) 버킷에 파일을 업로드하는 간단한 코드를 사용하는 방법을 설명합니다.

>! 본 문서의 내용은 XML 버전의 API를 기반으로 합니다.
>


<span id="사전 준비"></span>
## 전제 조건
1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고, 버킷을 생성하여 BucketName(버킷 이름)과 Region(리전 이름)을 구성합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참고하십시오.
2. [CAM 콘솔](https://console.cloud.tencent.com/capi)에 로그인하고 API 키 관리 페이지에서 프로젝트의 SecretId 및 SecretKey를 가져옵니다.

## 실행 순서

#### 1. WeChat 미니프로그램 얼로우리스트 구성
미니프로그램은 COS가 WeChat의 공개 플랫폼에 로그인하고 ‘개발’->’개발 설정’에서 도메인 이름 얼로우리스트를 구성해야 한다고 요청합니다. SDK는 wx.uploadFile 및 wx.request의 두 가지 API를 사용합니다.
- cos.postObject 메소드의 경우 wx.uploadFile을 사용하여 요청이 전송됩니다.
- 다른 방법의 경우 wx.request를 사용하여 요청을 보냅니다.

해당 얼로우리스트에서 COS 도메인 이름을 구성해야 합니다. 허용되는 도메인 이름에는 두 가지 형식이 있습니다.

- 버킷이 하나만 사용되는 경우 Bucket 도메인 이름을 얼로우리스트 도메인 이름으로 구성할 수 있습니다(예시: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`).
- 여러 버킷을 사용하는 경우 pathname에 bucket을 배치하여 접미사 COS 요청을 사용하도록 선택할 수 있습니다. 이 경우 `cos.ap-guangzhou.myqcloud.com`과 같이 리전 도메인 이름을 얼로우리스트로 구성해야 합니다.

#### 2. 임시 키 획득 및 서명 계산

보안을 위해 서명에 임시 키를 사용합니다. 서버에 임시 키 서비스 구축에 대한 자세한 내용은 [PHP 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) 및 [Nodejs 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js)를 참고하십시오.
다른 언어를 사용하거나 직접 구현하려면 다음 단계를 따르십시오.
(1) 서버에서 임시 키를 획득합니다. 서버는 먼저 고정 키의 SecretId와 SecretKey를 사용해 STS 서비스에서 tmpSecretId, tmpSecretKey, sessionToken과 같은 임시 키를 획득합니다. 자세한 방법은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 또는 [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk) 문서를 참고하십시오.
>!요청이 put인지 post인지에 따라 "name/cos:PutObject" 또는 "name/cos:PostObject"를 허용하도록 STS의 policy action을 추가해야 합니다.

(2) 프런트 엔드에서 tmpSecretId, tmpSecretKey, method, pathname을 통해 서명을 계산합니다. [cos-auth.js](https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js) 구문을 참고 및 사용해 서명을 계산하며, 비즈니스에 필요한 경우 백그라운드에서 서명을 계산할 수도 있습니다.
(3) 계산된 서명과 sessionToken을 넣고,
  - post 요청의 formData의 Signature 및 x-cos-security-token 필드에 업로드 요청을 COS API로 보냅니다.
  - put 요청의 headers의 Signature 및 x-cos-security-token 필드에 업로드 요청을 COS API로 보냅니다.

>! 정식 배포에 앞서 서버에 본인 웹 사이트의 권한 인증 기능을 추가하십시오.
>

#### 3. 접미사 요청

COS API의 일반적인 요청 형식은 `POST http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/`와 비슷합니다. 요청한 도메인 이름은 버킷 도메인 이름입니다. 이와 같이 미니프로그램에서 하나 이상의 버킷을 사용하는 경우 버킷 도메인 이름을 얼로우리스트 도메인 이름으로 설정해야 합니다. 솔루션은 다음과 같습니다.

COS는 접미사 요청 형식 `POST http://cos.ap-beijing.myqcloud.com/examplebucket-1250000000/`를 제공합니다. 요청된 도메인 이름은 리전 도메인 이름이며 요청한 경로에 버킷 이름이 위치합니다. 미니프로그램에서 동일한 리전에서 여러 버킷을 사용하는 경우 하나의 도메인 이름 `cos.ap-beijing.myqcloud.com`만 얼로우리스트 도메인 이름으로 구성하면 됩니다.

접미사 요청 형식은 서명할 때 사용되는 경로 앞에 버킷 이름을 붙여야 합니다(예시: `/examplebucket-1250000000/`).

#### 4. 다이렉트 업로드 예시 코드

다음 코드는 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) API(사용 권장) 및 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) API를 모두 예시한 것이며 작업 가이드는 다음과 같습니다.

```js
var CosAuth = require('./cos-auth'); // 여기에서 다운로드 주소가 https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js인 cos-auth.js를 참조함 

var Bucket = 'examplebucket-1250000000';
var Region = 'ap-shanghai';
var ForcePathStyle = false; // 서명 계산 및 도메인 이름 얼로우리스트 구성과 관련된 접미사 사용 여부

var uploadFile = function () {

    // 요청 시 사용한 매개변수
    var prefix = 'https://' + Bucket + '.cos.' + Region + '.myqcloud.com/';
    if (ForcePathStyle) {
		// 접미사 요청의 도메인 이름은 버킷 도메인 이름 대신 리전 도메인 이름을 사용하여 서명되며, 자세한 내용은 ‘3. 접미사 요청’ 참고
        prefix = 'https://cos.' + Region + '.myqcloud.com/' + Bucket + '/'; 
    }

    // 더 많은 문자열 코드의 url encode 형식
    var camSafeUrlEncode = function (str) {
        return encodeURIComponent(str)
            .replace(/!/g, '%21')
            .replace(/'/g, '%27')
            .replace(/\(/g, '%28')
            .replace(/\)/g, '%29')
            .replace(/\*/g, '%2A');
    };

    // 임시 키 획득
    var stsCache;
    var getCredentials = function (callback) {
        if (stsCache && Date.now() / 1000 + 30 < stsCache.expiredTime) {
            callback(data.credentials);
            return;
        }
        wx.request({
            method: 'GET',
            url: 'https://example.com/sts.php', // 서버측 서명, 자세한 내용은 위의 임시 키 가져오기 참고
            dataType: 'json',
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                if (credentials) {
                    stsCache = data
                } else {
                    wx.showModal({title: ‘임시 키 가져오기 실패’, content: JSON.stringify(data), showCancel: false});
                }
                callback(stsCache && stsCache.credentials);
            },
            error: function (err) {
                wx.showModal({title: ‘임시 키 가져오기 실패’, content: JSON.stringify(err), showCancel: false});
            }
        });
    };

    // 서명 계산
    var getAuthorization = function (options, callback) {
        getCredentials(function (credentials) {
            callback({
                XCosSecurityToken: credentials.sessionToken,
                Authorization: CosAuth({
                    SecretId: credentials.tmpSecretId,
                    SecretKey: credentials.tmpSecretKey,
                    Method: options.Method,
                    Pathname: options.Pathname,
                })
            });
        });
    };

    // post 파일 업로드
    var postFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // 여기에 업로드할 파일의 이름 지정
        var signPathname = '/'; // PostObject API의 경우 Key가 전송을 위해 Body에 배치되므로 요청 경로와 서명 경로는 /
        if (ForcePathStyle) {
			  // 접미사 요청의 서명에 사용된 경로에는 버킷의 이름이 포함되어야 하며, 자세한 내용은 ‘3. 접미사 요청’ 참고
            signPathname = '/' + Bucket + '/';  
        }
        getAuthorization({Method: 'POST', Pathname: signPathname}, function (AuthData) {
            var requestTask = wx.uploadFile({
                url: prefix,
                name: 'file',
                filePath: filePath,
                formData: {
                    'key': Key,
                    'success_action_status': 200,
                    'Signature': AuthData.Authorization,
                    'x-cos-security-token': AuthData.XCosSecurityToken,
                    'Content-Type': '',
                },
                success: function (res) {
                    var url = prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/');
                    console.log(res.statusCode);
                    console.log(url);
                    if (/^2\d\d$/.test('' + res.statusCode)) {
                        wx.showModal({title: ‘업로드 성공’, content: url, showCancel: false});
                    } else {
                        wx.showModal({title: ‘업로드 실패’, content: JSON.stringify(res), showCancel: false});
                    }
                },
                fail: function (res) {
                    wx.showModal({title: ‘업로드 실패’, content: JSON.stringify(res), showCancel: false});
                }
            });
            requestTask.onProgressUpdate(function (res) {
                console.log(‘진행률:’, res);
            });
        });
    };

    // put 파일 업로드
    var putFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // 여기에 업로드할 파일의 이름 지정
        var signPathname = '/' + Key; // PutObject API Key는 url 전송에 위치하므로 요청 경로와 서명 경로는 /Key
        if (ForcePathStyle) {
			  // 접미사 요청의 서명에 사용된 경로에는 버킷의 이름이 포함되어야 하며, 자세한 내용은 ‘3. 접미사 요청’ 참고
            signPathname = '/' + Bucket + '/' + Key;  
        }
        getAuthorization({Method: 'PUT', Pathname: signPathname}, function (AuthData) {
          // put 요청은 임시 파일 경로에서 파일 콘텐츠를 읽어야 함
          var wxfs = wx.getFileSystemManager();
          wxfs.readFile({
            filePath: filePath,
            success: function (fileRes) {
              var requestTask = wx.request({
                url: prefix + signPathname.substr(signPathname.lastIndexOf('/') + 1),
                method: 'PUT',
                header: {
                  'Authorization': AuthData.Authorization,
                  'x-cos-security-token': AuthData.XCosSecurityToken,
                },
                data: fileRes.data,
                success: function success(res) {
                  var url = prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/');
                  if (res.statusCode === 200) {
                      wx.showModal({title: ‘업로드 성공’, content: url, showCancel: false});
                  } else {
                      wx.showModal({title: ‘업로드 실패’, content: JSON.stringify(res), showCancel: false});
                  }
                  console.log(res.statusCode);
                  console.log(url);
                },
                fail: function fail(res) {
                  wx.showModal({title: ‘업로드 실패’, content: JSON.stringify(res), showCancel: false});
                },
              });
              requestTask.onProgressUpdate(function (res) {
                  console.log('진행 중:', res);
              });
            },
          });
        });
    };

    // 파일 선택
    wx.chooseImage({
        count: 1, // 기본값: 9
        sizeType: ['original'], // 원본 이미지 또는 압축 이미지를 지정할 수 있습니다. 여기에서 기본값은 원본 이미지입니다.
        sourceType: ['album', 'camera'], // 출처를 갤러리 또는 카메라로 지정할 수 있습니다. 기본값은 둘 다입니다.
        success: function (res) {
            putFile(res.tempFiles[0].path); // put 요청 업로드, 사용 권장
            // postFile(res.tempFiles[0].path); // post 요청 업로드
        }
    })
};
```

## 관련 문서

미니프로그램 SDK를 사용해야 하는 경우 미니프로그램 SDK [시작하기](https://intl.cloud.tencent.com/document/product/436/30609) 문서를 참고하십시오.

