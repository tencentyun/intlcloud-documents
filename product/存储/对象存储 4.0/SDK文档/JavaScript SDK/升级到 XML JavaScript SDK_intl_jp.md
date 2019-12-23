JSON  JavaScript SDKとXML  JavaScript SDKのドキュメントを詳しく比較すると、単なる増分更新ではないと分かります。XML  JavaScript SDKは、アーキテクチャ、可用性およびセ

## 機能比較

| 機能           |                     XML  JavaScript SDK                      |                     JSON  JavaScript SDK                     |
| -------------- | :----------------------------------------------------------: | :----------------------------------------------------------: |
| ファイルアップロード       | ローカルファイル、文字列内容をサポートします<br>デフォルトでアップロードを上書きします<br/>シャードアップロードは一括アップロードをサポートします<br>アップロードモードのスマート判断可能：簡易アップロードは最大5GBをサポートします<br>分割アップロードは最大48.82TB（50,000GB）をサポートします | ローカルファイルのアップロードのみをサポートします<br>上書きをするかどうかを選択できます<br/>20MB以下の場合、簡易アップロードを使用し、20MBを超えた場合、自動シャードアップロードをします<br>簡易アップロードは最大20MBをサポートします<br>シャードアップロードは最大64GBをサポートします |
| ファイルの削除       |                         一括削除をサポートします                         |                       単一ファイル削除のみをサポートします                       |
| バケットの基本操作 |            バケットの作成<br>バケットの取得<br>バケットの削除            |                            サポートしません                            |
| バケットACL操作  |   バケットACLを設定します<br>設定したバケットACLを取得します<br>設定したバケットACLを削除します    |                            非対応                            |
| バケットのライフサイクル | バケットのライフサイクルの作成<br>バケットのライフサイクルの取得<br>バケットのライフサイクルの削除 |                            サポートしません                            |
| ディレクトリ操作       |                        単独APIを提供しません                        |               ディレクトリを作成します<br>ディレクトリを照合します<br>ディレクトリを削除します               |
| 一時的な暗号鍵を使用します   |                     一時的な暗号鍵をサポートし、それをおすすめします                     |                        一時的な暗号鍵をサポートしません                        |

## アップグレード手順

#### 1. JavaScript SDKのアップデート

XML  JavaScript SDKについて[npm](https://www.npmjs.com/package/cos-js-sdk-v5)倉庫でリリースされ、npmインストール依頼パッケージをおすすめします。

```js
npm install cos-js-sdk-v5
```

githubソースコードでjsファイル[dist/cos-js-sdk-v5.min.js](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/dist)をダウンロードし、scriptタグを介してHTMLページに追加します。

```html
<script src="./cos-js-sdk-v5.min.js"></script>
```

#### 2. バケット名称と可能な地域の略称の変更

XML  JavaScript SDKのバケット名称と可能な地域の略称は JSON  JavaScript SDKと異なり、適切な変更が必要とされます。

#### バケット Bucket

XML  JavaScript SDK  バケット名称は、ユーザーカスタマイズ文字列とAPPIDからなり、両者はハイフン「-」で繋ぎます。
例えば、 `examplebucket-1250000000`、そのうち、 `examplebucket` はユーザーカスタマイズ文字列であり、`1250000000` はAPPIDです。

> ?APPIDは、Tencent Cloudアカウントのアカウント識別子の1つで、クラウドリソースを関連づけます。ユーザーがTencent Cloudアカウントを申請した後、システムは、自動的にユーザーに1つのAPPIDを割り当てます。[Tencent Cloudコンソール](https://console.cloud.tencent.com/) の【アカウント情報】でAPPIDを確認できます。

Bucketの設定について、以下のアップロードコード例を参照してください。

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

#### バケットの可能な地域の略称：Region

XML  JavaScript SDK のバケットの可能な地域の略称は変化します。地域ごとにJSON  JavaScript SDKとXML  JavaScript SDKの対応関係について、下表を参照してください。

| 地域             | XML SDK 地域略称      | JSON SDK 地域略称 |
| ---------------- | ---------------- | ----------- |
| 北京1区（華北） | ap-beijing-1     | tj          |
| 北京             | ap-beijing       | bj          |
| 上海（華東）     | ap-shanghai      | sh          |
| 広州（華南）     | ap-guangzhou     | gz          |
| 成都（西南）     | ap-chengdu       | cd          |
| 重慶             | ap-chongqing     | なし          |
| シンガポール           | ap-singapore     | sgp         |
| 香港             | ap-hongkong      | hk          |
| トロント           | na-toronto       | ca          |
| フランクフルト         | eu-frankfurt     | ger         |
| ボンベイ             | ap-mumbai        | なし          |
| ソウル             | ap-seoul         | なし          |
| シリコンバレー             | na-siliconvalley | なし          |
| バージニア州         | na-ashburn       | なし          |
| バンコク             | ap-bangkok       | なし          |
| モスクワ           | eu-moscow        | なし          |

[地域とアクセスドメイン名](https://cloud.tencent.com/document/product/436/6224) ドキュメントも参照してください。

各メソッドを呼び出す際には、バケットの所在地域の略称をパラメータ `Region`に設定してください。

```java
cos.headBucket({
    Bucket: 'examplebucket-1250000000,
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

#### 3. APIの変更

XML JavaScript SDKにアップグレードした後、一部操作のAPIが変化しますので、実際の需要に応じて変更してください。

また、SDKを使いやすくするためにAPIをカプセル化しました。詳細については、[サンプルコード](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo)と[APIドキュメント](https://cloud.tencent.com/document/product/436/12260)を参照してください。

APIの変更には、主に以下の変更があります。

**1）独立のディレクトリAPIがありません**

XML SDKでは、個別のディレクトリAPIは提供されなくなりました。COSにはフォルダとディレクトリの概念はありません。COSでは、オブジェクト`project/a.txt`のアップロードによってprojectフォルダは作成されません。COSはコンソールやCOS browserなどのグラフィカルツールに「フォルダ」または「ディレクトリ」の表示方法をエミュレートします。具体的にはキー値が`project/`で、中身が空のオブジェクトを作成することで、従来のフォルダをエミュレートする表示方法で実現します。

たとえば、アップロードオブジェクト`project/doc/a.txt`、区切り記号`/`は「フォルダ」の表示方法をシミュレートし、コンソールに「フォルダ」projectとdocが表示されます。docはprojectの下位レベルの「フォルダ」で、a.txtファイルが含まれています。

したがって、適用シナリオは単にファイルをアップロードするだけの場合は、最初にフォルダを作成ずに、直接アップロードすることができます。適用シナリオにフォルダの概念がある場合、フォルダの作成機能を提供する必要があります。パスは`／`で終わる0KBのファイルをアップロードできます。これにより、GetBucket APIを呼び出すときにこのファイルをフォルダとして扱うことができます。

**2）一時暗号鍵による認証**

暗号鍵をフロントエンドコードに入れるとセキュリティリスクがあり、アプリケーションサーバーでの署名計算によってフロントエンドに権限を与えることはコントロールしにくいため、XML  JavaScript SDKでは、一時暗号鍵をおすすめします。具体的なコードについて、以下のアップロード完全例を参照してください。

```js
var Bucket = 'examplebucket-1250000000';
var Region = 'ap-beijing';
var cos = new COS({
    getAuthorization: function (options, callback) {
        var url = 'http://example.com/sts.php';
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            try {
                var data = JSON.parse(e.target.responseText);
                var credentials = date.credentials;
            } catch (e) {
            }
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                ExpiredTime: data.expiredTime,
            });
        };
        xhr.send();
    }
});
cos.putObject({
    Bucket: Bucket,
    Region: Region,
    Key: file.name,
    Body: file,
    onProgress: function (progressData) {
        console.log('アップロード中', JSON.stringify(progressData));
    },
}, function (err, data) {
    console.log(err, data);
});
```

それでもアプリケーションサーバーを使用して手動で署名を計算してから、フロントエンドに戻って使用する方式の場合は、署名アルゴリズムが変更されたことに注意してください。署名は単一の署名と複数の署名を区別しなくなりましたが、署名の有効期間の設定によってセキュリティを確保します。署名をアップデートするには、[XMLリクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください。

**3）パラメータと返された統一なフォーマット**

パラメータはオブジェクトです。ツールメソッドを除き、以下のように、APIフォーマットは、コールバックによってエラー情報または成功結果を返します。

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing-1',
    Key: '1.txt',
}, function (err, data) {
    console.log(err || data);
});
```

**4）新しいAPI**

XML JavaScript SDKの新規追加APIを場合により呼び出すことができます。以下を含みます：

- バケットの操作。例えば、getService、putBucket、getBucketなど。
- バケットACLの操作。例えば、getBucketAcl、putBucketAclなど。
- バケットPolicyの操作：putBucketPolicy、getBucketPolicy、deleteBucketPolicy。
- バケットライフサイクルの操作。例えば、putBucketLifecycle、getBucketLifecycle、deleteBucketLifecycle。
- オブジェクトACLの操作：getObjectAcl、putObjectAcl。
- オブジェクトレプリケーションの操作：putObjectCopy、sliceCopyFile。
- ツールメソッド：getObjectUrl。
- オブジェクトアップロードキュー：pauseTask、restartTask、cancelTask、getTaskListメソッドおよびlist-updateイベント。

詳細については、[JavaScript SDKAPIドキュメント](https://cloud.tencent.com/document/product/436/12260)を参照してください。

