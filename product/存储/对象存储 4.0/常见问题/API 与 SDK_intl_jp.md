### どのようにAPIを呼び出しアップロード未完了のファイルを削除しますか？

先に、ListMultipartUploads APIを呼び出し、アップロード未完了のファイル一覧を示し、次にAbort Multipart upload　APIを呼び出し、分割アップロードを捨て、アップロードされたパートを削除します。

### 一括削除APIを呼び出して正しいと返されましたが、実際にファイルが削除されていなません。どうすればいい？

削除するファイルパスを確認してください。ファイルパスは「/」で始まる必要がありません。

### JSON APIで作成したバケットとアップロードするオブジェクトは、XML APIで管理できますか？

できます。XML APIはCOS最下層アーキテクチャに基づくものです。XML APIによってJSON APIにより生成されたデータを操作できます。

### XML APIとJSON APIの間の関係は？

 JSON APIは、2016年9月からユーザーがCOSにアクセスする時に使用するAPIです。アップロード用ドメイン名は、`<Region>.file.myqcloud.com`です。JSON APIはメンテナンス状態を維持し、正常に使用できますが新特性を開発しません。それが標準XML APIの最下層アーキテクチャと同じ、データの相互運用性があり、交互に使うことができますが、API互換性がなく、ドメイン名が一致しません。

### XML APIとJSON APIの暗号鍵は共通ですか？

共通です。暗号鍵は、[クラウドAPI暗号鍵コンソール](https://console.cloud.tencent.com/capi)で確認できます。

### XML APIとJSON APIの署名は共通ですか？

共通ではありません。XML APIとJSON APIはそれぞれの署名方式があります。詳細について次を参照してください。

- [JSON API署名](https://cloud.tencent.com/document/product/436/6054)
- [XML API署名](https://intl.cloud.tencent.com/document/product/436/7778)

### XML APIとJSON APIに設定されるACL権限は共通ですか？

共通ではありません。XML APIとJSON APIはそれぞれのACL権限があります。

### Python SDKダウンロードファイルのテンポラリリンクをどのように取得しますか？

詳細について、[事前署名ダウンロードリンクの取得](https://cloud.tencent.com/document/product/436/12270#.E8.8E.B7.E5.8F.96.E9.A2.84.E7.AD.BE.E5.90.8D.E4.B8.8B.E8.BD.BD.E9.93.BE.E6.8E.A5)ドキュメントを参照してください。

### SDKはCDNアクセラレーションドメイン名でアクセスできますか？

できます。使用するプログラミング言語に対応する[SDK ドキュメント](https://cloud.tencent.com/document/sdk)を参照しながら、操作してください。


### ミニプログラムで複数のドメイン名をリクエストし、またはバケット名が未知である場合、ホワイトリスト構成と制限問題をどのように解決しますか？

SDKのインスタンス化の時、`ForcePathStyle:true`でサフィックスを有効にできます。リクエスト対象url形式は、`https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>`サフィックスリクエストであれば、署名の時にバケット名`/<BucketName-APPID>`が署名計算に参加します。

### ミニプログラムはどのように画像をローカルに保存しますか？
先に`cos.getObjectUrl`で画像urlを取得し、次に`wx.downloadFile`を呼び出し画像をダウンロードしテンポラリパスを取得し、画面に画像保存ボタンが表示され、ユーザーがボタンをクリックし、`wx.saveImageToPhotosAlbum`を呼び出し、アルバムに保存します。

