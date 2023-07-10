## 概要
このドキュメントでは、SDKに依存せず、シンプルなコードを使用して、ミニプログラムでファイルをCloud Object Storage（COS）のバケットに直接転送する方法についてご説明します。

>! このドキュメントの内容はXMLバージョンのAPIをベースにしています。
>


<span id="事前準備"></span>
## 事前条件
1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、バケットを作成し、BucketName（バケット名）およびRegion（リージョン名）を設定します。詳細については[バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)のドキュメントをご参照ください。
2. [CAMコンソール](https://console.cloud.tencent.com/cam/capi)にログインし、APIキー管理ページに進み、プロジェクトのSecretIdとSecretKeyを取得します。

## 実践手順

#### 1. ミニプログラムドメイン名ホワイトリストを設定する
ミニプログラムでCOSをリクエストするには、WeChatパブリックプラットフォームにログインし、「開発」->「開発設定」でドメイン名ホワイトリストを設定する必要があります。SDKはwx.uploadFileとwx.requestという2つのインターフェースを使用します。
- cos.postObjectはwx.uploadFileを使用してリクエストを送信します。
- その他のメソッドはwx.requestを使用してリクエストを送信します。

どちらも対応するホワイトリストにあり、COSドメイン名を設定している必要があります。ホワイトリストに設定するドメイン名の形式には次の2種類があります。

- 1つのバケットのみに使用する場合は、Bucketドメイン名をホワイトリストのドメイン名に設定することができます（例：`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`）。
- 複数のバケットに使用する場合は、後置記法のCOSリクエストを選択し、bucketをpathnameに入れてリクエストすることを選択できます。この方式ではリージョンドメイン名をホワイトリストに設定する必要があります（例：`cos.ap-guangzhou.myqcloud.com`）。具体的には下記のコード内のコメントをご参照ください。

#### 2. 一時キーを取得して署名を計算する

セキュリティ上の観点から、署名には一時キーを使用し、サーバー側で一時キーサービスを構築します。[PHPの例](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.php)、[Nodejsの例](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/sts.js)をご参照ください。
その他の言語の場合、またはご自身で実装する場合は次のフローを参照することができます。
（1）サーバーから一時キーを取得します。サーバーはまず固定キーのSecretId、SecretKeyを使用してSTSサービスから一時キーを取得し、一時キーのtmpSecretId、tmpSecretKey、sessionTokenを得ます。詳細については、[一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)または[cos-sts-sdk](https://github.com/tencentyun/qcloud-cos-sts-sdk)をご参照ください。
>!使用するリクエストがputかpostかによって、STSのpolicy actionに"name/cos:PutObject"または"name/cos:PostObject"の許可を追加する必要があります。

（2）フロントエンドはtmpSecretId、tmpSecretKey、method、pathnameによって署名を計算します。下記を参照し、[cos-auth.js](https://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.js)を使用して署名を計算します。業務上必要であれば、バックエンドに置いて署名を計算することもできます。
（3）計算によって得た署名およびsessionTokenをそれぞれ以下に置きます。
  - postリクエストのformDataのSignatureおよびx-cos-security-tokenフィールド内。COS APIに対しアップロードリクエストを送信します。
  - putリクエストのheadersのSignatureおよびx-cos-security-tokenフィールド内。COS APIに対しアップロードリクエストを送信します。

>! 正式なデプロイの際は、サーバーにウェブサイト自体の権限チェックを1段階追加してください。
>

#### 3. 後置記法リクエスト

COS APIの一般的なリクエスト形式はすべて`POST http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/`に類似しており、リクエストのドメイン名はバケットドメイン名です。ミニプログラムで複数のバケットを使用している場合、このバケットドメイン名をホワイトリストのドメイン名に設定する必要があります。対処方法は次のとおりです。

COSは後置記法のリクエスト形式`POST http://cos.ap-beijing.myqcloud.com/examplebucket-1250000000/`を提供しています。リクエストのドメイン名はリージョンドメイン名であり、バケット名はリクエストのパス内に含めます。ミニプログラム内で同一リージョンの複数のバケットを使用する場合は、1つのドメイン名`cos.ap-beijing.myqcloud.com`をホワイトリストのドメイン名に設定するだけです。

後置記法リクエスト形式で注意が必要なのは、署名の際に使用するパスに、バケット名をプレフィックスとするパスを用いなければならないという点です（例：`/examplebucket-1250000000/`）。

#### 4. 直接転送のサンプルコード

以下のコードは[PUT Object ](https://intl.cloud.tencent.com/document/product/436/7749)インターフェース（使用を推奨）と[POST Object ](https://intl.cloud.tencent.com/document/product/436/14690)インターフェースの例を同時に挙げたものです。操作ガイドは次のとおりです。

```js
var CosAuth = require('./cos-auth'); // ここではcos-auth.jsを参照しています。ダウンロードアドレスはhttps://unpkg.com/cos-js-sdk-v5/demo/common/cos-auth.min.jsです 

var Bucket = 'examplebucket-1250000000';
var Region = 'ap-shanghai';
var ForcePathStyle = false; // 後置記法を使用するかどうか。署名計算とドメイン名ホワイトリストの設定に関係します。後置記法の説明は上記をご参照ください

var uploadFile = function () {

    // リクエストに使用するパラメータです
    var prefix = 'https://' + Bucket + '.cos.' + Region + '.myqcloud.com/';
    if (ForcePathStyle) {
		// 後置記法リクエストは署名の際のドメイン名に、バケットドメイン名ではなくリージョンドメイン名を使用します。具体的な説明については上記の「3.後置記法リクエスト」をご覧ください
        prefix = 'https://cos.' + Region + '.myqcloud.com/' + Bucket + '/'; 
    }

    // その他の文字エンコードに対するurl encode形式です
    var camSafeUrlEncode = function (str) {
        return encodeURIComponent(str)
            .replace(/!/g, '%21')
            .replace(/'/g, '%27')
            .replace(/\(/g, '%28')
            .replace(/\)/g, '%29')
            .replace(/\*/g, '%2A');
    };

    // 一時キーを取得します
    var stsCache;
    var getCredentials = function (callback) {
        if (stsCache && Date.now() / 1000 + 30 < stsCache.expiredTime) {
            callback(data.credentials);
            return;
        }
        wx.request({
            method: 'GET',
            url: 'https://example.com/sts.php', // サーバーの署名です。上記を参照して一時キーを取得します
            dataType: 'json',
            success: function (result) {
                var data = result.data;
                var credentials = data.credentials;
                if (credentials) {
                    stsCache = data
                }else{
                    wx.showModal({title: '一時キーの取得に失敗しました', content: JSON.stringify(data), showCancel: false});
                }
                callback(stsCache && stsCache.credentials);
            },
            error: function (err) {
                wx.showModal({title: '一時キーの取得に失敗しました', content: JSON.stringify(err), showCancel: false});
            }
        });
    };

    // 署名計算
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

    // postによるファイルアップロード
    var postFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // ここでアップロードするファイル名を指定します
        var signPathname = '/'; // PostObjectインターフェースKeyはBodyに含めて転送するため、リクエストパスと署名パスは /
        if (ForcePathStyle) {
			  // 後置記法リクエストが署名の際に用いるパスにはバケット名を含める必要があります。具体的な説明については上記の「3.後置記法リクエスト」をご覧ください
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
                        wx.showModal({title: 'アップロードに成功しました', content: url, showCancel: false});
                    }else{
                        wx.showModal({title: 'アップロードに失敗しました', content: JSON.stringify(res), showCancel: false});
                    }
                },
                fail: function (res) {
                    wx.showModal({title: 'アップロードに失敗しました', content: JSON.stringify(res), showCancel: false});
                }
            });
            requestTask.onProgressUpdate(function (res) {
                console.log('進捗:', res);
            });
        });
    };

    // putによるファイルアップロード
    var putFile = function (filePath) {
        var Key = filePath.substr(filePath.lastIndexOf('/') + 1); // ここでアップロードするファイル名を指定します
        var signPathname = '/' + Key; // PutObjectインターフェースKeyはurlに含めて転送するため、リクエストパスと署名パスは /Key
        if (ForcePathStyle) {
			  // 後置記法リクエストが署名の際に用いるパスにはバケット名を含める必要があります。具体的な説明については上記の「3.後置記法リクエスト」をご覧ください
            signPathname = '/' + Bucket + '/' + Key;  
        }
        getAuthorization({Method: 'PUT', Pathname: signPathname}, function (AuthData) {
          // putリクエストは一時ファイルパスからファイル内容を読み取る必要があります
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
                      wx.showModal({title: 'アップロードに成功しました', content: url, showCancel: false});
                  }else{
                      wx.showModal({title: 'アップロードに失敗しました', content: JSON.stringify(res), showCancel: false});
                  }
                  console.log(res.statusCode);
                  console.log(url);
                },
                fail: function fail(res) {
                  wx.showModal({title: 'アップロードに失敗しました', content: JSON.stringify(res), showCancel: false});
                },
              });
              requestTask.onProgressUpdate(function (res) {
                  console.log('進捗中:', res);
              });
            },
          });
        });
    };

    // ファイルの選択
    wx.chooseImage({
        count: 1, // デフォルトでは9
        sizeType: ['original'], // オリジナル画像と圧縮画像のどちらも指定できます。ここではデフォルトでのオリジナル画像を使用します
        sourceType: ['album', 'camera'], // ソースをアルバムにするかカメラにするかを指定できます。デフォルトでは両方です
        success: function (res) {
            putFile(res.tempFiles[0].path); // putによるアップロードリクエスト。使用を推奨します
            // postFile(res.tempFiles[0].path); // postによるアップロードリクエスト
        }
    })
};
```

##  関連ドキュメント

ミニプログラムSDKをご利用になりたい場合は、ミニプログラムSDK [クイックスタート](https://intl.cloud.tencent.com/document/product/436/30609)のドキュメントをご参照ください。

