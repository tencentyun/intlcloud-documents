メディアアップロードとは、ビデオ、オーディオ、カバー画像などのメディアファイルをVODのストレージにアップロードし、後続の処理と配信などを実行することをいいます。

## アップロード方法

VODでは次のいくつかのアップロード方法をサポートしています。

- [コンソールからのローカルアップロード](https://console.cloud.tencent.com/vod/media/upload)
VODコンソールのアップロードページで操作して、ローカルメディアファイルをVODにアップロードできます。少量のメディアを直接管理するケースに適しており、簡単かつ迅速、さらに技術的ハードルがないというメリットがあります。
- [コンソールからのプルアップロード](https://console.cloud.tencent.com/vod/media/upload)
VODコンソールのアップロードページで操作して、アップロードするメディアのURLを指定すると、VODバックエンドがファイルをオフラインでプルします。
- [サーバーからのアップロード](https://intl.cloud.tencent.com/document/product/266/33912)
バックエンドサーバーにストレージされたメディアファイルをVODにアップロードできます。自動化、システム化された本番環境に適しています。VODでは次のプログラム言語によるサーバーからのアップロードSDKからのアップロードを提供します。
    - [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
    - [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915)
    - [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
    - [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
    - [Golang SDK](https://intl.cloud.tencent.com/document/product/266/33919)
- [クライアントからのアップロード](https://intl.cloud.tencent.com/document/product/266/33921)
エンドユーザーはクライアントのローカルビデオをVODにアップロードできます。UGC、PGCなどのケースに適しています。VODは次のプラットフォームのクライアントからのアップロードSDKからのアップロードを提供します。
    - [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)
    - [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)
    - [Web端末のアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)
- [APIからのプルアップロード](https://intl.cloud.tencent.com/document/product/266/34118)
VOD が提供するサーバーAPIからのプルアップロードインタフェースを使用するとき、アップロードするメディアのURLを指定すると、VODバックエンドがファイルをオフラインでプルします。大量のまたは自動化されたメディアファイルを移行するケースに適しています。
- [LVBレコーディング](https://intl.cloud.tencent.com/document/product/267/31563)
CSSが提供するレコーディング機能を介して、LVBストリームのビデオ内容をVODにストレージし、アーカイブ、トリミングおよびレビューなどを実行します。

## ストレージリージョン

### サポート済みのリージョンリスト

VODでは世界中の複数のリージョンにストレージノードがあります。メディアをアップロードするプロセスではその内の1つのリージョンを選択してストレージします。現在、VODがサポートするストレージリージョンは次のとおりです。

|ストレージリージョン |リージョンの英語の略称 |
|---|----|
| 中国香港   |  ap-hongkong  |
| シンガポール     |     ap-singapore      |  
| ムンバイ      |    ap-mumbai        |
| ソウル     |     ap-seoul        |
| バンコク     |     ap-bangkok    |    
| シリコンバレー     |     na-siliconvalley |        
| アメリカ東部     |     na-ashburn |       
| トロント       |   na-toronto       | 
| フランクフルト     |     eu-frankfurt   |


### ストレージリージョンのアクティブ化

複数のストレージリージョンを構成する重要な目的はメディアアップロードの品質（成功率と速度）を向上させることです。アップロードの実行者とストレージノードの距離はアップロード品質に影響を及ぼし、通常、遠距離よりも近距離の方が高いアップロード品質を得られます。

VODサービスをアクティブにすると、VODは、**トロント、フランクフルト、中国香港、ムンバイ、東京、ソウル、モスクワ、シンガポール、バンコク、アメリカ東部**のストレージリージョンを自動的に割り当てます。業務上の必要性に応じて他のストレージリージョン（例：中国大陸）をアクティブにすることもできます。具体的な操作については、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)をご参照ください。**アクティブにすると、ストレージリージョンを非アクティブにすることはできません**。

### デフォルトのストレージリージョン

ストレージリージョンの内、デフォルトのストレージリージョンは1つのみです。ストレージリージョンを1つしか持たない場合は、それがデフォルトのストレージリージョンとなります。複数のストレージリージョンをアクティブにしている場合は、コンソールでその他のリージョンをデフォルトのストレージリージョンとして選択できます。具体的な操作については、 [ストレージリージョン設定](https://intl.cloud.tencent.com/document/product/266/18874#.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F.E6.AD.A5.E9.AA.A4) をご参照ください。

デフォルトのストレージリージョンの目的：一部のケースでは、このリージョンがメディアアップロードの対象リージョンとして優先的に選択されます。具体的な説明については、次のテキストをお読みください。

### ストレージリージョンの選択

メディアのアップロードにはストレージリージョンを選択する必要があります。デフォルトでVODバックエンドによって自動的に選択されることも、またアップロードリクエストで指定することもできます。

- VODバックグラウンドがストレージリージョンを自動的に選択する場合：
  - 開発者が1つのストレージリージョンしか持たない場合は、アップロードするすべてのメディアはそのリージョンにストレージされます。
  - 開発者が複数のストレージリージョンをアクティブにしている場合、各種アップロード方法の選択ポリシーは次のとおりです。
 <table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>アップロード方法</th>
<th>リージョン選択ポリシー</th>
</tr>
</thead>
<tbody>
<tr>
<td>コンソールからのローカルアップロード</td>
<td >アップロードする者の地理的位置に基づき、最寄りのストレージリージョンが選択されます</td>
</tr>
<tr>
<td>コンソールからのプルアップロード</td>
<td>デフォルトのストレージリージョンが常に選択されます</td>
</tr>
<tr>
<td>サーバーからのアップロード</td>
<td>アップロードする者の地理的位置に基づき、最寄りのストレージリージョンが選択されます</td>
</tr>
<tr>
<td>クライアントからのアップロード</td>
<td>アップロードする者の地理的位置に基づき、最寄りのストレージリージョンが選択されます </td>
</tr>
<tr>
<td>APIプルアップロード</td>
<td>デフォルトのストレージリージョンが常に選択されます   </td>
</tr>
<tr>
<td>LVBレコーディング</td>
<td>LVBストリームの所在リージョンに基づき、最寄りのストレージリージョンが選択されます </td>
</tr>
</tbody></table>
VODバックエンドでは、動的なスケジューリングを採用してより高品質なアップロードリージョンを選択します。選択結果は地理的位置、ネットワーク品質などの要因と関連します。
- 開発者がストレージリージョンを指定する場合の各種アップロード方法の指定方法は次のとおりです。
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>アップロード方法</th>
<th>リージョン指定方法</th>
</tr>
</thead>
<tbody>
<tr>
<td>コンソールからのローカルアップロード</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>コンソールからのプルアップロード</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>サーバーからのアップロード</td>
<td><ul style="margin:0;"><li><a href="https://intl.cloud.tencent.com/document/product/266/33914">Java SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">C# SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">PHP SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Python SDK</a></li></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Go SDK</a></li> </ul>  </td>
</tr>
<tr>
<td>クライアントからのアップロード</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/33922">クライアントからのアップロード署名パラメータ</a></td>
</tr>
<tr>
<td>APIプルアップロード</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/34118">プルアップロードインタフェースStorageRegionパラメータ</a> </td>
</tr>
<tr>
<td>LVBレコーディング</td>
<td>サポートしていません </td>
</tr>
</tbody></table>

## 機能と制限

### メディアのタイプ

VODは次のタイプのメディアファイルのアップロードをサポートしています。

* ビデオ：MP4、TS、FLV、WMV、ASF、RM、RMVB、MPG、MPEG、3GP、MOV、WEBM、MKV、AVI
* オーディオ：MP3、M4A、FLAC、OGG、WAV
* カバー画像：JPG、JPEG、PNG、GIF、BMP、TIFF、AI、CDR、EPS

### イベント通知

メディアアップロードが完了すると、VODバックエンドはこのイベント通知を送信します。イベント通知の原理については、 [イベントの通知](https://intl.cloud.tencent.com/document/product/266/33948) を、設定方法については、[イベント通知の設定](https://intl.cloud.tencent.com/document/product/266/14055) をそれぞれご参照ください。
各種アップロード方法に対応するイベント通知のタイプは次のとおりです。

| アップロード方法                                                 | イベント通知タイプ                                       |
| --------------------------------------------------------- | -------------------------------------------------- |
|<ul style="margin:0;"><li>コンソールからのローカルアップロード</li><li>サーバーからのアップロード</li><li>クライアントからのアップロード</li><li>LVBレコーディング</li></ul> | [ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950)         |
| <ul style="margin:0;"><li>コンソールからのプルアップロード</li><li>APIからのプルアップロード  </li>                         | [URLからのビデオプルアップロードの完了](https://intl.cloud.tencent.com/document/product/266/33951) |

### 付属機能

VODのメディアアップロードは、メディア資産管理関連、ビデオ処理とイベント通知関連、アップロード制御関連などの様々な付属機能をサポートしています。

#### メディア資産管理関連

- カバーの追加：ビデオをアップロードするときに画像を一緒にアップロードします。この画像はVODメディア資産システムでこのビデオのカバーとして自動的に設定されます。
- 有効期限の指定：アップロード時にメディアファイルの有効期限を指定し、指定時間に達した後、VODバックエンドはメディアファイルおよびそれに関連するファイル（トランスコードファイル、スクリーンキャプチャなど）を自動的に削除します。
- 分類の指定：アップロード後にこのメディアファイルの分類を設定します。

各種アップロード方法のサポート状況と使用法は下表のとおりです。

| 機能         | コンソールからのローカルアップロード                                               | コンソールからのプルアップロード | サーバーからのアップロード                                                   | クライアントからのアップロード                                                   | APIからのプルアップロード                                                 | LVBレコーディング                                |
| ------------ | ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------------- |
| カバーの追加     | サポートしていません                                                       | サポートしていません         | <ul style="margin:0;"><li>[Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2) | <ul style="margin:0;"><li> [Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926) | [プルアップロードインタフェースCoverUrlパラメータ](https://intl.cloud.tencent.com/document/product/266/34118)    | サポートしていません                                  |
| 有効期限の指定 | サポートしていません                                                       | サポートしていません         | <ul style="margin:0;"><li>[Java SDKインタフェースExpireTimeパラメータ](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDKインタフェースExpireTimeパラメータ](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[PHP SDKインタフェースExpireTimeパラメータ](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Python SDKインタフェースExpireTimeパラメータ](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Node.js SDKインタフェースExpireTimeパラメータ](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Go SDKインタフェースExpireTimeパラメータ](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | サポートしていません                                                       | [プルアップロードインタフェースExpireTimeパラメータ](https://intl.cloud.tencent.com/document/product/266/34118)  | [レコーディング設定](https://intl.cloud.tencent.com/zh/document/product/267/34223) |
| 分類の指定     | [分類の指定](https://intl.cloud.tencent.com/document/product/266/33890) | サポートしていません         | <ul style="margin:0;"><li> [Java SDKインタフェースClassIdパラメータ](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDKインタフェースClassIdパラメータ](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[PHP SDKインタフェースClassIdパラメータ](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Python SDKインタフェース ClassIdパラメータ](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Node.js SDKインタフェース ClassIdパラメータ](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Go SDKインタフェースClassIdパラメータ](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [クライアントからのアップロード署名classIdパラメータ](https://intl.cloud.tencent.com/document/product/266/33922) | [プルアップロードインタフェースClassIdパラメータ](https://intl.cloud.tencent.com/document/product/266/34118)| サポートしていません                                  |

#### ビデオ処理およびイベント通知関連

- 自動ビデオ処理：メディアのアップロードと同時に[タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931) を指定すると、アップロードの完了後にVODはこのタスクフローを自動的に実行します。よくあるケース：ビデオのスタートフレームの画像をキャプチャしてカバーにする、トランスコード、コンテンツ審査など。
- ビデオ処理イベント通知のパススルーフィールド：自動ビデオ処理が有効になっている場合は、処理が完了した後、VODバックエンドはイベント通知を開始して、このフィールドをパススルーします。
- アップロードイベント通知のパススルーフィールド：アップロードが完了後、VODバックエンドはイベント通知を開始してこのフィールドをパススルーします。

各種アップロード方法のサポート状況と使用法は下表のとおりです。

| 機能         | コンソールからのローカルアップロード                                               | コンソールからのプルアップロード | サーバーからのアップロード                                                   | クライアントからのアップロード                                                   | APIからのプルアップロード                                                 | LVBレコーディング                                |
| ------------------------ | ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| 自動ビデオ処理             | [アップロード後に自動的にビデオ処理を実行](https://intl.cloud.tencent.com/document/product/266/33890) | サポートしていません         | <ul style="margin:0;"><li>[Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81) | [クライアントからのアップロード署名procedureパラメータ](https://intl.cloud.tencent.com/document/product/266/33922) | [プルアップロードインタフェースProcedureパラメータ](https://intl.cloud.tencent.com/document/product/266/34118)   | サポートしていません   |
| ビデオ処理イベント通知のパススルーフィールド | サポートしていません                                                       | サポートしていません         | サポートしていません                                                       | クライアントからのアップロード署名 sessionContext パラメータ                           | [プルアップロードインタフェースSessionContextパラメータ](https://intl.cloud.tencent.com/document/product/266/34118) | サポートしていません   |
| アップロードイベント通知のパススルーフィールド     | サポートしていません                                                       | サポートしていません         | <ul style="margin:0;"><li>[Java SDKインタフェースSourceContextパラメータ](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDKインタフェースSourceContextパラメータ](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[PHP SDKインタフェースSourceContextパラメータ](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Python SDKインタフェースSourceContextパラメータ](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Node.js SDKインタフェースSourceContextパラメータ](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Go SDKインタフェースSourceContextパラメータ](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [クライアントからのアップロード署名sourceContextパラメータ](https://intl.cloud.tencent.com/document/product/266/33922) | サポートしていません                                                       | サポートしていません   |

#### アップロード制御関連

- 中断からの再開 ：アップロードプロセスが予期せず終了し（ネットワークの中断、ブラウザの終了など）、同一ファイルのアップロードを再度実行する場合に、ファイル全体をアップロードし直す必要がなく、中断した部分から引き続きアップロードすることができます。
- アップロードの一時停止/再開：アップロード中に自主的にアップロードを停止し、自主的にアップロードを再開することができます。
- アップロードのキャンセル：アップロード中に自主的にそのアップロードを終了することができます。
- アップロードの進行状況の取得：メディアのうちVODにアップロードされた部分の割合を取得することができます。
- マルチパートアップロード：アップロード時にメディアファイルを複数のパートに分割して、それぞれ別々にアップロードします。 弱いネットワーク環境の場合、ネットワーク異常による中断の影響を軽減できます。さらに高帯域幅環境の場合は、複数のパートを同時にアップロードして、ネットワーク帯域幅を充分に利用することができます。

各種アップロード方法のサポート状況と使用法は下表のとおりです。

| 機能         | コンソールからのローカルアップロード                                               | コンソールからのプルアップロード | サーバーからのアップロード                                                   | クライアントからのアップロード                                                   | APIからのプルアップロード                                                 | LVBレコーディング                                |
| -------------- | -------------------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------ | ------------------------------------------- |
| 中断からの再開       | サポートしていません               | 関連しません         | サポートしていません                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li><li>ミニプログラムSDKはサポートしていません | 関連しません       | 関連しません                                      |
| アップロードの一時停止と再開 | サポートしていません               | 関連しません         | サポートしていません                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>ミニプログラムSDKはサポートしていません | 関連しません       | 関連しません                                      |
| アップロードのキャンセル       | ブラウザページを更新または終了します | 関連しません         | サポートしていません                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>ミニプログラムSDKはサポートしていません | 関連しません       | [レコーディングタスクの終了](https://intl.cloud.tencent.com/document/product/267/30837) |
| アップロード進行状況の取得   |デフォルトでページに進行状況が表示されます     | サポートしていません         | サポートしていません                                                       |  <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li><li>[ミニプログラムSDK](https://intl.cloud.tencent.com/document/product/266/33927) | サポートしていません       | 関連しません                                      |
| マルチパートアップロード       | 有効になっています               | 関連しません         |<ul style="margin:0;"><li> [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0) | <ul style="margin:0;"><li> Web SDKではデフォルトで有効になっています</li><li>Android SDKではデフォルトで有効になっています</li><li>iOS SDKではデフォルトで有効になっています</li><li>ミニプログラム SDKはサポートしていません | 関連しません       | 関連しません                                      |

### 制限

- メディアファイルサイズの制限は次のとおりです。
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>アップロード方法</th>
<th>メディアサイズの制限</th>
</tr>
</thead>
<tbody>
<tr>
<td><ul style="margin:0;"><li>コンソールからのローカルアップロード</li><li>クライアントからのアップロード - Web SDK</td>
<td >60GB</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>サーバーからのアップロード</li><li>コンソールからのプルアップロード</li><li> APIからのプルアップロード</td>
<td>48.82TB（50,000GB）</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>クライアントからのアップロード - Android SDK</li><li>クライアントからのアップロード - iOS SDK </td>
<td>10GB </td>
</tr>
<tr>
<td>LVBレコーディング</td>
<td><ul style="margin:0;"><li>MP4/FLV 形式は48.82TB（50,000GB）です</li><li>HLS形式はサイズに制限はありません</li><li> その他制限は <a href="https://intl.cloud.tencent.com/document/product/267/31563">LVBレコーディングに依存します</a></td>
</tr>
</tbody></table>
- ファイル数量：制限がありません。
