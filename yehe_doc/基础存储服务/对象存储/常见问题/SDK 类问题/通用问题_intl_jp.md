### 指定のファイルストリームまたはファイルハンドラ方式によってアップロードを行うと、実際にアップロードされたコンテンツが分割されたり、サイズが0になったりしますが、どのように対処すればよいですか。

ファイルストリームまたはファイルハンドラ等の方式を使用してアップロードする場合、それらのストリームまたはハンドラには通常、オフセットポインタが含まれます。COSによってアップロードを行う前にこれらのストリームまたはハンドラを使用した場合、そのオフセットポインタはファイルの開始位置を指していない可能性があります。SDKはアップロードの際にデフォルトでこのオフセットポインタの位置からコンテンツを読みとるため、コンテンツが分割されたり、空ファイルがそのままアップロードされたりする可能性があります。オフセットをチェックし、必要に応じてオフセットポインタを開始位置に合わせることをお勧めします。

### アップロード完了後にファイルのURLを取得するにはどうすればよいですか。

COSのオブジェクトアクセスアドレス（ファイルURL）を、固定された形式を使用してスプライシングします。さらに詳しくお知りになりたい場合は、[オブジェクトの概要- オブジェクトアクセスアドレス](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください。


### ファイルをアップロードする際に「一時キーの期限切れ」エラーが発生しましたが、どのように対処すればよいですか。

次の手順に従って、トラブルシューティングを実施してください。
1. 現在の実行プログラムのマシン時刻が正確かどうかをチェックし、もし正確でなければ、マシン時刻を正確な時刻に修正してください。
2. 設定した有効期限（expirationDate）が現在の時刻より前の場合は、現在時刻が有効期限を過ぎると署名が期限切れとなるため、有効期限を変更して一時キーを再度生成する必要があります。
3. iOS SDKは初期化の際にQCloudSignatureProviderとQCloudCredentailFenceQueueDelegateという2つのプロトコルを使用します。一方、QCloudCredentailFenceQueueのスキャフォールディングは、一時キーに対しキャッシュと再利用を行うため、credentialFenceQueueインスタンスを再度初期化してキャッシュを更新することで、期限切れの一時キーの使用を避けることができます。詳細なガイドについては、[iOS SDKによるCOSサービスインスタンスの作成](https://intl.cloud.tencent.com/document/product/436/11280)をご参照ください。

### ファイルのアップロードが成功したことを確認するにはどうすればよいですか。

COS内の各オブジェクトにはそれぞれに**Etag**値が対応しており、ファイルのアップロードに成功すると、StringタイプのEtag値が返されます。アップロード成功後に返されるEtagはNULLではないため、判断条件を追加することで、ファイルのアップロードが成功したかどうかを確認することができます。

### リンク不正アクセス防止を設定していますが、Appでリンク不正アクセス防止設定済みのオブジェクトをリクエストするにはどうすればよいですか。

リクエスト送信時に指定のrefererを含むHeaderを追加することで、オブジェクトを正常にリクエストすることができます。


### 署名付きリンクを生成するとネットワークリクエストおよび料金が発生しますか。遅延は発生しますか。
署名付きリンクの生成はローカルロジックであり、ネットワークリクエストは発生しません。そのため、余計なネットワーク遅延は発生せず、追加料金が発生することもありません。署名付きリンクを取得する必要がある場合は、いつでもSDKのインターフェースを呼び出して生成することができます。

### COSの署名付きURLをカスタムドメイン名のURLにするにはどうすればよいですか。

署名付きURLのメソッドは固定されたデフォルトのドメイン名となります。ご自身でエンコードを行って切り替える必要があります。

### COS SDKでディレクトリを作成するにはどうすればよいですか。

COSのディレクトリは仮想ディレクトリであり、実際には / で終わる1つのオブジェクトです。オブジェクトアップロードインターフェースを呼び出し、 / で終わるオブジェクトキーを作成してディレクトリとすることができます。[ミニプログラムSDKによるディレクトリ作成の例](https://intl.cloud.tencent.com/document/product/436/32457)をご参照ください。

### COS SDKを使用してObjectListを取得すると、プレフィックスルールとデータ構造が同じでも異なる結果が返されてしまいます。

COSはユーザーの使用上の習慣に沿って、**コンソール、COSbrowser**などのグラフィックツールで「フォルダ」または「ディレクトリ」という表示方法を疑似的に再現しています。具体的には、キー値がproject/、内容が空のオブジェクトを作成することで、従来のフォルダを模した表示方法を実現します。このため、SDKによって取得するObjectListには、オブジェクト名が「/」で終わる空のオブジェクトが含まれる場合があります。

