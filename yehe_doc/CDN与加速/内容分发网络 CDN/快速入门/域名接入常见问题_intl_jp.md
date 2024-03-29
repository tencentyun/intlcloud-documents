[](id:q1)
### ドメイン名を追加する方法は？
CDNのコンソールでドメイン名を追加できます。詳細については、[ドメイン名のアクセス](https://intl.cloud.tencent.com/document/product/228/5734)をご参照ください。

[](id:q2)
### ドメイン名をCDNに追加するための要件は何ですか？
1. アクセラレーションドメイン名の長さは81文字以下としてください。
2. アクセラレーションリージョンが中国本土、グローバルアクセラレーションの場合、ドメイン名はすでに工業情報化部でICP申告を行っている必要があります。アクセラレーションリージョンが中国本土以外であれば、ドメイン名のICP申告を行う必要はありません。
3. ドメイン名のICP申告同期には遅延が発生します。1～2時間かかる見込みです。ICP申告完了後、1～2時間待ってから、ドメイン名の追加を再試行してください。
4. アンダーバー付きのドメイン名、またはpunycodeに変換された中国語ドメイン名の追加をサポートします。中国語のドメイン名は、あらかじめ中国語の形式でICP申告を行う必要があります。
5. `*.example.com`、`*.a.example.com`などのワイルドカード形式のドメイン名の追加がサポートされます。ワイルドカード形式のドメイン名を追加した後、そのサブドメイン名または第2レベルのワイルドカード形式のドメイン名をその他のアカウントに追加することはできません。例：追加されたワイルドカード形式のドメイン名が`*.example.com`である場合、ユーザーがアクセスするドメイン名`a.example.com`はこのワイルドカード形式のドメイン名とマッチングするため、ワイルドカード形式のドメイン名構成に従ってアクセラレーションが適用されます。ユーザーがアクセスするドメイン名`example.com`がワイルドカード形式のドメイン名とマッチングしないため、アクセラレーション効果はありません。
6. 同じアカウントでは、複数のネストされたドメイン名を追加できます。例えば、`*.example.com`、`*.path.example.com`、`a.path.example.com`は、同じアカウントで同時に追加できます。ドメイン名の設定、アクセストラフィックの統計は優先度別に統計できます。一致性が高いほど、優先度が高くなります。たとえば、`a.path.example.com`へのアクセスは、`a.path.example.com`のドメイン名構成が適用されます。`b.path.example.com`へのアクセスは、`*.path.example.com`のドメイン名構成が適用されます。`c.example.com`へのアクセスは、`*.example.com`の構成が適用されます。アクセストラフィックの統計は同様です。
7. 追加する必要のあるワイルドカード形式のドメイン名に含まれるサブドメイン名が、すでにその他のアカウントに追加されている場合、現在のアカウントに追加する前に、対応するアカウントで対応するサブドメイン名を削除する必要があります。例：Aアカウントにドメイン名`a.example.com`が追加されており、Bアカウントに`*.example.com`を追加する必要がある場合は、`*.example.com`にサブドメイン名`a.example.com`が含まれているため、Bアカウントに`*.example.com`を追加する前に、Aアカウントで`a.example.com`を削除する必要があります。

[](id:q3)
### CDNはワイルドカード形式のドメイン名の追加をサポートしますか？
CDNは現在、ワイルドカード形式のドメイン名の追加をサポートしていますが、ドメイン名所有権の確認を行う必要があります。確認に成功した後、ドメイン名を追加またはドメイン名を取得することができます。
その他：
1. ワイルドカード形式のドメイン名（例：`*.test.com`）がTencent Cloudにすでに追加されている場合、そのワイルドカード形式のドメイン名に含まれるサブドメイン名はいずれも、他のアカウントに追加できません。
2. ワイルドカード形式のドメイン名`*.test.com`がすでに追加されている場合、現在のアカウントにおいてのみ、`*.path.test.com`などのワイルドカード形式のドメイン名を追加できます。
3. アカウントの下に同時に複数のネストされたドメイン名がある場合（`*.test.com`、`*.path.test.com`、`a.path.test.com`）、ドメイン名の構成と統計は、一致性の高いものから低いもの順に適用されます。たとえば、`a.path.test.com`リクエストは`a.path.test.com`ドメイン名のリクエストとして扱われ、`b.path.test.com`リクエストは`*.path.test.com`ドメイン名のリクエストとして扱われます。


### VODドメイン名を追加できない旨のメッセージが出力された場合、どうすればよいですか？
ご利用中のドメイン名がすでにVODのカスタムデリバリーアクセラレーションドメイン名に追加されています。同じアクセラレーションドメイン名を繰り返して設定できないため、CDNコンソールでもこのアクセラレーションドメイン名を使用する必要がある場合は、先にVODからアクセラレーションドメイン名を削除してください（非アクティブ化のみを行っても競合が発生するため、ドメイン名を無効化してから削除してください）。削除して約1分間待ってから、CDNコンソールに追加します。または、異なるサブドメイン名でCDNコンソールに追加することもできます。

[](id:q4)
### CDNの構成にはどれくらい時間がかかりますか？
通常、CDNの構成は5分以内に有効になります。一部の構成は、実行するタスク数が多いため、有効になるまで5～15分かかります。構成が完了するまでしばらくお待ちください。

[](id:q5)
###オリジンサーバーIPは複数設定できますか？
複数のオリジンサーバーIPを設定できます。複数のIPを設定している場合、CDNはBack-to-Originリクエストを受信したときに、入力したIPの任意1つにランダムにアクセスします。あるIPのBack-to-Origin失敗回数がしきい値を超えた場合、デフォルトで当該IPは300秒間隔離され、オリジンサーバーにBack-to-Originしなくなります。

[](id:q6)
###ドメイン名がCDNに追加された後、CNAMEをバインディングするにはどうすればよいですか？
[CNAMEの設定](https://www.tencentcloud.com/document/product/228/3121)ドキュメントに記載されている操作説明を参照し、DNSプロバイダーでCNAMEをバインディングしてください。

[](id:q13)
### CDNがサポートしているサービスタイプはどのようなものがあるでしょうか？
サービスタイプの選択によって、ドメイン名のスケジューリングのためのリソースプラットフォームが決まります。リソースプラットフォームによってアクセラレーション構成に違いがあります。お客様のビジネスにマッチしたサービスタイプを選択してください。
- 小容量Webページファイル：eコマース、ウェブサイト、UGCコミュニティなど、小容量の静的リソース（たとえば、ホームページのスタイル、画像および小容量ファイル）を主とするサービスシーンに適しています。
- 大容量ファイルのダウンロード：ゲームのインストールパッケージ、アプリケーションの更新、アプリケーションパッケージのダウンロードなど、比較的ファイル容量が大きいサービスシーンに適しています。
- オーディオ/ビデオ・オン・デマンド：オーディオとビデオのオンライン・オンデマンドなど、オーディオ/ビデオファイルのオンデマンドアクセラレーションサービスシーンに適しています。
- 動的・静的アクセラレーション：各種Webサイトのトップページなど、動的・静的データが組み合わさったサービスシーンに適しています。
- 動的アクセラレーション：アカウントのログイン、注文取引、APIの呼び出し、リアルタイム照会などのシーンに適しています。


### CDNアクセラレーション後、リソースが古い、コンテンツが更新されていない、またはコンテンツが間違っているなどの例外が発生します。
CDNノードは、[ノードのキャッシュの有効期限設定](https://intl.cloud.tencent.com/document/product/228/38424)に従ってリソースをキャッシュします。CDNノードのキャッシュが有効期限内であれば、オリジンサーバーに戻ってリソースを更新することはありません。
オリジンサーバーのリソースを更新した直後に、CDNノードのキャッシュを直ちに更新する必要がある場合、[キャッシュを更新](https://console.cloud.tencent.com/cdn/refresh)機能を使用し、CDNノードで未期限切れのキャッシュを自主的に更新することで、CDNノードのキャッシュをオリジンサーバーのリソースと一致させることができます。

[](id:q14)

### CDNドメイン名の所属プロジェクトを変更するにはどうすればよいですか？

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側メニューバーの【ドメイン名管理】を選択して、ドメイン名または操作バーの【管理】をクリックします。Tabの【基本設定】ページで、所属プロジェクトを変更できます。複数のドメイン名の所属プロジェクトを変更する場合は、【ドメイン名管理】ページで複数のドメイン名を選択し、上の【その他の操作】で【プロジェクトの編集】を選択することで、複数のドメイン名の所属プロジェクトを同時に変更できます（1回につき最大50件のドメイン名を選択可能）。

>!CDNの権限システムを使用しているユーザーの場合は、この操作によりサブユーザーの権限が変更される可能性がありますので、注意して操作してください。


[](id:m1)
### ドメイン名を工業情報化部にてICP申告を行っているにもかかわらず、CDNアクセラレーションドメイン名に追加するとドメイン名がICP未申告と表示されます。なぜですか？
ICP申告完了後、通常、工業情報化部の情報が同期され、Tencent Cloud CDNでICP申告情報が更新されるまでには、ある程度の時間を要します。24時間待ってから再試行してください。

[](id:q16)
### アクセラレーションドメイン名/オリジンサーバーではポート設定をサポートしていますか？
- アクセラレーションドメイン名ポート：現在CDNアクセラレーションのポートは、デフォルトで80、443、8080の3つをサポートしています。その他のポートは現在サポートしていません。
- オリジンサーバーポート：オリジンサーバーアドレスの後のポート設定に対応しています。ポート（1 - 65535）を設定可能です。

[](id:q17)
### CDN Back-to-Origin HOST設定とは何ですか？
Back-to-Origin HOSTは、CDNノードがBack-to-Originの処理中に統合され、オリジンサーバーでアクセスするサイトのドメイン名を指します。オリジンサーバーで設定したIP/ドメイン名は、Back-to-Originの際にCDNノードを対応するオリジンサーバーにポイントするように指示することができます。オリジンサーバーに複数のWebサイトをデプロイしている場合、Back-to-Origin HOSTの設定により、特定のサイトドメインにアクセスするように指定することができます。オリジンサーバーにサイトが1つしかない場合、デフォルトではBack-to-Origin HOSTを変更する必要がなく、サイトをアクセラレーションドメインとして設定するだけです。
オリジンサーバーがCOSソースまたはサードパーティーのオブジェクトストレージである場合、Back-to-Origin HOSTは変更できず、デフォルトでBack-to-Originアドレスとなります。

[](id:q18)
### CDNが有効になっているかどうかをどのように判断しますか？

1. コンソールのドメイン名管理リストで確認できます。ドメイン名のCNAME解決が正しく行われていれば、現在CDNドメイン名のアクセラレーションが有効になっていることを意味します。CNAME解決が2つ存在する場合は、そのうちの1つだけが有効になっていれば十分です。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XPtc239_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224145315.png)
2. nslookupまたはdigコマンドを使用して、現在ドメイン名の解決ステータスを確認することもできます。
	- Windows OSをご利用の場合、cmdを開いてプログラムを実行します。たとえばドメイン名が`www.test.com`の場合、cmdで`nslookup -qt=cname www.test.com`を実行します。実行結果では、当該ドメイン名のCNAME情報が表示されます。Tencent Cloud CDNによって提供されたCNAMEアドレスと一致する場合、現在CDNアクセラレーションが有効になっていることを意味します。
	![](https://qcloudimg.tencent-cloud.cn/raw/5e862065b78633043f7cf1da228f6554.png)
	- macOSまたはlinuxをご利用の場合、digコマンドを使用して確認できます。たとえばドメイン名が`www.test.com`の場合、端末で`dig www.test.com`コマンドを実行します。実行結果では、当該ドメイン名のCNAME情報が表示されます。Tencent Cloud CDNによって提供されたCNAMEアドレスと一致する場合、現在CDNアクセラレーションが有効になっていることを意味します。
	![](https://qcloudimg.tencent-cloud.cn/raw/0c1b07cd489d05f450297983df191d50.png)

[](id:q19)
### CDNファイルをダウンロードできません

ファイルをダウンロードできない場合は、次のいくつかの方法で解決することを推奨します：
1. オリジンサーバーが正常にダウンロードできるかを確認します。
2. CDNドメイン名が正しく設定されているかを確認します。CDNコンソール > 基本設定 > Back-to-Origin Hostの順に確認し、設定したBack-to-Origin Hostドメイン名がアクセスできる状態になっていることを確認してください。そうなっていない場合、Back-to-Originが失敗し、お客様のサービスに影響します。
3. オリジンサーバーのセキュリティポリシーを確認します。オリジンサーバーで構成されているセキュリティポリシーが、Back-to-Originの失敗を引き起こした原因であるかを確認します。そうである場合、CDN Back-to-Origin IPネットワークセグメントを取得した後、オリジンサーバーでホワイトリストに追加します。

[](id:q20)
### wordpressでCDNのアクセラレーションを設定した後、バックグラウンドでログインできません。
WordPressはログイン（バックグラウンドでディレクトリ/wp-adminにログイン）、インターフェースなどの動的リクエストを伴います。キャッシュ設定が適切に行われていない場合、ログイン異常が発生します。対応する動的ファイルタイプのキャッシュ時間を「キャッシュなし」に設定することをお勧めします。


### オリジンサーバーの構成中に、Back-to-Originプロトコルが正しくないか、ポート番号が正しくないというメッセージが表示されます。

Tencent Cloud CDNのオリジンサーバーの構成では、ポート番号のカスタムをサポートします。Back-to-OriginプロトコルとしてHTTPが選択されている場合、デフォルトのBack-to-Originポートはポート80です。Back-to-OriginプロトコルとしてHTTPSが選択されている場合、デフォルトのBack-to-Originポートはポート443です。カスタムポートを設定している場合、Back-to-Originポートとしてカスタムポートが使用されます。そのため、Back-to-Originが確実に行われるようにするには、オリジンサーバーの構成中に正しいBack-to-Originプロトコルとポート番号を使用する必要があります。よくある構成エラーは次のとおりです：
1. Back-to-OriginプロトコルとしてHTTPが選択されていますが、オリジンサーバーではHTTPSしかサポートしていないため、Back-to-Originに失敗します。
2. Back-to-OriginプロトコルとしてHTTPが選択され、カスタムポートが443になっています。しかし、実際にはオリジンサーバーのBack-to-OriginプロトコルがHTTPSであり、Back-to-OriginプロトコルをHTTPSに変更する必要があります。
3. Back-to-OriginプロトコルとしてHTTP が選択され、カスタムポート番号が8080に変更されています。しかし、実際にオリジンサーバーではポート8080が遮断されています。ポートが通信できない状態のため、Back-to-Originに失敗します。

Back-to-Originプロトコルが正しく選択されているにもかかわらず、ポート80または443が通信できないというメッセージが表示された場合、ソースが正しいポート番号で返されるようにBack-to-Originポートをカスタマイズしてください。オリジンサーバーの情報を入力すると、プラットフォームではオリジンサーバーのポートが通信可能かどうかを自動的に検知します。お客様はプロンプトに従って、現在のBack-to-Originプロトコルまたはポート番号が正しいかどうかを確認することができます。これにより、正常な通信を確保し、Back-to-Origin失敗を回避することができます。

### CDNはtopドメイン名をサポートしていませんか？
現在CDNは、.pwおよび.topドメイン名の追加をすでにサポートしています。


### Tencent Cloud CDNは中国語のドメイン名をサポートしていますか？
現在CDNは、アンダーバー付きのドメイン名、およびpunycodeに変換された中国語ドメイン名の追加をすべてサポートています。
- 中国語ドメイン名は、まず中国語の形式でICP申告を行う必要があります。
- 「中文.域名」などの中国語ドメイン名はホワイトリストに追加された後、サードパーティ製ツールを使用して、「xn--fiq228c.xn--eqrt2g」に変換して追加できます。
- 「test_qq.tencent.cloud」などのアンダーバー付きドメイン名は、直接追加できます。


### CDN管理で追加されたドメイン名をオフにすると、CDNノード上のファイルはどうなりますか？
現在CDNに追加されているドメイン名のアクセラレーションサービスをオフにすると、CDNノードはドメイン名に対応するアクセス構成を保持しますが、CDNトラフィックは発生しなくなります。同時に当該ドメイン名にもアクセスできなくなります。


### 新しく追加されたドメイン名について、「サブアカウントでcamポリシーが構成されていません」というエラーが表示されます
サブアカウントでドメイン名の追加やデータの照会などの操作を実行する際に、ルートアカウントがサブアカウントに対して承認を行っていない場合、「サブアカウントでcamポリシーが構成されていません」というメッセージが表示されます。ルートアカウントは、[Cloud Access Management-ポリシー](https://console.cloud.tencent.com/cam/policy/createV3)でCDN関連のサービスポリシーを作成し、サブアカウントを承認できます。承認後、[Cloud Access Management-ユーザー-ユーザーリスト](https://console.cloud.tencent.com/cam)でサブアカウントの権限を表示できます。

### アクセラレーションドメイン名をオフにする/削除する方法とは何ですか？ドメイン名をオフにした/削除した後、その構成は保持されますか？
アクセラレーションをオフにする必要がある場合は、CDNコンソールでアクセラレーションサービスをオフにすることができます。アクセラレーションドメイン名をオフにした後、削除することができます。詳細については、[ドメイン名の操作](https://intl.cloud.tencent.com/document/product/228/5736)をご参照ください。アクセラレーションドメイン名をオフにした後に削除できない場合、ドメイン名が現在オフ処理を実行しているか、お客様は現在協力者アカウントを利用している可能性があります。協力者アカウントの操作権限は、CDNサービスの作成者のルートアカウントによって作成され設定されます。操作を実行するには、当該ドメイン名に対する削除権限が付与されている必要があります。
ドメイン名をオフにすると、現在の構成リソースは保持されますが、アクセラレーションサービスは提供されなくなります。ユーザーのリクエストに対しては404のエラーコードが返されます。ドメイン名を削除すると、その構成は直ちに削除され、復元できなくなります。

### example.com、www.example.com、m.example.comに対して同時にCDNアクセラレーション効果を適用するにはどうすればいいですか?

1. `example.com`、`www.example.com`、`m.example.com`が異なるドメイン名に属しているため、CDNアクセラレーション効果を適用するには、それぞれをCDNに追加する必要があります。ドメイン名の構成が同じ場合は、ドメイン名を一括追加するか、ドメイン名の構成をコピーして追加することができます。
2. ドメイン名が同じリソースにアクセスする場合（たとえば、`example.com`と`www.example.com`が同じリソースにアクセスする場合）、ドメイン名解決サービスプロバイダ経由で、内部転送、または外部転送による301リダイレクトを設定することで、すでにCDNアクセラレーションが適用されているドメイン名にポイントできます。詳細については、[内部転送、外部転送の履歴設定](https://docs.dnspod.cn/dns/help-redirect-url/)をご参照ください。

### CDNはwebsocket接続をサポートしますか？
ECDN動的・静的アクセラレーションまたはECDN動的アクセラレーションを使用することをお勧めします。高度な構成でwebsocket接続のタイムアウト構成を有効にすることができます。許容される最大値は300秒です。アクセラレーションの種類がCDN小容量Webページファイル、CDN大容量ファイルのダウンロード、CDNオーディオ/ビデオ・オン・デマンドの場合、websocket接続を使用すると、接続が切断したり、失敗したりする可能性があります。
