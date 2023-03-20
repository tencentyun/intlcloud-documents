Cloud Object Storage（COS）は主に次の機能を提供します。

## 操作

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td nowrap="nowrap">バケット操作</td>
      <td>バケットの作成、照会、削除、クリアをサポートしています。具体的な操作については <a href="https://intl.cloud.tencent.com/document/product/436/13309">バケット管理</a>ディレクトリ下のドキュメントをご参照ください。</td>
   </tr>
   <tr>
      <td>オブジェクト操作</td>
      <td>複数のストレージタイプ：アクセス頻度と障害復旧のレベルに応じて、COSは、複数のオブジェクトストレージタイプを提供しており、その中には標準ストレージ（マルチAZ）、低頻度ストレージ（マルチAZ）、INTELLIGENT_TIERINGストレージ、標準ストレージ、低頻度ストレージ、アーカイブストレージ、ディープアーカイブストレージがあります。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/30925">ストレージタイプ</a>をご参照ください<br>オブジェクト/フォルダ：アップロード、照会、ダウンロード、コピー、削除操作。具体的な操作については<a href="https://intl.cloud.tencent.com/document/product/436/13321">オブジェクト管理</a>ディレクトリ下のドキュメントをご参照ください。
   </tr>
</table>	 

## データ管理

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>ライフサイクル</td>
      <td>COSはオブジェクトに対するライフサイクルルールの設定をサポートしており、指定したオブジェクトに対し、定期的に自動的に削除またはストレージタイプの変更を行うことができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/17028">ライフサイクルの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>静的ウェブサイト</td>
      <td>バケットを静的ウェブサイトのホスティングモードに設定し、バケットドメイン名によってその静的ウェブサイトにアクセスできるようにします。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/30958">静的ウェブサイトホスティング</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>リスト</td>
      <td>COSはユーザーのリストに基づいてタスクを設定し、毎日または毎週一定の時刻にユーザーのバケット内の指定されたオブジェクトまたは同一のオブジェクトプレフィックスをもつオブジェクトのスキャンを行い、リストレポートを出力して、CSV形式のファイルをユーザーが指定したバケットに保存することができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/30622">リスト機能の概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td nowrap="nowrap">バケットタグ</td>
      <td>バケットタグはバケットを管理する標識として、ユーザーがバケットのグループ化管理を行う際に便利に使用できます。ユーザーは指定したバケットに対し、タグの設定、照会および削除操作を行うことができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/31509">バケットタグの概要</a>をご参照ください</td>
   </tr>
   <tr>
      <td>イベント通知</td>
      <td>COSはSCF（Serverless Cloud Function）と組み合わせることで、COSリソースに変動（新規ファイルのアップロード、ファイルの削除など）があった場合に、ユーザーが速やかに通知メッセージを受信できるようにします。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/31648">イベント通知</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>データ検索</td>
      <td>COS Select機能は、COS上に保存されたオブジェクトを構造化問い合わせ言語（SQL）によってフィルタリングすることで、オブジェクトを検索してユーザーが必要とするデータを取得するために役立てるものです。COS Select機能によってオブジェクトデータをフィルタリングすることで、ユーザーはCOSの転送データ量を削減することができ、そのデータの検索に必要なコストと遅延を減少させることができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/32472">Selectの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>ログ管理</td>
      <td>ログ管理機能は、指定したソースバケットへの詳細なアクセス情報を記録し、これらの情報をログファイル形式で指定のバケットに保存することで、バケットのより適切な管理を実現するものです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/16920">ログ管理の概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>オブジェクトタグ</td>
      <td>オブジェクトタグ機能は、オブジェクトにキーバリューペア形式の標識を追加することで、ユーザーがバケット内のオブジェクトをグループ化管理しやすくするものです。オブジェクトタグはタグのキー（tagKey）とタグの値（tagValue）を=でつないだ構成となっています（例：group = IT）。ユーザーは指定したオブジェクトに対しタグの設定、照会、削除操作を行うことができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/35665">オブジェクトタグの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>ストレージゲートウェイ</td>
      <td>ストレージゲートウェイはTencent Cloudがご提供するハイブリッドクラウドストレージサービスです。バケットにストレージゲートウェイを設定することを選択でき、設定が完了すると、COS内のバケットをネットワークフォルダの形で任意のCVMサーバーにマウントし、ストレージデバイスとして使用することができるようになります。</td>
   </tr>
</table>

## 異なるリージョン間の障害復旧

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>バージョニング</td>
      <td>バージョニングは同一のバケット内に同一のオブジェクトの複数のバージョンを保存する場合に使用します。ユーザーがあるバケットでバージョニング機能を有効にすると、バケット内に保存したオブジェクトをバージョンIDに基づいて検索、削除または復元できるようになります。ユーザーが誤って削除したデータや、アプリケーションプログラムの障害によって消失したデータの回復に役立ちます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/19883">バージョニングの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td nowrap="nowrap">バケットコピー</td>
      <td>ユーザーはバケットコピールールを設定することで、インクリメンタルオブジェクトを異なるバケットに自動的かつ非同期的にコピーし、データの障害復旧とバックアップを実現することができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/19237">バケットコピーの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td nowrap="nowrap">マルチAZの特性</td>
      <td>COSはマルチAZストレージアーキテクチャをご提供しています。このストレージアーキテクチャはユーザーデータにデータセンターレベルの障害復旧機能を提供することが可能です。詳細については<a href="https://intl.cloud.tencent.com/document/product/436/35208">マルチAZの特徴の概要</a>をご参照ください。</td>
   </tr>
</table>


## Data Security

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>暗号化</td>
      <td>COSはデータをデータセンター内のディスクに書き込む前に、オブジェクトレベルでアプリケーションデータを暗号化する保護ポリシーをサポートしています。データはアクセス時に自動的に復号されます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/18145">サーバー側の暗号化の概要</a>および<a href="https://intl.cloud.tencent.com/document/product/436/33457">バケットの暗号化の概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>リンク不正アクセス防止</td>
      <td>COSはリンク不正アクセス防止設定をサポートしています。ユーザーはコンソールのリンク不正アクセス防止機能によって、ブラックリスト/ホワイトリストを設定し、データリソースのセキュリティ保護を行うことができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/32466">リンク不正アクセス防止の実践</a>をご参照ください。</td>
   </tr>
</table>

## Cloud Access Management

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>クロスドメインアクセス</td>
      <td>COSはHTML5標準のクロスドメインアクセス設定を提供し、クロスドメインアクセスの実現を支援します。クロスドメインアクセスについて、COSはOPTIONSリクエストへのレスポンスをサポートし、開発者が設定したルールに基づいて、具体的な設定ルールをブラウザに返します。具体的な操作については <a href="https://intl.cloud.tencent.com/document/product/436/13318">クロスドメインアクセスの設定</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>back-to-origin機能</td>
      <td>バケットにback-to-originルールを設定すると、ユーザーがリクエストしたオブジェクトがバケット内にない場合、または特定のリクエストに対しリダイレクトを行う必要がある場合に、ユーザーはback-to-originルールによってCOSから対応するデータにアクセスすることができます。具体的な操作については <a href="https://intl.cloud.tencent.com/document/product/436/31508">back-to-originの設定</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>バケットポリシー</td>
      <td>ユーザーはバケットにポリシーを追加し、特定のアカウント、特定のリソースIP（またはIPセグメント）によるCOSリソースへのアクセスを許可または禁止することができます。具体的な操作については <a href="https://intl.cloud.tencent.com/document/product/436/30927">バケットポリシーの追加</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>アクセス制御</td>
      <td>ユーザーはバケットとオブジェクトへのアクセス権限を管理することができます。特定のリソースのリクエストを受信した際に、対応するACLをCOSがチェックし、リクエスト送信者が必要なアクセス権限を持っているかどうかを検証します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/30581">アクセス制御の基本概念</a>および<a href="https://intl.cloud.tencent.com/document/product/436/11714">サブアカウントのCOSアクセス権限承認</a>をご参照ください。</td>
   </tr>
</table>

## アクセス速度

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>CDNアクセラレーション</td>
      <td>COSはCDNアクセラレーションサービスと組み合わせることで、バケット内のコンテンツを広範囲にダウンロード、配信することができます。特に、同一のコンテンツを繰り返しダウンロードするユースケースに適しています。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/18669">CDNアクセラレーションの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>グローバルアクセラレーション</td>
      <td>Tencent Cloud COSのグローバルアクセラレーション機能により、世界各地のユーザーがお客様のバケットにスピーディーにアクセスしやすくなり、ビジネスのアクセス成功率が向上することで、ビジネスの安定とビジネス体験向上がさらに保障されます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/33409">グローバルアクセラレーションの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>単一リンクの速度制限</td>
      <td>COSはファイルのアップロード、ダウンロード時のトラフィック制御をサポートすることで、他のアプリケーションのネットワーク帯域幅を保証することができます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/34072">単一リンクの速度制限</a>をご参照ください。</td>
   </tr>
</table>

## バッチ作業

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td nowrap="nowrap">バッチ処理</td>
      <td>ユーザーはバケット内のオブジェクトリストを指定して、指定の操作を実行することができます。具体的な操作は、リスト機能によって生成したオブジェクトリストを指定のオブジェクトリストとするか、または処理したいオブジェクトをリストファイルの形式で、CSV形式のファイルに記録し、COSのバッチ処理機能によってこれらのオブジェクトリストファイルに対しバッチ処理を行います。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/32958">バッチ処理の概要</a>をご参照ください。</td>
   </tr>
</table>

## データ監視

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>監視とアラート</td>
      <td>COSの読み取り/書き込みリクエスト量、トラフィックなどのデータは <a href="https://www.tencentcloud.com/document/product/248">Cloud Monitor</a>によって集計され、表示されます。ユーザーはCMの<a href="https://console.cloud.tencent.com/monitor/product/COS">コンソール</a>上で、COSの読み取り/書き込みリクエスト量、トラフィックなどの詳細な監視データを確認することができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/31649">監視とアラート</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>データ概要の確認</td>
      <td>COSはストレージデータの監視機能を提供しています。データウィンドウの監視を通じて、時間帯ごとに異なるストレージタイプのデータ量および傾向を照会することができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/36542">データ概要の確認</a>および<a href="https://intl.cloud.tencent.com/document/product/436/31634">監視データの照会</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>監視アラートの設定</td>
      <td>Cloud Monitor（CM）のアラートポリシーによってCOS監視指標のアラート閾値を設定できます。アラートポリシーには、名称、ポリシータイプ、アラートのトリガー条件、アラートオブジェクト、アラート通知テンプレートという5つの必要構成部分が含まれます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/39104">監視アラートの設定</a>をご参照ください。</td>
   </tr>
</table>

## Data Processing

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td nowrap="nowrap">画像処理</td>
      <td>COSはCloud Infinite（CI）のプロフェッショナルな一体化メディアソリューションを統合し、画像処理、審査、認識などの機能をすべてカバーします。COSのアップロードおよび処理インターフェースを通じて、メディアデータの処理操作を行うことができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/35280">画像処理の概要</a>をご参照ください。また、画像の高度圧縮およびブラインドウォーターマーク機能もサポートしていますので、詳細については <a href="https://intl.cloud.tencent.com/document/product/436/40115">画像の高度圧縮の概要</a>および<a href="https://intl.cloud.tencent.com/document/product/436/46325">ブラインドウォーターマークの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>Media Processing Service</td>
      <td>Media Processing Service（MPS）は、COSがCloud Infiniteをベースにしてリリースした、マルチメディアファイル処理サービスです。オーディオビデオトランスコーディング、ビデオフレームキャプチャ、オーディオビデオスプライシング、ビデオアニメーション画像生成、ビデオメタ情報の取得などのVideo Cloudサービス、さらにTencent Cloudの先進的なAIテクノロジーとの組み合わせをカバーした、インテリジェントカバーの高度な処理サービスです。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/48303">MPSの概要</a>および<a href="https://intl.cloud.tencent.com/document/product/436/46387">データワークフローの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>ファイル処理</td>
      <td>ファイル処理はCOSがCloud Infiniteをベースにしてリリースした、すべての形式のファイルを対象とした処理サービスです。現在はファイルのハッシュ値計算、ファイル解凍および複数ファイルのパッケージ化圧縮機能を提供しています。</td>
   </tr>
   <tr>
      <td>ドキュメントプレビュー</td>
      <td>ドキュメントプレビューサービスは、Tencent Cloud Infiniteをベースにしており、この機能を有効化すると、バケット内のドキュメントタイプのファイルをダウンロードすることなく、オンラインプレビューすることができるため、ドキュメントコンテンツのページの表示の問題を解決することができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/49159">ドキュメントプレビューの概要</a>をご参照ください。</td>
   </tr>
   <tr>
      <td>スマート音声</td>
      <td>スマート音声サービスはTencent Cloud Infiniteをベースにしたもので、有効化すると、音声合成、音声認識、オーディオノイズリダクションなどの操作を行うことができます。</td>
   </tr>

   <tr>
      <td>関数計算</td>
      <td>COSは指定のバケットに対するファイル解凍およびCDNキャッシュ更新の設定をサポートしています。</td>
   </tr>
	 
	 
</table>

## データ審査

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>コンテンツ審査</td>
      <td>COSコンテンツ審査サービスは、画像、ビデオ、音声、テキスト、ドキュメント、ウェブページなどのマルチメディアのコンテンツセキュリティのインテリジェント審査を提供するサービスです。ユーザーが、ポルノ・低俗、暴力・テロ、違法・不正、不快感を与えるなどの禁止コンテンツを効果的に識別し、運営リスクを回避できるようにサポートします。</td>
   </tr>
</table>

## アプリケーション統合

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td nowrap="nowrap">他のクラウド製品との統合</td>
      <td>COSはServerless Cloud Function（SCF）をベースにして、データベースバックアップ、メッセージバックアップ、ログバックアップ、ログ分析、ファイル解凍、データエクスポートなどの機能をユーザーにご提供します。詳細については、<a href="https://www.tencentcloud.com/document/product/436/39924">アプリケーション統合</a>をご参照ください。</td>
   </tr>
</table>

## ツール

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td nowrap="nowrap">様々な管理ツール/td>
      <td>COSはCOSBrowser、COSCMD、COSCLI、COS Migrationなどのさまざまな実用的なツールを提供し、ユーザーがデータ管理やデータ移行を便利に行えるようにしています。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/6242">ツールの概要</a>をご参照ください。</td>
   </tr>
</table>

## API/SDK

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td nowrap="nowrap">様々なAPIおよびSDK</td>
      <td><ul  style="margin: 0;"><li>API：COSは、機能インターフェースの使用方法およびパラメータを含む、豊富なAPIインターフェースを提供しており、リクエストのサンプル、レスポンスのサンプル、エラーコードの説明などを利用することができます。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/10111">操作リスト</a>をご参照ください。</li><li>COSは、Android、C、C++、.NET、Go、iOS、Java、JavaScript、Node.js、PHP、Python、ミニプログラムSDKといったさまざまな開発言語を提供しています。詳細については <a href="https://intl.cloud.tencent.com/document/product/436/6474">SDKの概要</a>をご参照ください。</li></ul></td>
   </tr>
</table>

## プロトコルをサポート

<table>
   <tr>
      <th style="width: 18%;">機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td>複数の伝送プロトコル</td>
      <td>COSはHTTP1.0、HTTP1.1プロトコルを含む複数の伝送プロトコルをサポートしています。またTLS1.0、TLS1.1、TLS1.2暗号化プロトコルもサポートしています。</td>
   </tr>
</table>


