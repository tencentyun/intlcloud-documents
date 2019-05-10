## 소개
본 문서에서는 SDK에 의존하지 않고 간단한 코드로 웹페이지(Web)에서 파일을 COS의 버킷에 직접적으로 업로드할 수 있는 방법을 소개해 드립니다.

>! 본 문서의 내용은 XML 버전의 API를 기반으로 합니다.

## 절차
<span id="사전 준비"></span>
### 1. 사전 준비
1) [COS 콘솔](https://console.cloud.tencent.com/cos4)에 로그인하고 버킷을 생성하여 Bucket(버킷 이름)과 Region(지역 이름)을 얻습니다.
2) [키 관리 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인하여 프로젝트의 SecretId와 SecretKey를 획득합니다.
3) COS 콘솔에서 새로 생성한 버킷에 액세스하고 [기본 구성]을 클릭하여 CORS 규칙을 구성합니다. 구성 예시는 다음 그림과 같습니다.
![cors](//mc.qcloudimg.com/static/img/2e7791e9274ce3ebf8b25bbeafcd7b45/image.png)

### 2. 임시 키 서비스 구축
보안성을 위해 서명할 때 임시 키를 사용할 경우 서버 측에서 임시 키 서비스를 구축해야 합니다. [PHP 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php)와 [Nodejs 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js)를 참조하십시오.
기타 언어는 [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk) 또는 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

>! 공식적으로 배포할 때 서버에 사용자의 웹사이트 자체의 권한 인증을 한 단계 더 추가하십시오.

### 3. 서명 컴퓨팅
보안성을 위해 서명할 때 임시 키를 사용할 경우 서버 측에서 임시 키 서비스를 구축해야 합니다. [PHP 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php)와 [Nodejs 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js)를 참조하십시오.
기타 언어나 자체 보유한 API로 구현할 경우 아래 절차를 참조하십시오.
1) 프런트 엔드는 서명해야 하고 서버로부터 임시 키를 받아 method와 pathname의 필요한 매개변수를 가져옵니다.
2) 서버 엔드에서는 우선 고정 키 SecretId, SecretKey를 사용하여 STS 서버로부터 임시 키 tmpSecretId, tmpSecretKey, sessionToken를 획득합니다. 자세한 사항은 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048) 또는 [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk) 문서를 참조하십시오.
3) 프런트 엔드는 tmpSecretId, tmpSecretKey 및 method, pathname으로 서명을 컴퓨팅합니다. 아래 예시에는 프런트 엔드의 서명 컴퓨팅 절차를 포함하였습니다. 필요하면 백 엔드에 서명을 컴퓨팅할 수도 있습니다.
4) 서버는 컴퓨팅으로 얻은 서명 authorization과 sessionToken을 프런트 엔드에 반환합니다. 프런트 엔드는 서버로부터 반환된 두 개 값을 각각 header의 Authorization과 x-cos-security-token 필드에 넣어 COS API에 업로드 요청을 보냅니다.

>! 공식적으로 배포할 때 서버에 사용자의 웹사이트 자체의 권한 인증을 한 단계 더 추가하십시오.

### 4. 프런트 엔드에 업로드
#### 솔루션 A: AJAX로 업로드
AJAX로 업로드하려면 브라우저가 기본적인 HTML5 특성을 지원해야 하며 현재 솔루션으로는 [PUT Object](https://cloud.tencent.com/document/product/436/7749) 문서를 사용하며 작업 가이드는 다음과 같습니다.
1) [절차 1. 사전 준비](#사전 준비)의 절차에 따라 버킷의 관련 구성을 준비합니다.
2) `test.html` 파일을 생성하고 아래 코드의 Bucket 과 Region을 수정하며 `test.html` 파일에 복사합니다.
3) 백 엔드의 서명 서비스를 배포하고 `test.html`의 서명 서비스 주소를 수정합니다.
4) `test.html`을 Web 서버에 넣고 브라우저를 통해 페이지에 접근하여 파일 업로드 기능을 테스트합니다.

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Ajax Put 업로드</title>
    <style>
        h1, h2 {
            font-weight: normal;
        }

        #msg {
            margin-top: 10px;
        }
    </style>
</head>
<body>

<h1>Ajax Put 업로드</h1>

<input id="fileSelector" type="file">
<input id="submitBtn" type="submit">

<div id="msg"></div>

<script src="https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js"></script>
<script>
    (function () {
        // 요청에 사용되는 매개변수
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';

        // 더 많은 문자 인코딩에 대한 url encode 포맷
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // 서명 컴퓨팅
        var getAuthorization = function (options, callback) {
            // var url = 'http://127.0.0.1:3000/sts-auth' +
            var url = '../server/sts.php';
            var xhr = new XMLHttpRequest();
            xhr.open('GET', url, true);
            xhr.onload = function (e) {
                var credentials;
                try {
                    credentials = (new Function('return ' + xhr.responseText))().credentials;
                } catch (e) {}
                if (credentials) {
                    callback(null, {
                        XCosSecurityToken: credentials.sessionToken,
                        Authorization: CosAuth({
                            SecretId: credentials.tmpSecretId,
                            SecretKey: credentials.tmpSecretKey,
                            Method: options.Method,
                            Pathname: options.Pathname,
                        })
                    });
                } else {
                    console.error(xhr.responseText);
                    callback('서명 획득 오류');
                }
            };
            xhr.onerror = function (e) {
                callback('서명 획득 오류');
            };
            xhr.send();
        };

        // 파일 업로드
        var uploadFile = function (file, callback) {
            var Key = 'dir/' + file.name; // 여기서 업로드 디렉터리와 파일 이름을 지정합니다
            getAuthorization({Method: 'PUT', Pathname: '/' + Key}, function (err, info) {

                if (err) {
                    alert(err);
                    return;
                }

                var auth = info.Authorization;
                var XCosSecurityToken = info.XCosSecurityToken;
                var url = prefix + camSafeUrlEncode(Key).replace(/%2F/, '/');
                var xhr = new XMLHttpRequest();
                xhr.open('PUT', url, true);
                xhr.setRequestHeader('Authorization', auth);
                XCosSecurityToken && xhr.setRequestHeader('x-cos-security-token', XCosSecurityToken);
                xhr.upload.onprogress = function (e) {
                    console.log('업로드 진행률 ' + (Math.round(e.loaded / e.total * 10000) / 100) + '%');
                };
                xhr.onload = function () {
                    if (xhr.status === 200 || xhr.status === 206) {
                        var ETag = xhr.getResponseHeader('etag');
                        callback(null, {url: url, ETag: ETag});
                    } else {
                        callback('파일 ' + Key + ' 업로드 실패, 상태 코드：' + xhr.status);
                    }
                };
                xhr.onerror = function () {
                    callback('파일 ' + Key + ' 업로드 실패, CORS 영역 간 규칙이 구성되는지를 검사하십시오');
                };
                xhr.send(file);
            });
        };

        // 양식 제출 모니터링
        document.getElementById('submitBtn').onclick = function (e) {
            var file = document.getElementById('fileSelector').files[0];
            if (!file) {
                document.getElementById('msg').innerText = '업로드 파일을 선택하지 않았습니다';
                return;
            }
            file && uploadFile(file, function (err, data) {
                console.log(err || data);
                document.getElementById('msg').innerText = err ? err : ('업로드 성공,ETag=' + data.ETag);
            });
        };
    })();
</script>

</body>
</html>
```

실행 효과는 다음 그림과 같습니다.
![Ajax로 업로드](https://main.qcloudimg.com/raw/4bfc2883d71deddccc76b250ebb6a051.png)

#### 솔루션 B: 양식으로 업로드
양식으로 업로드는 낮은 버전의 브라우저를 통한 업로드(예: IE8)를 지원하며 현재 솔루션은 [XML API 의 PostObject API](/doc/product/436/7751)를 사용합니다. 작업 가이드:
1) [1. 사전 준비](#사전 준비)의 절차에 따라 버킷을 준비합니다.
2) `test.html` 파일을 생성하고 아래 코드의 Bucket 과 Region을 수정하며 `test.html` 파일에 복사합니다.
3) 백 엔드의 서명 서비스를 배포하고 `test.html`의 서명 서비스 주소를 수정합니다.
4) `test.html`과 동일한 디렉터리 하에 하나의 빈 `empty.html`을 생성하여 업로드 성공 시 리디렉션합니다.
5) `test.html`와 `empty.html`을 Web 서버에 두고 브라우저를 통해 페이지에 접근하여 파일 업로드 기능을 테스트합니다.

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Form 양식의 간편 업로드</title>
    <style>h1, h2 {font-weight: normal;}#msg {margin-top:10px;}</style>
</head>
<body>

<h1>Form 양식의 간편 업로드(IE8과 호환)</h1>
<div>최저 IE6 업로드와 호환하며, 지원하지 않음 onprogress</div>

<form id="form" target="submitTarget" action="" method="post" enctype="multipart/form-data" accept="*/*">
    <input id="name" name="name" type="hidden" value="">
    <input name="success_action_status" type="hidden" value="200">
    <input id="success_action_redirect" name="success_action_redirect" type="hidden" value="">
    <input id="key" name="key" type="hidden" value="">
    <input id="Signature" name="Signature" type="hidden" value="">
    <input name="Content-Type" type="hidden" value="">
    <input id="x-cos-security-token" name="x-cos-security-token" type="hidden" value="">
    <input id="fileSelector" name="file" type="file">
    <input id="submitBtn" type="button" value="제출">
</form>
<iframe id="submitTarget" name="submitTarget" style="display:none;" frameborder="0"></iframe>

<div id="msg"></div>

<script src="https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js"></script>
<script>
    (function () {

        // 요청에 사용되는 매개변수
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';
        var form = document.getElementById('form');
        form.action = prefix;

        // 더 많은 문자 인코딩에 대한 url encode 포맷
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // 서명 컴퓨팅
        var getAuthorization = function (options, callback) {
            // var url = 'http://127.0.0.1:3000/sts' +
            var url = '../server/sts.php';
            var xhr = new XMLHttpRequest();
            xhr.open('GET', url, true);
            xhr.onreadystatechange = function (e) {
                if (xhr.readyState === 4) {
                    if (xhr.status === 200) {
                        var credentials;
                        try {
                            credentials = (new Function('return ' + xhr.responseText))().credentials;
                        } catch (e) {}
                        if (credentials) {
                            callback(null, {
                                XCosSecurityToken: credentials.sessionToken,
                                Authorization: CosAuth({
                                    SecretId: credentials.tmpSecretId,
                                    SecretKey: credentials.tmpSecretKey,
                                    Method: options.Method,
                                    Pathname: options.Pathname,
                                })
                            });
                        } else {
                            console.error(xhr.responseText);
                            callback('서명 획득 오류');
                        }
                    } else {
                        callback('서명 획득 오류');
                    }
                }
            };
            xhr.send();
        };

        //모니터링 업로드 완료
        var Key;
        var submitTarget = document.getElementById('submitTarget');
        var showMessage = function (err, data) {
            console.log(err || data);
            document.getElementById('msg').innerText = err ? err : ('업로드 성공，ETag=' + data.ETag);
        };
        submitTarget.onload = function () {
            var search;
            try {
                search = submitTarget.contentWindow.location.search.substr(1);
            } catch (e) {
                showMessage('파일 ' + Key + ' 업로드 실패');
            }
            if (search) {
                var items = search.split('&');
                var i, arr, data = {};
                for (i = 0; i < items.length; i++) {
                    arr = items[i].split('=');
                    data[arr[0]] = decodeURIComponent(arr[1] || '');
                }
                showMessage(null, {url: prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/'), ETag: data.etag});
            } else {
            }
        };

        //업로드 시작
        document.getElementById('submitBtn').onclick = function (e) {
            var filePath = document.getElementById('fileSelector').value;
            if (!filePath) {
                document.getElementById('msg').innerText = '업로드 파일을 선택하지 않았습니다';
                return;
            }
            Key = 'dir/' + filePath.match(/[\\\/]?([^\\\/]+)$/)[1]; // 여기서 업로드 디렉터리와 파일 이름을 지정합니다
            getAuthorization({Method: 'POST', Pathname: '/'}, function (err, AuthData) {
                // 현재 디렉터리에 빈 empty.html을 놓아두어 API가 업로드 완료 후 리디렉션하는 데 도움이 됩니다.
                document.getElementById('success_action_redirect').value = location.href.substr(0, location.href.lastIndexOf('/') + 1) + 'empty.html';
                document.getElementById('key').value = Key;
                document.getElementById('Signature').value = AuthData.Authorization;
                document.getElementById('x-cos-security-token').value = AuthData.XCosSecurityToken || '';
                form.submit();
            });
        };
    })();
</script>

</body>
</html>
```
실행 효과는 다음 그림과 같습니다.
![양식으로 업로드](https://main.qcloudimg.com/raw/ef666461bc5f88715f28934393ebe4f4.png)
## 관련 문서
더 다양한 API 호출 수요가 있을 경우, 아래 JavaScript SDK 문서를 참조하십시오.
- [JavaScript SDK](https://cloud.tencent.com/document/product/436/11459)
- [JavaScript SDK(이전 버전 API)](https://cloud.tencent.com/document/product/436/8095)
