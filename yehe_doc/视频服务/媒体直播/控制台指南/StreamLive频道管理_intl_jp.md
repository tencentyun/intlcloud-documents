StreamLiveコンソールはChannelディメンションをベースとして管理されます。お客様は高品質のビデオストリームを作成し、さまざまなタイプのデバイスに配信することができます。チャネルはStreamLiveのメインモジュールであり、所定の設定に従って入力ストリームに対し、トランスコードやカプセル化形式の変換など、一連のビデオ処理操作を行い、指定された宛先またはアーカイブストレージに出力することができます。

### チャネル作成

【Channel Management】メニューを選択し、【Create Channel】をクリックしてチャネル入力を作成します。

#### 1、チャネル名のカスタマイズ

作成したさまざまなチャネルを識別するために用いられます。【Next Step】をクリックして、次のステップに進みます。

![img](https://main.qcloudimg.com/raw/824d8ad80106fb65f69df5dffae7bd0b.png)

#### 2、入力ソースの追加

作成済みのチャネル入力から1つまたは複数を入力ソースとして選択してStreamLiveチャネルに追加します。**通常、デフォルトでは最初の入力を入力ソースとして使用します**。その他の入力ソースはフェイルオーバー（Failover）やタイムプラン（Plan）で使用されることがあります。1つのチャネルには、最大5つの入力ソースをバインドすることができ、そのうちPUSH入力は最大2つとなります。
![img](https://main.qcloudimg.com/raw/72974873310b8f07ea0acc09ce3c3f64.png)

さまざまなタイプの入力ソースについて、【settings】をクリックして以下の設定を行うことができます。

a. 【オーディオセレクター】RTP_PUSH / RTP-FEC_PUSH / UDP_PUSH入力ソースに複数のオーディオストリームがある場合、MPEGTSにおいてカプセル化されたオーディオPIDに基づいてここでセレクターを作成し、後で出力設定画面で複数のオーディオ言語を設定できるようにすることが可能です。
![img](https://main.qcloudimg.com/raw/8ea9e3a78e57242e446f4ab2f4cd6850.png)

>!
> - ここのPIDは、必ず入力オーディオストリームのPIDと同じである必要があります。同じでない場合、トランスコードタスクが失敗する可能性があります。
> - 最初の入力（1行目の入力）のみ、オーディオセレクターの設定を行うことができます。その他の状況では設定は無効になります。Planの入力切り替えにより入力ソースが使用されている場合、システムはデフォルトで1つのオーディオトラックを選択し、トランスコードを行います。
> - 入力ソースがフェイルオーバーを設定している場合、バックアップストリームは自動的にメインストリームと一致するオーディオセレクターの設定を維持し、メイン/バックアップの切り替え時にオーディオトランスコードの可用性を確保できるようにします。

b. 【プル設定】MP4_PULL / HLS_PULL入力ソースに、プルリツイートのソース側の動作を設定することができます。2つのモード：LOOPは繰り返しプルします。ONCEは1回プルした後、自動的に入力ストリームを切断します。
![img](https://main.qcloudimg.com/raw/a721d60a7263dddeab3927b3331cfaa2.png)

c. 【フェイルオーバーの設定】RTMP_PUSH / RTP_PUSH入力ソースにフェイルオーバーを設定し、メインストリームに異常が生じたときに自動的にバックアップストリームに切り替えて入力できるようにすることができます。フェイルオーバーの有効化を選択した後、1つの入力ソースを現在の入力ストリームのバックアップストリームとして選択することができ、また障害検出時間（メインストリームの異常がどれほど続いたらフェイルオーバーを起動するか。デフォルトは3000ms）や入力ソースの優先順位（メインストリームの回復後にメインストリームの入力へ優先的に切り替えるかどうか。PRIMARY_PREFERREDはメインストリームを優先とし、EQUAL_PREFERREDはメイン/バックアップを同一優先順位とします）を設定することができます。
![img](https://main.qcloudimg.com/raw/588efa49ee40b158793421c6ced77319.png)
![img](https://main.qcloudimg.com/raw/ebc0d3305a94534edaf97d09ecf18f9c.png)

>?
> - 最大で1組のメインストリームとバックアップストリームしか設定できず、メインストリームとバックアップストリームは入力ソースタイプが同一、チャネル数も同一であることが必要です。
> - メイン/バックアップ関係の確定後、バックアップストリームのフェイルオーバースイッチは自動的にOFFにロック（自分でバックアップストリームを追加し続けることができないことを示す）されます。メイン/バックアップ関係の調整が必要な場合（メイン/バックアップの交換など）は、まず現在のメイン/バックアップ関係を解除/変更した後に新たに設定することが必要です。
> - フェイルオーバーの設定完了後、メインストリームとバックアップストリームの入力名の横に「Primary」と「Backup」の表示フィールドが出現することがあります。
> - バックアップストリームは自動的にメインストリームの下に位置づけられます。

以上の設定以外に、各入力について、以下の操作を行うことができます。

- 【details】をクリックして、入力アドレスなど、入力ソースの基本情報を確認します
- 【Set as First】をクリックして入力をトップに置き、この設定をデフォルト入力とします。注意：バックアップストリームをトップに置くことはできません。
- 【delete】をクリックして特定の入力ソースを削除します。

【Next Step】をクリックして次のステップに進みます。

#### 3、出力グループの設定

a. 複数の出力グループを設定します。StreamLiveは、1つのチャネルに対して複数のOutput Groupの出力をサポートします。右上のプラス記号をクリックして、複数のOutput Groupを追加します。

![img](https://main.qcloudimg.com/raw/e6af7ba8a52e288e0d02dc3bea54871e.png)

b. 出力グループ名とタイプです。現在のOutput Groupの名称とタイプを設定します。 現在、StreamLiveをサポートし、HLSおよびDASHタイプの出力をサポートするとともに、HLSファイルのTencent Cloud COSへの出力、アーカイブをサポートしています（具体的な操作についてはセクション6を参照）。また、Tencent Cloud StreamPackageと直接組み合わせて一緒に使用し、HLS/DASH形式のCSSストリームを同じアカウントのStreamPackageへ直接出力することもサポートしています（具体的な操作についてはセクション7を参照）。これにより、お客様が独自のオリジンサーバーを構築し、ライブストリーミングの大規模かつ安定的な配信を行うお手伝いをします。

>?
> - Tencent Cloud COSの詳細については、[Tencent Cloud COSの詳細](https://intl.cloud.tencent.com/document/product/436/6222)をご参照ください。
> - Tencent Cloud StreamPackageの詳細については、[Tencent Cloud StreamPackageの詳細](https://intl.cloud.tencent.com/document/product/1063/41786)をご参照ください。

![img](https://main.qcloudimg.com/raw/6b87cbe42011cc98c045af99369348a3.png)

c. CDNのプッシュアドレスの設定です。HLSまたはDASHプロトコルタイプの出力を選択した場合は、ここにCDNのプッシュアドレスを入力できます。プッシュアドレスに検証要件がある場合は、検証情報を入力できます。

![img](https://main.qcloudimg.com/raw/8fb39dfab5a32ea34444b9a6f1e4edab.png)

d. セグメントの設定です。ManifestファイルのSegment長とSegment数を設定します。タグファイルにutc時間を挿入する必要がある場合は、Pdtスイッチをオンにして、utc時間を挿入する間隔を設定できます。

![img](https://main.qcloudimg.com/raw/36b16a1dda37c530d7b8f497688a93d9.png)

e. DRMの設定です。Tencent Cloud StreamLiveはユーザー定義のDRMをサポートしており、お客様は実際のニーズに応じて選択することができます。

![](https://qcloudimg.tencent-cloud.cn/raw/f1cffba329af61327687d0efbe7442e1.png)

DRMの設定においてはSDMCDRMをDRMとして選択することもサポートしています。ユーザーはUid、SecretID、Secret KeyおよびUrlフィールドの入力が必須です。

![](https://qcloudimg.tencent-cloud.cn/raw/e1350792aa213fe072920231474b0f68.png)

>?
>- Output Group SettingのOutput Group Typeにおいて、HLS/HLS_ARCHIVE/HLS_StreamPackageを選択し、DRMを有効にした場合、デフォルトでFairplay暗号化が用いられます。Output Group SettingのOutput Group Typeにおいて、DSAH/DASH_StreamPackageを選択し、DRMを有効にした場合、デフォルトではWidevineにより暗号化が行われます。
>- Fairplayキーの設定です。出力タイプとしてHLS/HLS_ARCHIVE/HLS_StreamPackageを選択した場合、その時点での暗号化方法はFairplay暗号化であり、FairplayのContentId（KeyId）、Key、Ivを入力する必要があります。KeyとIvは32ビットの16進文字列です。
 ![img](https://main.qcloudimg.com/raw/e172623be22b4397d9f4964d90e8eb03.png)
>- Widevineキーの設定です。出力タイプとしてDSAH/DASH_StreamPackageを選択した場合、そのときの暗号化方法はWidevineになります。WidevineのContentIdとそのTrack Settingのうち、TrackタイプはSD/HD/UHD1/UHD2/AUDIOに分かれます。
>- All Trackを選択することは、5つのTrackタイプで同一のKeyIdとKeyを指定することを意味します。
 ![img](https://main.qcloudimg.com/raw/06b22ae97702570f7bdfac4161219ece.png)
>- Select Trackを選択すると、Trackタイプ毎にKeyIdとKeyをカスタマイズできます。
![img](https://main.qcloudimg.com/raw/9c9e6b56980d6c87aea64c2b3b426ad5.png)

f. オーディオの設定です。StreamLiveは、1つの出力ユニットをサポートして、複数のオーディオトランスコードを構成します。ここでは、オーディオ名、オーディオトランスコード形式、オーディオビットレート、対応するオーディオ言語などのオーディオテンプレートを構成することができます。オーディオセレクターが関連付けられていない場合は、Input入力ストリームからデフォルトのストリームが選択され、トランスコードの出力が行われます。現在サポートされているオーディオトランスコードのビットレートの範囲は、6000～1024000ビットです。言語コードはISO639規格に準拠しており、3文字の言語コードの入力が必要です。

![img](https://main.qcloudimg.com/raw/c092adee1a2aeca7f9e98f18659b4aef.png)

g. ビデオの設定です。StreamLiveは、ビデオテンプレート名、エンコーダタイプの選択（現在H264をサポート）、ビデオトランスコードのビットレート（サポート範囲は50000～40000000ビット）解像度、フレームレート構成などを含むビデオテンプレートの構成をサポートします。「Top Speed Codec Transcoding」は、Tencent Cloudビデオチームによって開発された高性能ビデオトランスコードサービスです。この機能をオンにすると、AIアルゴリズム機能を使用して、ビジネスシナリオに適した最適な動的コーデックパラメータをリアルタイムに算出し、低ビットレートかつ高品質のトランスコーディングサービスを実現することができます。「Bitrate compression ratio」とは、低減が必要と思われるビデオビットレートのパーセンテージのことです。

![img](https://main.qcloudimg.com/raw/92242c0a054e342a1071794db28600de.png)

>? インテリジェントなビデオ圧縮アルゴリズムを備えたより優れたコーデックが必要な場合は、「超高速HD（TESHD）」トランスコーディングを選択できます。この機能を有効にすると、AIアルゴリズムはビジネスシナリオに応じて、最適な動的コーデックパラメータをリアルタイムに算出し、低ビットレートかつ高品質なトランスコーディングサービスを実現することができます。

h. 出力の組み合わせです。Outputsを構成し、作成済みのオーディオトランスコードテンプレートとビデオトランスコードテンプレートを組み合わせてバインドします。また、HLSまたはDASHのファイルタグにおけるScte35関連情報の伝送をサポートします。

![img](https://main.qcloudimg.com/raw/9e2db2401085804c20ea520364f43c3a.png)

i. 下の【Done】をクリックして、設定を保存します。

![img](https://main.qcloudimg.com/raw/1874e5ebae643cddbe8f41c00bc92731.png)

j. この時点で、チャネル全体の構成が完了しています。【Start】をクリックすれば、実行できます。

![img](https://main.qcloudimg.com/raw/ec0fe249551d5db6d80697a1c5d47d36.png)


### チャネルのインポート・エクスポート、クローン作成および編集・削除

StreamLiveは、チャネル構成ファイルのエクスポート/インポートとチャネルのクローン機能により、チャネルの作成をすばやく完了する業務をサポートしています。

#### チャネルのエクスポート

StreamLiveの【Channel Management】インターフェースには、作成したすべてのチャネルとそのステータスが表示されます。右側の【Export】ボタンをクリックすると、チャネル構成jsonファイルをすばやくエクスポートできます。

![img](https://main.qcloudimg.com/raw/764c7eea7b0ea222364a5b4dad88eb41.png)

![img](https://main.qcloudimg.com/raw/e67829bbee59c2148ba68ae1e652f8da.png)

#### チャネルのインポート

【Channel Management】インターフェースを開き、【Create Channel】ボタンをクリックして【Import Configuration】を選択し、変更したチャネル構成jsonファイルを選択して保存します。

jsonファイルを送信した後、チャネル編集ステータスに入るので、続いて通常の構成プロセスに従ってチャネルを保存して送信すれば完了です。

![img](https://main.qcloudimg.com/raw/1fe8fdf4c50c5be5a6fe1dc820f5469f.png)

>?
> - チャネルインポート機能とは、実際はクイック入力プロセスです。インポートしたjsonファイルに基づいて、【Basic Information】、【Output Group Setting】という2つの部分の内容が自動的に入力されます。【Input Setting】部分は無視されますので、Inputを再選択する必要があります。従って、この方法ですばやくChannelを作成する必要がある場合は、あらかじめ新しいinputを作成できます。
> - チャネルの編集時に新しい構成ファイルをインポートすると、元のチャネル構成情報が上書きされます。

#### チャネルクローン

チャネルクローンの本質とは、特殊なチャネルのエクスポート/インポートのすばやい操作です。【Channel Management】インターフェースを開き、【Operation】の下の【Clone】をクリックすれば、クローンチャネルの構成ステータスに進めます。

このとき、チャネルは作成されたクローンチャネルの基本情報（【Input Setting】部分を除く）を自動的に入力し、通常の構成プロセスに従ってチャネルを保存して送信します。

![img](https://main.qcloudimg.com/raw/92bf580af5c4f013363915688744f1f6.png)

1. チャネルの編集と削除

【RUNNING】プロセスではチャネルの編集・削除はできませんので、まず【Stop】チャネルの編集/削除操作を行ってください。

![img](https://main.qcloudimg.com/raw/57923bc62f83d99ee10df572bebbb6e3.png)

### チャネル品質のモニタリング

【Channel Management】インターフェースを開き、チャネル名をクリックしてチャネル詳細画面に進みます。チャネルの詳細画面には、チャネル情報、入力、出力、Alerts、Healthなどの詳細情報が表示されます。

![img](https://main.qcloudimg.com/raw/c97468a3a9fbeb51e9c15ae552d53efd.png)

いずれかのチャネルのいずれかのパイプラインで問題または潜在的な問題が発生すると、StreamLiveはそのチャネルのアラームを生成します。Set timeはアラーム発生時のイベント、Cleared timeはアラームがキャンセルされた時間です。 同じアラーム記録にステータスが更新されます。アラーム記録がSETステータスの場合、Set time、Stateは赤で表示されます。アラーム記録が削除されると、ステータスがCLEAREDになると同時に、上記の赤い表示は消えます。アラームは、問題が発生したパイプライン、アラームタイプおよび詳細情報を明確に記録します。データクエリーは過去5日間のみクエリーを実行でき、クエリー期間は24時間未満です。

キャンセル前：

![img](https://main.qcloudimg.com/raw/a76c4bb27dd86c6e2d06f2dd6ccbb42e.png)

キャンセル後：

![img](https://main.qcloudimg.com/raw/4a986687ccdf97ce0e222aac2b936fb6.png)

Heathはユーザーに対し、チャネル入力（帯域幅・入力ビデオフレームレート・入力オーディオフレームレート）と出力（帯域幅）の情報および対応するグラフを提供して、現在のチャネルが正しく機能しているかどうか判断します。データクエリーは過去5日間のみクエリーを実行でき、クエリー期間は24時間未満です。

![img](https://main.qcloudimg.com/raw/e49e312b0d134d0d9fb1c8dccbcee00b.png)
![img](https://main.qcloudimg.com/raw/de84757254338b428e55695b4b3a2170.png)


### タイムプランの設定

StreamLiveチャネルにタイムプランを設定し、プッシュ中の予定時間に特定イベントをトリガーする設定を実装することができます（例：15:00:00に入力ソースをinput2に切り替える）。

【Channel Management】インターフェースを開き、チャネル名をクリックしてチャネル詳細画面に進み、【Plan】を選択し、【Add】をクリックしてイベントを追加します。

1. 2種類のトリガー時間のモードを選択することができます。Fixed Timeは手動で日付と時間の設定が必要で、イベントは設定された時間に実行されます。Immediateは現在のセットアップタイムをトリガー時間とし、すぐにイベントが開始されます。
2. イベントタイプは現在「入力切り替え」機能のみをサポートしており、その対象となる入力ソースを選択することができます。

【create】をクリックして、時間-イベントの作成を完了します。

![img](https://main.qcloudimg.com/raw/b45ec0b7275bc1c4363bd683652dd541.png)

![img](https://main.qcloudimg.com/raw/cb4c8a9d4f289072476364297346fb4d.png)

>!
> - 入力する時間はお客様の所在地の現地時間です。現在より早い時間を入力することはできません。
> - 切り替えたMP4_PULL (またはHLS_PULL)入力ソースのストリーム設定がONCEの場合、一度プルした後で入力ストリームは自動的に切断され、その後のイベントはトリガーされません。

作成されたすべてのイベントを「トリガー時間」の時系列によって上から順に並べ、イベントを閲覧、削除、追加することができます。

>! 作成済みイベントの編集操作はサポートしていません。

### チャネル構成のベストプラクティス

StreamLiveではその他にも様々なカスタマイズ機能をご提供しています。具体的には次のベストプラクティス操作ガイドをご参照ください。

[DRMtodayをチャネル構成DRMとして使用](https://intl.cloud.tencent.com/document/product/1048/45217) 
[StreamLiveによるTencent Cloud COSアーカイブへの出力](https://intl.cloud.tencent.com/document/product/1048/45218)
[StreamLiveによるTencent Cloud StreamPackageへの出力](https://intl.cloud.tencent.com/document/product/1048/45218)
[StreamLiveを使用したCSSタイムシフト](https://intl.cloud.tencent.com/document/product/1048/45220)

