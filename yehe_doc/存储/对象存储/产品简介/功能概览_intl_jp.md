COSは主に次の機能を提供します。

<table>
   <tr>
      <th colspan=2>機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td rowspan=2>操作</td>
      <td nowrap="nowrap">バケット操作</td>
      <td>バケットの作成、照会、削除、クリアをサポートしています。具体的な操作については <a href="https://intl.cloud.tencent.com/document/product/436/13309">バケット管理</a>ディレクトリ下のドキュメントをご参照ください</td>
   </tr>
   <tr>
      <td>オブジェクト操作</td>
      <td>複数のストレージタイプ：アクセス頻度に応じて、COSは複数のオブジェクトストレージタイプを提供しており、その中にはINTELLIGENT_TIERINGストレージ、標準ストレージ、低頻度ストレージ、アーカイブストレージ、ディープアーカイブストレージがあります。詳細については<a href="https://intl.cloud.tencent.com/document/product/436/30925">ストレージタイプ</a>をご参照ください<br>オブジェクト/フォルダ：アップロード、照会、ダウンロード、コピー、削除操作。具体的な操作については、<a href="https://intl.cloud.tencent.com/document/product/436/13321">オブジェクト管理</a>ディレクトリ下のドキュメントをご参照ください</td>
   </tr>
   <tr>
      <td rowspan=8>データ管理</td>
      <td>ライフサイクル</td>
      <td>COSはユーザー設定ルールをサポートし、指定したオブジェクトに対し、ある時間（日数）が経過した後に自動的に削除またはストレージタイプの変更を行うことができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/17028">ライフサイクルの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>静的ウェブサイト</td>
      <td>バケットを静的ウェブサイトのホスティングモードに設定し、バケットドメイン名によってその静的ウェブサイトにアクセスできるようにします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/30958">静的ウェブサイトホスティング</a>をご参照ください</td>
   </tr>
   <tr>
      <td>リスト</td>
      <td>COSはユーザーのリストに基づいてタスクを設定し、毎日または毎週一定の時刻にバケット内のユーザーが指定したオブジェクトまたは同一のオブジェクトプレフィックスを持つオブジェクトのスキャンを行い、インベントリレポートを出力して、CSV形式のファイルをユーザーが指定したバケットに保存することができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/30622">リスト機能の概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td nowrap="nowrap">バケットタグ</td>
      <td>バケットタグはバケットを管理する標識として、ユーザーがバケットのグループ化管理を行う際に便利に使用できます。ユーザーは指定したバケットに対しタグの設定、照会および削除操作を行うことができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/31509">バケットタグの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>イベント通知</td>
      <td>COSはSCF（Serverless Cloud Function）と組み合わせて、COSリソースに変動（新規ファイルのアップロード、ファイルの削除など）があった場合にユーザーが速やかにメッセージ通知を受信できるようにすることができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/31648">イベント通知</a>をご参照ください</td>
   </tr>
   <tr>
      <td>データ検索</td>
      <td>COS Select機能は、COS上に保存されたオブジェクトを構造化問い合わせ言語（SQL）によってフィルタリングすることで、オブジェクトを検索してユーザーが必要とするデータを取得するために役立てるものです。COS Select機能によってオブジェクトデータをフィルタリングすることで、ユーザーはCOSの転送データ量を削減することができ、そのデータの検索に必要なコストと遅延を減少させることができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/32472">Selectの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>ログ管理</td>
      <td>ログ管理機能は、指定したソースバケットへの詳細なアクセス情報を記録し、これらの情報をログファイル形式で指定のバケットに保存することで、バケットのより適切な管理を実現するものです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/16920">ログ管理の概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>オブジェクトタグ</td>
      <td>オブジェクトタグ機能は、オブジェクトにキーバリューペア形式の標識を追加することで、ユーザーがバケット内のオブジェクトをグループ化管理しやすくするものです。オブジェクトタグはタグのキー（tagKey）とタグの値（tagValue）を=でつないだ構成となっています（例：group = IT）。ユーザーは指定したオブジェクトに対しタグの設定、照会、削除操作を行うことができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/35665">オブジェクトタグの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td rowspan=3>リモートディザスタリカバリ</td>
      <td>バージョニング</td>
      <td>バージョニングは同一のバケット内に同一のオブジェクトの複数のバージョンを保存する場合に使用します。ユーザーがあるバケットでバージョニング機能を有効にすると、バケット内に保存したオブジェクトをバージョンIDに基づいて検索、削除または復元できるようになります。ユーザーが誤って削除したデータや、アプリケーションプログラムの障害によって消失したデータの回復に役立ちます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/19883">バージョニングの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td nowrap="nowrap">バケットコピー</td>
      <td>ユーザーはバケットコピールールを設定することで、増分のオブジェクトを異なるバケットに自動的かつ非同期的にコピーし、データの障害復旧とバックアップを実現することができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/19237">バケットコピーの概要</a>をご参照ください</td>
   </tr>
   <tr>
​     

   <tr>
      <td rowspan=2>データセキュリティ</td>
      <td>暗号化</td>
      <td>COSはデータをデータセンター内のディスクに書き込む前に、オブジェクトレベルでデータの暗号化を適用する保護ポリシーをサポートしています。データはアクセス時に自動的に復号されます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/18145">サーバー側の暗号化の概要</a>および<a href="https://intl.cloud.tencent.com/document/product/436/33457">バケットの暗号化の概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>リンク不正アクセス防止</td>
      <td>COSはリンク不正アクセス防止設定をサポートしています。ユーザーはコンソールのリンク不正アクセス防止機能によってブラックリスト/ホワイトリストを設定し、データリソースのセキュリティ保護を行うことができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/32466">リンク不正アクセス防止の実践</a>をご参照ください</td>
   </tr>
   <tr>
      <td rowspan=4>アクセス管理</td>
      <td>クロスドメインアクセス</td>
      <td>COSはHTML5標準のクロスドメインアクセス設定を提供し、クロスドメインアクセスの実現を支援します。クロスドメインアクセスについて、COSはOPTIONSリクエストへのレスポンスをサポートし、開発者が設定したルールに基づいて、具体的な設定ルールをブラウザに返します。具体的な操作については、<a href="https://intl.cloud.tencent.com/document/product/436/13318">クロスドメインアクセスの設定</a>をご参照ください</td>
   </tr>
   <tr>
      <td>back-to-origin機能</td>
      <td>バケットにback-to-originルールを設定すると、ユーザーがリクエストしたオブジェクトがバケット内にない場合、または特定のリクエストに対しリダイレクトを行う必要がある場合に、back-to-originルールによってCOSから対応するデータにアクセスすることができます。具体的な操作については、<a href="https://intl.cloud.tencent.com/document/product/436/31508">back-to-originの設定</a>をご参照ください</td>
   </tr>
   <tr>
      <td>バケットポリシー</td>
      <td>ユーザーはバケットにポリシーを追加し、特定のアカウント、特定のソースIP（またはIPセグメント）のCOSリソースへのアクセスを許可または禁止することができます。具体的な操作については、<a href="https://intl.cloud.tencent.com/document/product/436/30927">バケットポリシーの追加</a>をご参照ください</td>
   </tr>
   <tr>
      <td>アクセス制御</td>
      <td>ユーザーはバケットとオブジェクトへのアクセス権限を管理することができます。特定のリソースのリクエストを受信した際に、対応するACLをCOSがチェックし、リクエスト送信者が必要なアクセス権限を持っているかどうかを検証します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/30581">アクセス制御の基本概念</a>および<a href="https://intl.cloud.tencent.com/document/product/436/11714">サブアカウントのCOSアクセス権限承認</a>をご参照ください</td>
   </tr>
   <tr>
      <td rowspan=3>アクセス速度</td>
      <td>CDNアクセラレーション</td>
      <td>COSはCDNアクセラレーションと組み合わせることで、バケット内のコンテンツを広範囲にダウンロード、配信することができます。特に、同一のコンテンツを繰り返しダウンロードするユースケースに適しています。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/18669">CDNアクセラレーションの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>グローバルアクセラレーション</td>
      <td>Tencent Cloud COSのグローバルアクセラレーション機能により、世界各地のユーザーがお客様のバケットにスピーディーにアクセスしやすくなり、ビジネスのアクセス成功率が向上することで、ビジネスの安定とビジネス体験向上がさらに保障されます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/33409">グローバルアクセラレーションの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>単一リンクの速度制限</td>
      <td>COSはファイルのアップロード、ダウンロード時のトラフィック制御をサポートすることで、他のアプリケーションのネットワーク帯域幅を保証することができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/34072">単一リンクの速度制限</a>をご参照ください</td>
   </tr>
   <tr>
      <td>バッチ作業</td>
      <td nowrap="nowrap">バッチ処理</td>
      <td>ユーザーはバケット内のオブジェクトリストを指定して、指定の操作を実行することができます。具体的な操作は、リスト機能によって生成したオブジェクトリストを指定のオブジェクトリストとするか、または処理したいオブジェクトをリストファイルの形式で、CSV形式のファイルに記録し、COSのバッチ処理機能によってこれらのオブジェクトリストファイルに対しバッチ処理を行います。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/32958">バッチ処理の概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td rowspan=3>データ監視</td>
      <td>監視とアラート</td>
      <td>COSの読み取り/書き込みリクエスト量、トラフィックなどのデータは<a href="https://intl.cloud.tencent.com/doc/product/248">Basic Cloud Monitor（BCM）</a>によって集計され、表示されます。ユーザーはBCMの<a href="https://console.cloud.tencent.com/monitor/product/COS">コンソール</a>上で、COSの読み取り/書き込みリクエスト量、トラフィックなどの詳細な監視データを確認することができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/31649">監視とアラート</a>をご参照ください</td>
   </tr>
   <tr>
      <td>データ概要の確認</td>
      <td>COSはストレージデータの監視機能を提供しています。データ監視ウィンドウを通じて、時間帯ごとに異なるストレージタイプのデータのデータ量および傾向を照会することができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/36542">データ概要の確認</a>および<a href="https://intl.cloud.tencent.com/document/product/436/31634">監視データの照会</a>をご参照ください</td>
   </tr>
   <tr>
      <td>監視アラートの設定</td>
      <td>Basic Cloud Monitor（BCM）のアラートポリシーによってCOS監視指標のアラート閾値を設定できます。アラートポリシーには、名称、ポリシータイプ、アラートのトリガー条件、アラームオブジェクト、アラート通知テンプレートという5つの必要構成部分が含まれます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/39104">監視アラートの設定</a>をご参照ください</td>
   </tr>
   <tr>
      <td rowspan=3>データ処理</td>
      <td nowrap="nowrap">画像処理</td>
      <td>Tencent Cloud COSはCloud Infinite（CI）のプロフェッショナルな一体化メディアソリューションを統合し、画像の処理、審査、認識などの機能をすべてカバーします。COSのアップロードおよび処理インターフェースを通じてメディアデータの処理操作を行うことができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/35280">画像処理の概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>ファイル解凍</td>
      <td>ファイル解凍機能はTencent Cloud COSがServerless Cloud Function（SCF）をベースにして提供するデータ処理ソリューションです。ファイル解凍機能を追加すると、圧縮ファイルがCOSにアップロードされた時点で、COSがあらかじめ設定したSCFが自動的にトリガーされ、ファイルが自動的に指定のバケットとディレクトリに解凍されます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/35663">ファイル解凍</a>をご参照ください</td>
   </tr>
   <tr>
      <td>CDNキャッシュ更新</td>
      <td>CDNキャッシュ更新はTencent Cloud COSがServerless Cloud Function（SCF）をベースにして提供するデータ更新機能です。ユーザーがCDNエッジノード上のキャッシュデータを自動的に更新する上で役立ちます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/37273">CDNキャッシュ更新</a>をご参照ください</td>
   </tr>
   <tr>
      <td>ツール</td>
      <td nowrap="nowrap">様々な管理ツール/td>
      <td>COSはCOSBrowser、COSCMD、COS Migrationなどの様々な実用的なツールを提供し、ユーザーがデータ管理やデータ移行を便利に行えるようにしています。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/6242">ツールの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>API/SDK</td>
      <td nowrap="nowrap">様々なAPIおよびSDK</td>
      <td>API：COSは、機能インターフェースの使用方法およびパラメータを含む、豊富なAPIインターフェースを提供しており、リクエストのサンプル、レスポンスのサンプル、エラーコードの説明などを利用することができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/10111">操作リスト</a>をご参照ください<br><li>COS は、Android、C、C++、.NET、Go、iOS、Java、JavaScript、Node.js、PHP、Python、ミニプログラムSDKといった様々な開発言語を提供しています。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/6474">SDKの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>サポートプロトコル</td>
      <td nowrap="nowrap">様々な伝送プロトコル/td>
      <td>COSは、HTTP1.0、HTTP1.1、HTTP2.0およびQUICプロトコルを含む複数の伝送プロトコルのほか、TLS1.0、TLS1.1、TLS1.2暗号化プロトコルもサポートします。このうちHTTP2.0とQUICプロトコルは現在ベータ版テスト段階のため、ご利用を希望される場合は、<a href="https://intl.cloud.tencent.com/support">オンラインサポート</a>または<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a>してご連絡いただければ、ホワイトリストをアクティブ化します。</td>
   </tr>
</table>
