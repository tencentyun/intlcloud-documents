このドキュメントでは、TencentDB for MySQLコンソールを介してデータベースエージェントを有効化する方法をご紹介します。

データベースエージェントは、TencentDB for MySQLサービスとアプリケーションサービスの間に位置するネットワークエージェントサービスで、アプリケーションサービスがデータベースにアクセスする際のすべての要求をエージェントします。データベースエージェントは自動読み取り/書き込み分離、トランザクション分割、接続プール、接続保持などの高度な機能を提供し、高可用性、高性能、運用可能、簡単で使いやすいなどの特徴があります。

## 前提条件
- インスタンスのステータスは実行中で、インスタンスは2ノードまたは3ノードのアーキテクチャです。
- インスタンスは、シングルアベイラビリティーゾーンにデプロイされています。

## 注意事項
- データベースエージェントによって現在サポートされているリージョン：
  - 北京（1、2、4区を除く）、上海（1区を除く）、広州（1、2区を除く）、成都、重慶、南京、中国香港（1区を除く）。
  - 東京（1区を除く）、バンコク（1区を除く）、バージニア（1区を除く）、シリコンバレー（1区を除く）、ムンバイ（1区を除く）、ソウル（1区を除く）、シンガポール（1、2区を除く）。
- データベースエージェントが現在サポートするバージョン：2ノード、3ノードのMySQL 5.7（カーネルマイナーバージョンは20211030以降）、2ノード、3ノードのMySQL 8.0（カーネルマイナーバージョンは20211202以降）。マスターインスタンスのカーネルマイナーバージョンのアップデートは、関連する読み取り専用インスタンスとディザスタリカバリインスタンスも同時にアップデートします。[カーネルマイナーバージョンのアップデート](https://intl.cloud.tencent.com/document/product/236/36816)をご参照ください。

## 操作手順
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストで、エージェントの有効化が必要なマスターインスタンスを選択し、インスタンスIDまたは**操作**の列の**管理**をクリックし、インスタンス管理ページに進みます。
2. インスタンス管理ページで、**データベースエージェント**ページを選択し、**今すぐ有効化**をクリックします。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vMSm892_10.png)
3.　ポップアップされたのダイアログボックスで、以下の設定を完了し、**OK**をクリックします。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZUjv978_11.png)
<table>
<thead><tr><th>パラメータ</th><th>説明</th></tr></thead>
<tbody><tr>
<td>ネットワーク</td>
<td>プライベートネットワークVPCのみをサポートするデータベースエージェントのネットワークを選択します。</td></tr>
<tr>
<td>エージェント仕様</td>
<td>2コア4000MBメモリ、4コア8000MBメモリ、8コア16000MBメモリの規格を選択できます。</td></tr>
<tr>
<td>アベイラビリティーゾーンとノードの数</td>
<td>1. データベース・エージェントのアベイラビリティーゾーンを選択します。<strong>新規アベイラビリティーゾーン</strong>をクリックして複数選択できます。選択可能なアベイラビリティーゾーンの数は、現在のリージョンの選択可能なアベイラビリティーゾーンの数に関連し、最大3つのアベイラビリティーゾーンが選択できます。<br>2. 選択するノードの個数：推奨するエージェントノード個数は、マスターインスタンスと読み取り専用インスタンスのCPUコア数合計の1/8（切り上げ）です。例えば、マスターインスタンスが4コアのCPUで、読み取り専用インスタンスが8コアのCPUの場合、推奨するエージェント数＝(4+8)/8 ≒2となります。<blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">注意</div>        <div class="rno-document-tip-desc"><ol><li>選択したデータベースエージェントがマスターインスタンスと同じアベイラビリティーゾーンにない場合、データベースエージェントを介して接続すると書き込みパフォーマンスが低下することがあります。</li><li>推奨するノード数を計算した結果、必要なエージェントノード数が購入制限を超える場合は、より高規格のエージェントを選択することをお勧めします。</li></ol></div>    </div></blockquote></td></tr>
<tr>
<td>セキュリティグループ</td>
<td>デフォルトで選択されたセキュリティグループは、マスターインスタンスと一致しています。必要に応じて、既存のセキュリティグループを選択するか、新しいセキュリティグループを作成することもできます。複数のセキュリティグループをサポートします。<blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">注意</div>        <div class="rno-document-tip-desc"><p>データベースエージェントにアクセスするには、セキュリティポリシーの設定を有効にし、プライベートネットワークアクセスポートをインターネットにオープンする必要があります（現在のプライベートネットワークポートは3306です）。具体的には<a href="https://intl.cloud.tencent.com/document/product/236/14470">MySQLセキュリティグループの設定をご参照ください</a>。</p></div>    </div></blockquote></td></tr>
<tr>
<td>備考</td>
<td>有効にするデータベースエージェントサービスのコメントを記入するための非必須項目です。</td></tr>
</tbody></table>
4.　サービスを有効にすると、データベースエージェントページで基本情報を確認し、エージェントノードを管理し、接続アドレスでデータベースエージェントのアクセスアドレス、ネットワークタイプおよびコメントを変更し、接続アドレス操作項目で接続設定の詳細を確認、設定を調整し、Cloud Load Balancer操作を繰り返します。
>?
>- エージェントノードリストの**接続数**を確認するか、各エージェントノードのパフォーマンス監視を確認することで、各ノードへのアクセスが偏っているかどうかを判断することができます。各エージェントノードへの接続数が偏っている場合、**リロードバランシング**をクリックして接続を分散させることができます。
>- リロードバランシングはエージェントノードの再起動をトリガーし、再起動中は一時的にサービスが利用できなくなります。 オフピーク時にサービスを再起動することをお勧めします。業務に再接続メカニズムが備わっていることを確認してください。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CH3a932_12.png)

