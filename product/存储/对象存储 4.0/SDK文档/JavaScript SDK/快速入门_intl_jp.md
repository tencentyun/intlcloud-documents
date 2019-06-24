## 開発準備

### SDKの取得

COSのXML JS SDK リソース githubアドレス：[tencentyun/cos-js-sdk-v5](https://github.com/tencentyun/cos-js-sdk-v5)。

Demoのダウンロードアドレス：[XML JS SDK Demo](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo)。

### 開発準備

1. JS SDKは、HTML5基本特性をサポートするブラウザが必要とされ、それでajaxのアップロードファイルとファイルmd5値の計算をサポートします。
2. [COSオブジェクトストレージコンソール](https://console.cloud.tencent.com/cos4)でバケットを作成し、Bucket（バケット名）と[Region](https://cloud.tencent.com/document/product/436/6224)（地域名称）を取得します。
3. [コンソール暗号鍵管理](https://console.cloud.tencent.com/capi)でプロジェクトSecretIdとSecretKeyを取得します。
4. CORS規則を構成します。構成例を下図に示します。
![cors](//mc.qcloudimg.com/static/img/2e7791e9274ce3ebf8b25bbeafcd7b45/image.png)


>?文章に記載されているSecretId、SecretKey、Bucketなどの名称の意味と取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。
    
## クイックスタート		
### 一時暗号鍵の取得

暗号鍵をフロントエンドに配置するとSecretIdとSecretKeyがさらけ出されるため、永続暗号鍵プロセスをバックエンドに配置します。フロントエンドがajaxを介してバックエンドから一時暗号鍵を取得し、正式配置ときにバックエンドに当サイトの権限チェックを追加します。具体的な内容について[一時暗号鍵の生成および使用ガイドライン](https://cloud.tencent.com/document/product/436/14048)ドキュメントを参照してください。

### アップロード例

1. test.htmlを作成し、次のコードを入力し、BucketとRegionを変更します。
2. バックエンドの一時暗号鍵サービスを配置してから、getAuthorizationの暗号鍵サービスアドレスを変更します。
3. test.htmlをWebサーバー下に格納し、ブラウザからページにアクセスし、ファイルアップロードをテストします。

test.htmlファイルのサンプルコードは以下の通りです。 
```
<input id="file-selector" type="file">
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'test-1250000000';
var Region = 'ap-guangzhou';

// インスタンスの初期化
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 一時暗号鍵の非同期取得
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

// ユーザーがファイルを選択したかどうかをリスニングする
document.getElementById('file-selector').onchange = function () {
    
    var file = this.files[0];
    if (!file) return;

    // ファイルのシャードアップロード
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


## webpackの参照方式

webpackによってまとめられたシナリオをサポートするには、npmをモジュールとして参照します。コードは以下の通りです。
```shell
npm i cos-js-sdk-v5 --save
```

## その他のドキュメントとコード例

1. 他のコード例については、[XML JavaScript SDK Demo](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/demo)を参照してください。
2. 完全なAPIドキュメントについては、[XML JavaScript SDKAPIドキュメント](https://cloud.tencent.com/document/product/436/12260)を参照してください。

