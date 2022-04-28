### COSはファイル解凍をサポートしていますか。

ファイル解凍機能はTencent CloudのCloud Object Storage（COS）が[Serverless Cloud Function（SCF）](https://intl.cloud.tencent.com/document/product/583)をベースにして提供するデータ処理ソリューションです。詳細については、[ファイル解凍設定](https://intl.cloud.tencent.com/document/product/436/35663)をご参照ください。

### COSのファイル解凍機能は第2階層ディレクトリ下の圧縮ファイルの解凍をサポートしていますか。

現在のファイル解凍機能では、第2階層ディレクトリ下の圧縮パッケージを解凍することはできません。このケースはご自身で関数のロジックを調整することで実現できます。

### COSはアップロード時のファイル自動圧縮をサポートしていますか。

サポートしません。

### COSはCDNの自動更新設定をサポートしていますか。

[Serverless Cloud Function（SCF）](https://intl.cloud.tencent.com/document/product/583)によって自動更新を設定できます。詳細については、[CDNキャッシュ更新の設定](https://intl.cloud.tencent.com/document/product/436/37273)をご参照ください。

### クラウドデータベースのデータをCOSにバックアップすることは可能ですか。

[Serverless Cloud Function（SCF）](https://intl.cloud.tencent.com/document/product/583)によってデータベースバックアップ機能を設定することができます。ユーザーが指定のバケット内にバックアップ関数ルールを設定すると、SCFはデータベースバックアップファイルを定期的にスキャンし、ファイルをバケット内に転送して保存します。詳細については、[クラウドデータベースバックアップの設定](https://intl.cloud.tencent.com/document/product/436/39629)をご参照ください。

