## 概要
本ドキュメントでは、SDKに頼らずに簡単なコードを使用して、Webページ（Webサイト）でファイルをCOSのバケットに直接転送する方法を紹介します。

>！ 本ドキュメントの内容は、XMLバージョンのAPIに基づいたものです。

## 作業手順
<span id="事前準備"></span>
### 1. 事前準備
1）[COSコンソール](https://console.cloud.tencent.com/cos4)にログインした後、バケットを作成し、Bucket（バケット名）とRegion（地域名）を取得します。
2）[暗号鍵管理コンソール](https://console.cloud.tencent.com/cam/capi)にログインして、プロジェクトのSecretIdとSecretKeyを取得します。
3）COSコンソールで、新規作成のバケットにアクセスし、「基本構成」をクリックしてCORS規則を構成します。構成例は下記のとおりです。
![cors](//mc.qcloudimg.com/static/img/2e7791e9274ce3ebf8b25bbeafcd7b45/image.png)

### 2. 一時暗号鍵サービスの構築
安全上の理由から、署名には一時暗号鍵が使用され、サーバーで一時暗号鍵サービスを構築する必要があります。[PHPの例](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php)、[Nodejsの例](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js)を参照してください。
その他の言語は、[cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk)または[一時暗号鍵の生成および使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

>! 正式に配備する際に、サーバーにはサイト自身の権限検査を追加してください。

### 3. 署名の計算
安全上の理由から、署名には一時暗号鍵が使用され、サーバーで一時暗号鍵サービスを構築する必要があります。[PHPの例](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php)、[Nodejsの例](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js)を参照してください。
その他の言語や独自の実行については、下記のプロセスを参照してください。
1）フロントエンドには署名が必要です。サーバーから一時暗号鍵を取得し、methodとpathnameの必要なパラメータを渡します。
2）サーバーでは、まず固定暗号鍵SecretId、SecretKeyを使用して、STSサービスから一時暗号鍵を取得し、一時暗号鍵tmpSecretId、tmpSecretKey、sessionTokenを取得します。詳細については、[一時暗号鍵の生成および使用ガイド](https://cloud.tencent.com/document/product/436/14048)または[cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk)ドキュメントを参照してください。
3）フロントエンドでは、tmpSecretId、tmpSecretKeyおよびmethod、pathnameで署名を計算します。下記の例では、フロントエンドで署名を計算する作業手順を示します。ビジネスニーズに応じて、バックエンドで署名を計算することもできます。
4）サーバーは計算された署名authorizationとsessionTokenをフロントエンドに戻し、フロントエンドはサーバーから戻された二つの値をheaderのAuthorizationとx-cos-security-tokenフィールドに配置して、COS APIにアップロードリクエストを発します。

>! 正式に配備する際に、サーバーにはサイト自身の権限検査を追加してください。

### 4. フロントエンドのアップロード
#### プランA：AJAXによるアップロード
AJAXを通してアップロードするには、ブラウザが基本的なHTML5プロパティをサポートしている必要があります。現在のプランでは、[PUT Object ](https://cloud.tencent.com/document/product/436/7749) ドキュメントを使用します。操作手順は下記のとおりです。
1）[手順1. 事前準備](#事前準備)に従って、バケットに関連する構成を準備します。
2）`test.html`ファイルを作成し、下のコードのBucketとRegionを変更して、`test.html`ファイルにコピーします。
3）バックエンドの署名サービスを配備し、`test.html`の署名サービスアドレスを変更します。
4）`test.html`をWebサーバーの下に置き、ブラウザでページにアクセスすることで、ファイルのアップロード機能をテストします。

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Ajax Put アップロード</title>
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

<h1>Ajax Put アップロード</h1>

<input id="fileSelector" type="file">
<input id="submitBtn" type="submit">

<div id="msg"></div>

<script src="https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js"></script>
<script>
    (function () {
        // リクエストに使用するパラメータ
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';

        // より多くの文字にエンコーディングするurl encodeフォーマット
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // 署名の計算
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
                    callback('署名の取得エラー');
                }
            };
            xhr.onerror = function (e) {
                callback('署名の取得エラー');
            };
            xhr.send();
        };

        // ファイルのアップロード
        var uploadFile = function (file, callback) {
            var Key = 'dir/' + file.name; // ここでアップロードディレクトリとファイル名を指定します。
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
                    console.log('アップロードの進捗 ' + (Math.round(e.loaded / e.total * 10000) / 100) + '%');
                };
                xhr.onload = function () {
                    if (xhr.status === 200 || xhr.status === 206) {
                        var ETag = xhr.getResponseHeader('etag');
                        callback(null, {url: url, ETag: ETag});
                    } else {
                        callback('ファイル ' + Key + ' のアップロードに失敗、ステータスコード：' + xhr.status);
                    }
                };
                xhr.onerror = function () {
                    callback('ファイル ' + Key + ' のアップロードに失敗、CORS規則が構成されていないか確認してください');
                };
                xhr.send(file);
            });
        };

        // レポート提出のリスニング
        document.getElementById('submitBtn').onclick = function (e) {
            var file = document.getElementById('fileSelector').files[0];
            if (!file) {
                document.getElementById('msg').innerText = 'アップロードファイルが未選択';
                return;
            }
            file && uploadFile(file, function (err, data) {
                console.log(err || data);
                document.getElementById('msg').innerText = err ? err : ('アップロードに成功、ETag=' + data.ETag);
            });
        };
    })();
</script>

</body>
</html>
```

実行効果は下記の通りです。
![Ajaxアップロード](https://main.qcloudimg.com/raw/4bfc2883d71deddccc76b250ebb6a051.png)

#### プランB：Formフォームによるアップロード
Formフォームでアップロードする場合、IE8など古いバージョンのブラウザのアップロードがサポートされており、現在のプランでは[XML APIのPostObject API](/doc/product/436/7751)が使用されています。操作ガイドは下記のとおりです。
1）[手順1. 事前準備](#事前準備)に従って、バケットを用意します。
2）`test.html`ファイルを作成し、下のコードのBucketとRegionを変更して、`test.html`ファイルにコピーします。
3）バックエンドの署名サービスを配備し、`test.html`の署名サービスアドレスを変更します。
4）`test.html`と同じディレクトリに空の`empty.html`を作成します。それによってアップロードが成功した後ジャンプバックすることができます。
5）`test.html`と`empty.html`をWebサーバーの下に置き、ブラウザでページにアクセスすることで、ファイルのアップロード機能をテストします。

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Form フォームの簡単なアップロード</title>
    <style>h1, h2 {font-weight: normal;}#msg {margin-top:10px;}</style>
</head>
<body>

<h1>Formフォームの簡単なアップロード（IE8互換可能）</h1>
<div>最低限にIE6のアップロードが互換可能、サポートされていない onprogress</div>

<form id="form" target="submitTarget" action="" method="post" enctype="multipart/form-data" accept="*/*">
    <input id="name" name="name" type="hidden" value="">
    <input name="success_action_status" type="hidden" value="200">
    <input id="success_action_redirect" name="success_action_redirect" type="hidden" value="">
    <input id="key" name="key" type="hidden" value="">
    <input id="Signature" name="Signature" type="hidden" value="">
    <input name="Content-Type" type="hidden" value="">
    <input id="x-cos-security-token" name="x-cos-security-token" type="hidden" value="">
    <input id="fileSelector" name="file" type="file">
    <input id="submitBtn" type="button" value="送信">
</form>
<iframe id="submitTarget" name="submitTarget" style="display:none;" frameborder="0"></iframe>

<div id="msg"></div>

<script src="https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js"></script>
<script>
    (function () {

        // リクエストに使用するパラメータ
        var Bucket = 'test-1250000000';
        var Region = 'ap-guangzhou';
        var protocol = location.protocol === 'https:' ? 'https:' : 'http:';
        var prefix = protocol + '//' + Bucket + '.cos.' + Region + '.myqcloud.com/';
        var form = document.getElementById('form');
        form.action = prefix;

        // より多くの文字にエンコーディングするurl encodeフォーマット
        var camSafeUrlEncode = function (str) {
            return encodeURIComponent(str)
                .replace(/!/g, '%21')
                .replace(/'/g, '%27')
                .replace(/\(/g, '%28')
                .replace(/\)/g, '%29')
                .replace(/\*/g, '%2A');
        };

        // 署名の計算
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
                            callback('署名の取得エラー');
                        }
                    } else {
                        callback('署名の取得エラー');
                    }
                }
            };
            xhr.send();
        };

        // アップロード完了のリスニング
        var Key;
        var submitTarget = document.getElementById('submitTarget');
        var showMessage = function (err, data) {
            console.log(err || data);
            document.getElementById('msg').innerText = err ? err : ('アップロードに成功，ETag=' + data.ETag);
        };
        submitTarget.onload = function () {
            var search;
            try {
                search = submitTarget.contentWindow.location.search.substr(1);
            } catch (e) {
                showMessage('ファイル ' + Key + ' のアップロードに失敗');
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

        // アップロードを開始
        document.getElementById('submitBtn').onclick = function (e) {
            var filePath = document.getElementById('fileSelector').value;
            if (!filePath) {
                document.getElementById('msg').innerText = 'アップロードファイルが未選択';
                return;
            }
            Key = 'dir/' + filePath.match(/[\\\/]?([^\\\/]+)$/)[1]; // ここでアップロードディレクトリとファイル名を指定します。
            getAuthorization({Method: 'POST', Pathname: '/'}, function (err, AuthData) {
                // APIのアップロードが完了した後ジャンプバックできるように、現在のディレクトリに空のempty.htmlを配置します。
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
実行効果は下記の通りです。
![Formフォームのアップロード](https://main.qcloudimg.com/raw/ef666461bc5f88715f28934393ebe4f4.png)
## 関連ドキュメント
API呼び出しの必要性が高まっている場合は、次のJavaScript SDKドキュメントを参照してください。
- [JavaScript SDK](https://cloud.tencent.com/document/product/436/11459)
- [JavaScript SDK（履歴バージョンAPI）](https://cloud.tencent.com/document/product/436/8095)
