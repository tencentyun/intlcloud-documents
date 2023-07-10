### COS Python SDKのアップグレード後に、「ファイル移動」操作が実行できなくなりましたが、どのように対処すればよいですか。

[PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)および[DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)インターフェースを使用して実現できます。削除操作を実行する前に、データの整合性を検証することをお勧めします。詳細な説明については、[MD5検証](https://intl.cloud.tencent.com/document/product/436/32467)のドキュメントをご参照ください。

### COS Python SDKによってダウンロードファイルの一時リンクを取得するにはどうすればよいですか。

Python SDKは署名取得、リクエスト署名付きURL取得インターフェースおよびオブジェクトダウンロード用署名付きURL取得インターフェースを提供しています。パーマネントキーを使用する場合と一時キーを使用する場合では、署名付きURL取得のための呼び出し方法は同じですが、一時キーを使用する場合はheaderまたはquery_stringにx-cos-security-tokenを追加する必要があります。詳細については、[署名付きURLの生成](https://intl.cloud.tencent.com/document/product/436/31548)のドキュメントをご参照ください。

### COS Python SDKを使用した際にエラーが発生しましたが、どのように対処すればよいですか。

COS XML Python SDKの操作に成功すると、dictまたはNoneが返されます。SDKインターフェースを呼び出してCOSサービスのリクエストを行って失敗した場合、システムはCosClientError（クライアントのエラー）またはCosServiceError（サーバーのエラー）をスローします。

- サーバーから返されたエラー：サーバーが要件に適合しないクライアントのリクエストを処理した場合に返されるエラーです。例えば、存在しないファイルにアクセスした場合、ファイルへのアクセス権限がない場合などです。サーバーから返されるエラーコードの詳細な情報については、[APIエラーコード](https://intl.cloud.tencent.com/document/product/436/7730)をご参照ください。
- クライアントエラー：主にネットワークエラー、ファイルの読み取り/書き込みIOのエラー、パラメータチェックの失敗などがあります。

