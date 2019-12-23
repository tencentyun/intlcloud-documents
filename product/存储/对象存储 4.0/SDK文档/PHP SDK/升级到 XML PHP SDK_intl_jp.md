JSON PHP SDKとXML PHP SDKのドキュメントを詳しく比較すると、単なる増分更新ではないことがわかります。XML PHP SDKは、フレームワーク、可用性、セキュリティが大幅に向上し、さらに使いやすさ、ロバスト性、および伝送性能が大幅に改善されます。XML PHP SDKにアップグレードする場合は、次のガイドラインを参照して、PHP SDKのアップグレードを完了してください。

## 機能比較

下記のグラフに、JSON PHP SDKとXML PHP SDKの主な機能の比較を示しています。

| 機能      | XML PHP SDK         | JSON PHP SDK                         |
| -------- | :------------: | :------------------:    |
| ファイルアップロード | ローカルファイル、バイトストリーム、入力ストリームのアップロードをサポートします<br>デフォルトでは、アップロードを上書きします<br>アップロードモードを知的に判断します<br>簡単なアップロードは最大5GBをサポートします<br>マルチパートアップロードは最大48.82TB（50,000GB）をサポートします | ローカルファイルのアップロードのみをサポートします<br>上書きかどうかを選択できます<br>簡単なアップロードかマルチパートアップロードかを手動で選択する必要があります<br>簡単アップロードは最大20MBをサポートします<br>マルチパートアップロードは最大64GBをサポートします |
| ファイルの削除 | 一括削除をサポートします | 単一ファイルの削除のみをサポートします |
| バケット基本操作 | バケットの作成<br>バケットの取得<br>バケットの削除   | サポートしません |
| バケットACL操作 | バケットACLを設定します<br>バケットACLの設定を取得します<br>バケットACLの設定を削除します   | サポートしません |
| バケットライフサイクル | バケットライフサイクルを作成します<br>バケットライフサイクルを取得します<br>バケットライフサイクルを削除します | サポートしません |
| ディレクトリ操作 | APIを独立に提供しません   | ディレクトリを作成します<br>ディレクトリを照合します<br>ディレクトリを削除します |


## アップグレード手順
PHP SDKをアップグレードするには、下記の4つの手順を実行してください。

**1. PHP SDKのアップデート**

COS XML PHP SDKのインストールは3つの方式があります。
* Composer方式。
* Phar方式。
* ソースコード方式。

**Composer方式**
PHPの依存管理ツールであるComposerを使用してCOS XML　PHP　SDKをインストールすることをお勧めします。プロジェクトに必要な依存関係を宣言し、プロジェクトに自動的にインストールできます。

Composerのインストール方法、自動ロードの構成、依存関係を定義するその他のベストプラクティスについての詳細は、「Composer公式サイト」(https://getcomposer.org/)を参照してください。

Composerを使用するXML　PHP　SDKのインストール手順は下記の通りです。
1）ターミナルを開きます。
2）Composerをダウンロードし、下記のコマンドを実行します。
```
curl -sS https://getcomposer.org/installer | php
```
3）`composer.json`という名前のファイルを下記のように作成します。
```
{
    "require": {
        "qcloud/cos-sdk-v5": "1.*"
    }
}
```
4）Composerでインストールし、下記のコマンドを実行します。
```
php composer.phar install
```
このコマンドを使用すると、現在のディレクトリにvendorフォルダが作成されます。このフォルダには、簡単に呼び出すためにSDKの依存ライブラリとautoload.phpスクリプトが含まれています。

5）autoloaderスクリプトによってXML　PHP　SDKを呼び出す。
```
require '/path/to/sdk/vendor/autoload.php';
```

プロジェクトはCOS XML　PHP　SDKを使用できるようになりました。


**Phar方式**
Phar方式でXML　PHP　SDKのインストール手順は下記の通りです。

1）「GitHub発表画面」(https://github.com/tencentyun/cos-php-sdk-v5/releases)に相応するPharファイアをダウンロードします。

2）コードにpharファイルを取り込みます。
```
require  '/path/to/cos-sdk-v5.phar';
```

**ソースコード方式**
ソースコード方式でSDKのインストール手順は下記の通りです。

1）「GitHub発表画面」(https://github.com/tencentyun/cos-php-sdk-v5/releases)に相応するcos-sdk-v5.tar.gz圧縮ファイルをダウンロードします。

2）圧縮ファイルを解凍して、autoload.phpスクリプトを使用してSDKをロードします。
```
require '/path/to/sdk/vendor/autoload.php';
```

**2. SDKの初期化方式の変更**

XML PHP SDKでは、初期化APIがいくつか変更されています。これに対応して変更してください。

JSON PHP SDKの初期化方式は下記の通りです。

```
require('cos-php-sdk-v4/include.php'); 
use Qcloud\Cos\Api;
//COSClientConfigオブジェクトを作成し、必要に応じてデフォルトの構成パラメータを変更します
$config = array(
    'app_id' => '',
    'secret_id' => '',
    'secret_key' => '',
    'region' => 'gz',
    'timeout' => 60
);
//cosApiオブジェクトを作成して、COSの操作を実装します。
$cosApi = new Api($config);
```

XML PHP SDKの初期化方式は下記の通りです。

```
require '/path/to/sdk/vendor/autoload.php';
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv(' COS_SECRETID'),
        'secretKey' => getenv(' COS_SECRETKEY'))));
```


**3. バケット名称とAvailability Zoneの略称を変更します**

XML PHP SDKのバケット名と可能な地域の短縮名は、JSON PHP SDKとは異なり、状況に対応して変更する必要があります。

**バケット**
XML PHP SDKバケット名は、ユーザー設定の文字列とAPPID2つの部分で構成されています。これらはハイフン「-」でつなぎます。
例えば、`examplebucket-1250000000`の場合、`examplebucket`はユーザー設定の文字列、`1250000000`はAPPIDです。

>？APPIDはTencent Cloudアカウントのアカウントタグの1つで、クラウドリソースを関連付けるために使用されます。ユーザーがTencent Cloudアカウントの申し込みに成功すると、システムは自動的にAPPIDをユーザーに割り当てます。「Tencent Cloudコンソール」(https://console.cloud.tencent.com/)にログインして「アカウント情報」でAPPIDを確認できます。

**バケットのAvailability Zoneの略称Region**
XML PHP SDKのバケットの可能な地域の短縮名が変更されました。初期化時に、regionフィールドを下記のように入力してください。

| 地域       | XML PHP SDK地域短縮名         | JSON PHP SDK地域短縮名                        |
| -------- | ------------ | ---------------------------------------- |
| 北京1区（華北） | ap-beijing-1 | tj |
| 北京       | ap-beijing   | bj |
| 上海（華東）   | ap-shanghai  | sh |
| 広州（華南）   | ap-guangzhou | gz |
| 成都（西南）   | ap-chengdu   | cd |
| 重慶       | ap-chongqing | 無し |
| シンガポール      | ap-singapore | sgp |
| 香港       | ap-hongkong  | hk |
| トロント      | na-toronto   | ca |
| フランクフルト     | eu-frankfurt | ger |
| ムンバイ       | ap-mumbai    | 無し |
| ソウル       | ap-seoul     | 無し |
| シリコンバレー       | na-siliconvalley     | 無し |
| バージニア       | na-ashburn     | 無し |
| バンコク       | ap-bangkok     | 無し |
| モスクワ       | eu-moscow     | 無し |


**4. APIの変更
XML PHP SDKにアップグレードした後、一部操作のAPIが変更されました。実際のニーズに合わせて変更してください。SDKを使いやすくするためにAPIをカプセル化しました。詳細については、例と「APIドキュメント」(https://cloud.tencent.com/document/product/436/12267)を参照してください。

API変化は以下の3点があります：

**1）独立のディレクトリAPIがありません**

XML SDKでは、個別のディレクトリAPIは提供されなくなりました。COSにはフォルダとディレクトリの概念はありません。オブジェクトストレージでは、オブジェクト`project/a.txt`のアップロードによってprojectフォルダは作成されません。ユーザの使用習慣を満たすために、COSはコンソールやCOS browserなどのグラフィカルツールに「フォルダ」または「ディレクトリ」の表示方法をシミュレートします。具体的にはキー値が`project/`で、中身が空のオブジェクトを作成することで、従来のフォルダをエミュレートする表示方法で実現します。

たとえば、アップロードオブジェクト`project/doc/a.txt`、区切り記号`/`は「フォルダ」の表示方法をシミュレートし、コンソールに「フォルダ」projectとdocが表示されます。docはprojectの下位レベルの「フォルダ」で、a.txtファイルが含まれています。

したがって、適用シナリオは単にファイルをアップロードするだけの場合は、最初にフォルダを作成せずに、直接アップロードすることができます。適用シナリオにフォルダの概念がある場合、フォルダの作成機能を提供する必要があります。パスは`／`で終わる0KBのファイルをアップロードできます。これにより、`GetBucket`APIを呼び出すときにこのようなファイルをフォルダとして扱うことができます。

**2）署名アルゴリズムの変化**

通常は手動で署名を計算する必要がないが、SDKの署名をフロントエンドに返却して使用する場合、署名アルゴリズムの変化に注意してください。署名につき、単回と複数回署名の区別がなくなり、一方、署名の有効期の設定により安全性を確保するようになります。詳しいアルゴリズムについては、[XML署名のリクエスト](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください。


**3）新規追加されたAPI**

XML PHP SDKには、下記のような多くの新しいAPIが追加されています。
* バケットの操作、例えば、PutBucketRequest、GetBucketRequest、ListBucketRequestなど。
* バケットACLの操作、例えば、PutBucketACLRequest、GetBucketACLRequestなど。
* バケットのライフサイクルの操作、例えば、PutBucketLifecycleRequest、GetBucketLifecycleRequestなど。

詳細については、PHP SDK[APIドキュメント](https://cloud.tencent.com/document/product/436/12267)を参照してください。




