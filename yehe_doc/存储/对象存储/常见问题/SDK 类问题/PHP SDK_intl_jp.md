### PHP SDKが実行時に`Call to undefined method GuzzleHttp\Utils::chooseHandler()`というエラーをスローしましたが、どのように対処すればよいですか。


PHP SDKはGuzzleに依存しています。ユーザーにはComposer方式でSDKをインストールすることをお勧めします。
- Composer方式でインストールする場合は、`php composer.phar install`コマンドを実行してSDKと依存関係をインストールする必要があります。
- ソースコード方式でインストールする場合は、`composer install`コマンドを実行してSDKと依存関係をインストールする必要があります。詳細については、[PHP SDK - ダウンロードとインストール](https://intl.cloud.tencent.com/document/product/436/12266)をご参照ください。


### COSでPHP SDKにアクセスしてファイルをアップロードする際に、`cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html`というエラーが発生しましたが、どのように対処すればよいですか。

PHP環境証明書に問題がある場合に、`cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html`に類似したエラーが発生することがあります。次の手順に従って解決を試みてください。

1. `https://curl.haxx.se/ca/cacert.pem`のアドレスにアクセスして証明書ファイルcacert.pemをダウンロードし、PHPインストールパスに保存します。
2. php.iniファイルを編集し、curl.cainfo設定項目の前のコメント記号セミコロン（;）を削除し、保存した証明書ファイルのcacert.pemの絶対パスを値として設定します。
3. PHPに依存するサービスを再起動します。

