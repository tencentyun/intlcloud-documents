## 소개
본 문서에서는 SDK에 종속되지 않고 간단한 코드를 사용하여 웹 페이지(Web)에서 직접 파일을 COS의 버킷에 전송하는 방법을 소개합니다.

> 본 문서의 내용은 XML 버전의 API를 기반으로 합니다.


## 전제 조건
<span id="사전 준비"></span>
1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 버킷을 생성하여 Bucket(버킷 이름)과 Region(리전 이름)을 획득합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참조하십시오.
2. 버킷 상세 페이지로 이동하여 [기본 정보] 탭을 클릭합니다. 페이지를 아래로 내려 [크로스 도메인 액세스 CORS 설정]의 설정 페이지를 찾아 [규칙 추가]를 클릭한 후, 다음 이미지와 같이 설정합니다. 자세한 내용은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318) 문서를 참조하십시오.
![cors](https://main.qcloudimg.com/raw/eb73177a2302ad976be301254bcd9630.png)
3. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.



## 실행 순서


>! 정식 배포에 앞서 서버에 본인 웹 사이트의 권한 인증 기능을 추가하십시오.

### 임시 키 획득 및 서명 계산
보안을 위해 서명에 임시 키를 사용합니다. 서버에 임시 키 서비스 구축에 대한 자세한 내용은 [PHP 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php) 및 [Nodejs 예시](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js)를 참조하십시오.
다른 언어가 있거나 직접 구현할 경우, 다음 방법을 확인하십시오.
1. 서버에서 임시 키를 획득합니다. 서버는 먼저 고정 키의 SecretId와 SecretKey를 사용해 STS 서비스에서 tmpSecretId, tmpSecretKey, sessionToken과 같은 임시 키를 획득합니다. 자세한 방법은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 또는 [cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk) 문서를 참조하십시오.
2. 프런트 엔드에서 tmpSecretId, tmpSecretKey, method, pathname을 통해 서명을 계산합니다. [cos-auth.js](https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js) 구문을 참고 및 사용해 서명을 계산하며, 비즈니스에 필요한 경우 백그라운드에서 서명을 계산할 수도 있습니다.
3. PutObject 인터페이스를 사용해 파일을 업로드하는 경우, 요청 전송 시 계산된 서명과 sessionToken을 각각 header의 authorization과 x-cos-security-token 필드에 넣습니다.
PostObject 인터페이스를 사용해 파일을 업로드하는 경우, 요청 전송 시 계산된 서명과 sessionToken을 각각 폼(form)의 Signature와 x-cos-security-token 필드에 넣습니다.


### 프런트 엔드 업로드
#### 방법 A: AJAX를 사용하여 업로드
AJAX 업로드 시에는 브라우저에서 기본적으로 HTML5 특성을 지원해야 합니다. 해당 방법은 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)를 사용하며, 작업 방법은 다음과 같습니다.
1. [전제 조건](#사전 준비)의 순서에 따라 버킷 관련 설정을 준비합니다.
2. `test.html` 파일을 생성하고, 아래 코드에서 Bucket과 Region 정보를 수정하여 `test.html` 파일에 복사합니다.
3. 백그라운드의 서명 서비스를 배포하고, `test.html`의 서명 서비스 주소를 수정합니다.
4. `test.html`을 Web 서버에 올리고, 브라우저로 페이지에 접속해 파일 업로드 기능을 테스트합니다.

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
        // 요청 시 사용한 매개변수
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';

        // 더 많은 문자열 코드의 url encode 형식
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // 서명 계산
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
            var Key = 'dir/' + file.name; // 여기에서 업로드 디렉터리 및 파일 이름 지정
            getAuthorization({Method: 'PUT', Pathname: '/' + Key}, function (err, info) {

                if (err) {
                    alert(err);
                    return;
                }

                var auth = info.Authorization;
                var XCosSecurityToken = info.XCosSecurityToken;
                var url = prefix + camSafeUrlEncode(Key).replace(/%2F/g, '/');
                var xhr = new XMLHttpRequest();
                xhr.open('PUT', url, true);
                xhr.setRequestHeader('Authorization', auth);
                XCosSecurityToken && xhr.setRequestHeader('x-cos-security-token', XCosSecurityToken);
                xhr.upload.onprogress = function (e) {
                    console.log('업로드 진행률' + (Math.round(e.loaded / e.total * 10000) / 100) + '%');
                };
                xhr.onload = function () {
                    if (/^2\d\d$/.test('' + xhr.status)) {
                        var ETag = xhr.getResponseHeader('etag');
                        callback(null, {url: url, ETag: ETag});
                    } else {
                        callback(Key + ' 파일 업로드에 실패했습니다. 상태 코드: ' + xhr.status);
                    }
                };
                xhr.onerror = function () {
                    callback(Key + ' 파일 업로드에 실패했습니다. CORS 크로스 도메인 규칙을 설정했는지 확인하십시오.');
                };
                xhr.send(file);
            });
        };

        // 폼 제출 수신
        document.getElementById('submitBtn').onclick = function (e) {
            var file = document.getElementById('fileSelector').files[0];
            if (!file) {
                document.getElementById('msg').innerText = '업로드할 파일을 선택하지 않았습니다.';
                return;
            }
            file && uploadFile(file, function (err, data) {
                console.log(err || data);
                document.getElementById('msg').innerText = err ? err : ('업로드 성공, ETag=' + data.ETag);
            });
        };
    })();
</script>

</body>
</html>
```

실행 결과는 다음 이미지와 같습니다.
![Ajax 업로드](https://main.qcloudimg.com/raw/970bc04c0a1e0b3c5be077f360000424.png)

#### 방법 B: 폼(Form)을 사용하여 업로드
낮은 버전의 브라우저(예: IE8)에서도 Form 업로드를 실행할 수 있습니다. 본 솔루션은 [Post Object](https://cloud.tencent.com/document/product/436/14690) 인터페이스를 사용합니다. 다음은 작업 가이드입니다.
1. [전제 조건](#사전 준비)의 순서에 따라 버킷을 준비합니다.
2. `test.html` 파일을 생성하고, 아래 코드에서 Bucket과 Region 정보를 수정하여 `test.html` 파일에 복사합니다.
3. 백그라운드의 서명 서비스를 배포하고, `test.html`의 서명 서비스 주소를 수정합니다.
4. `test.html`과 동일한 디렉터리에 비어 있는 `empty.html`을 생성하여 업로드 성공 시 리디렉션하는 데 사용합니다.
5. `test.html`과 `empty.html`을 Web 서버에 올리고, 브라우저로 페이지에 접속해 파일 업로드 기능을 테스트합니다.

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>폼(Form) 간편 업로드</title>
    <style>h1, h2 {font-weight: normal;}#msg {margin-top:10px;}</style>
</head>
<body>

<h1>폼(Form) 간편 업로드(IE8 호환)</h1>
<div>최저 버전은 IE6까지 호환해 업로드하며, onprogress는 미지원</div>

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

        // 요청 시 사용한 매개변수
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';
        var form = document.getElementById('form');
        form.action = prefix;

        // 더 많은 문자열 코드의 url encode 형식
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // 서명 계산
        var getAuthorization = function (options, callback) {
            // var url = 'http://127.0.0.1:3000/sts' +
            var url = '../server/sts.php';
            var xhr = new XMLHttpRequest();
            xhr.open('GET', url, true);
            xhr.onreadystatechange = function (e) {
                if (xhr.readyState === 4) {
                    if (/^2\d\d$/.test('' + xhr.status)) {
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

        // 업로드 완료 수신
        var Key;
        var submitTarget = document.getElementById('submitTarget');
        var showMessage = function (err, data) {
            console.log(err || data);
            document.getElementById('msg').innerText = err ? err : ('업로드 성공, ETag=' + data.ETag);
        };
        submitTarget.onload = function () {
            var search;
            try {
                search = submitTarget.contentWindow.location.search.substr(1);
            } catch (e) {
                showMessage(Key + ' 파일 업로드에 실패했습니다.');
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

        // 업로드 시작
        document.getElementById('submitBtn').onclick = function (e) {
            var filePath = document.getElementById('fileSelector').value;
            if (!filePath) {
                document.getElementById('msg').innerText = '업로드할 파일을 선택하지 않았습니다.';
                return;
            }
            Key = 'dir/' + filePath.match(/[\\\/]?([^\\\/]+)$/)[1]; // 여기에서 업로드 디렉터리 및 파일 이름 지정
            getAuthorization({Method: 'POST', Pathname: '/'}, function (err, AuthData) {
                // 현재 디렉터리에 빈 empty.html를 넣어 인터페이스에서 업로드 완료 시 리디렉션 페이지로 사용
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
실행 결과는 다음 이미지와 같습니다.
![폼(Form) 업로드](https://main.qcloudimg.com/raw/90a3460c58ed7e056f08624ce329c1a4.png)
## 관련 문서
더 다양한 인터페이스 호출이 필요한 경우 다음 JavaScript SDK 문서를 참조하십시오.
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/11459)

  
