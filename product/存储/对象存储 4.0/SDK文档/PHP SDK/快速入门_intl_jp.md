本文は主にCOS PHP SDK V5バージョンのクイックスタートについて紹介します。XML APIドキュメントは[XML API 概要](https://cloud.tencent.com/document/product/436/7751)を参照してください。

## 環境の準備
*   PHP　5.3+
    `php -v`コマンドで現在のPHPバージョンを確認します。
*   cURL拡張
    `php -m`コマンドで、cURL拡張機能がインストールされているかどうかを確認することができます。

>- Ubuntuシステムでは、apt-getパッケージマネージャーを使用してPHPのcURL拡張機能をインストールします。インストールコマンドは下記の通りです。
```
sudo apt-get install php-curl
```
>- CentOSシステムでは、yumパッケージマネージャーを使用してPHPのcURL拡張機能をインストールすることができます。
```
sudo yum install php-curl
```

## SDKのインストール
SDKのインストールには3つの方式があります。
* Composer方式。
* Phar方式。
* ソースコード方式。

### Composer方式
PHPの依存管理ツールであるComposerを使用してcos-php-sdk-v5をインストールすることをお勧めします。プロジェクトに必要な依存関係を宣言し、プロジェクトに自動的にインストールできます。
Composerのインストール方法、自動ロードの構成、依存関係を定義するその他のベストプラクティスについての詳細は、「Composer公式サイト」(https://getcomposer.org/)を参照してください。

#### インストール手順： 
1. ターミナルを開く。
2. Composerをダウンロードし、下記のコマンドを実行する。
```
curl -sS https://getcomposer.org/installer | php
```
3. `composer.json`という名前のファイルを下記のように作成する。
```
{
    "require": {
        "qcloud/cos-sdk-v5": "1.*"
    }
}
```
4. Composerを使用してインストールし、下記のコマンドを実行する。
```
php composer.phar install
```
このコマンドを使用すると、現在のディレクトリにvendorフォルダが作成されます。このフォルダには、簡単に呼び出すためにSDKの依存ライブラリとautoload.phpスクリプトが含まれています。
5. autoloaderスクリプトによってcos-php-sdk-v5を呼び出す。
```
require '/path/to/sdk/vendor/autoload.php';
```

プロジェクトはCOS V5バージョンSDKを使用できるようになりました。

### Phar方式
Phar方式でSDKのインストール手順は下記の通りです。
1. [GitHub発表画面](https://github.com/tencentyun/cos-php-sdk-v5/releases)に相応するpharファイルをダウンロードする。
2. コードにpharファイルを取り込む。
```
require  '/path/to/cos-sdk-v5.phar';
```

### ソースコード方式
ソースコード方式でSDKのインストール手順は下記の通りです。
1. [GitHub 発表画面](https://github.com/tencentyun/cos-php-sdk-v5/releases)に相応するcos-sdk-v5.tar.gz圧縮ファイルをダウンロードする。
2. 圧縮ファイルを解凍して、autoload.phpスクリプトを使用してSDKをロードする。
```
require '/path/to/sdk/vendor/autoload.php';
```

## クイックスタート 
Demoプログラムを参照して、詳細については[sample.php](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/sample.php)を参照してください。

## APIドキュメント
詳細については、PHP SDK [APIドキュメント](https://cloud.tencent.com/document/product/436/12267)を参照してください。

### 構成ファイル
```php
$cosClient = new Qcloud\Cos\Client(array('region' => '<Region>',
    'credentials'=> array(
        'secretId'    => '<SecretId>',
        'secretKey' => '<SecretKey>')));
```

[一時暗号鍵](https://cloud.tencent.com/document/product/436/14048)を使用して初期化する場合、下記の方法でインスタンスを作成してください。

```
$cosClient = new Qcloud\Cos\Client(array('region' => '<Region>',
    'credentials'=> array(
        'secretId'    => '<SecretId>',
        'secretKey' => '<SecretKey>',
        'token' => '<XCosSecurityToken>')));
```

### ファイルのアップロード
* putObject APIを使用するファイルのアップロード（最大5GB）
* Upload APIを使用するマルチパートアップロード

```php
# ファイルのアップロード
## putObject（アップロードAPI、最大5GBのファイルアップロードをサポートします）
### メモリ内の文字列のアップロード
//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### ファイルストリームのアップロード
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb')));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### headerとmetaの設定
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb'),
        'ACL' => 'string',
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => integer,
        'ContentType' => 'string',
        'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'GrantFullControl' => 'string',
        'GrantRead' => 'string',
        'GrantWrite' => 'string',
        'Metadata' => array(
            'string' => 'string',
        ),
        'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

## Upload（ハイレベルのアップロードAPI、デフォルトではマルチパートアップロードは最大50TBをサポートします）
### メモリ内の文字列のアップロード
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = 'Hello World!');
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### ファイルストリームのアップロード
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### headerとmetaの設定
try {
    $result = $cosClient->Upload(
        $bucket= $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'),
        $options = array(
            'ACL' => 'string',
            'CacheControl' => 'string',
            'ContentDisposition' => 'string',
            'ContentEncoding' => 'string',
            'ContentLanguage' => 'string',
            'ContentLength' => integer,
            'ContentType' => 'string',
            'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
            'GrantFullControl' => 'string',
            'GrantRead' => 'string',
            'GrantWrite' => 'string',
            'Metadata' => array(
                'string' => 'string',
            ),
            'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

### ファイルのダウンロード
* getObject　APIを使用するファイルのダウンロード
* getObjectUrl　APIを使用して、ファイルダウンロードのURLの取得

```php
# ファイルのダウンロード
## getObject（ファイルのダウンロード）
### メモリにダウンロード
//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    echo($result['Body']);
} catch (\Exception $e) {
    echo "$e\n";
}

### ローカルにダウンロード
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### ダウンロード範囲の指定
/*
 * Rangeフィールドのフォーマットは'bytes=a-b'です
 */
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### headerへ戻る設定
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'ResponseCacheControl' => 'string',
        'ResponseContentDisposition' => 'string',
        'ResponseContentEncoding' => 'string',
        'ResponseContentLanguage' => 'string',
        'ResponseContentType' => 'string',
        'ResponseExpires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

## getObjectURL（ファイルURLの取得）
try {
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    echo $signedUrl;
} catch (\Exception $e) {
    print_r($e);
}
```


