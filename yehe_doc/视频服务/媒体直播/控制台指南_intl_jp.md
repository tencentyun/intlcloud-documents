## 概要

Tencent Cloud StreamLiveは、Tencent Cloudが新たにリリースした高品質のストリーム処理プラットフォームです。ブロードキャストレベルのリアルタイム・オンラインストリーミングメディアの処理サービスを提供できます。Tencent Cloud独自の高性能ビデオコーデックおよび圧縮アルゴリズムを使用することによって、より良い視聴体験を確保しながら、送信トラフィックの節約に取り組みます。

StreamLiveコンソールはChannelディメンションをベースとして管理されます。お客様は高品質のビデオストリームを作成し、さまざまなタイプのデバイスに配信することができます。

## コンソール概要

StreamLiveコンソールはChannelディメンションをベースとして管理されます。これは主に、セキュリティグループ（Security Groups）、チャネル入力（Input）、チャネル管理（Channel）という3つのモジュールに分かれます。セキュリティグループは、主に入力ソースのセキュリティ検証を管理します。チャネル入力は、チャネル入力ソースのプロトコルと入力モードを設定することができます。チャネルはStreamLiveのメインモジュールであり、所定の設定に従って入力ストリームに対し、トランスコードやカプセル化形式の変換など、一連のビデオ処理操作を行い、指定された宛先またはアーカイブストレージに出力することができます。

![](https://main.qcloudimg.com/raw/e76d930fd73f010632e9e4571a8351d9.png)

## 前提条件

[Tencent CloudのStreamLiveコンソール](https://console.cloud.tencent.com/mdl/security)にログインします。

## 操作手順

### 1.   リージョンの選択

Tencent Cloud StreamLiveは現在、インドのムンバイ、タイのバンコク、韓国のソウルに3つのアベイラビリティーゾーンを提供しており、お客様はここで所在するリージョンを選択することができます。日本の東京などのリージョンでは、アクセラレーションのデプロイがリリースされているところです。他のアベイラビリティーゾーンにおけるアクセラレーションのデプロイのリクエストがある場合は、[お問い合わせください](https://intl.cloud.tencent.com/contact-sales)。

![](https://main.qcloudimg.com/raw/c9da8ddd469f557487c5b6d943ef69af.png)

### 2.   セキュリティグループの作成

セキュリティグループは、入力ソースのIPV4アドレスの有効性を検証するために用いられます。セキュリティグループの設定を入力することにより、StreamLiveチャネルの入力をより安全なものにできます。

【Security Group Management】メニューを選択し、【Create Security Group】をクリックしてセキュリティグループを作成します。Nameを入力した後、CIDR形式の文字列を新しい入力セキュリティグループに追加し、コンマまたは改行文字で区切ります。入力が終わったら、【Confirm】をクリックして作成を完了します。

![](https://main.qcloudimg.com/raw/e5c7365ba3724802b2013b3c25cdc07b.png)

>?
>- セキュリティグループには、idleとoccupiedという2つのステータスがあります。
>- idleとは、現在のセキュリティグループが関連付けられておらず、編集と削除ができることを意味します。
>- occupiedとは、現在のセキュリティグループがchannel-inputに関連付けられていることを意味します。現時点では、セキュリティグループは編集のみが可能で、削除はできません。
>- コンソールはデフォルトで、5つのセキュリティグループの作成のみをサポートしています。セキュリティグループの作成要件がさらにある場合は、[チケットを提出](https://console.cloud.tencent.com/workorder)して、Tencent Cloudカスタマサービスのスタッフにお問い合わせください。

### 3.   入力の作成

【Input Management】メニューを選択し、【Create Input】をクリックしてチャネル入力を作成します。

チャネル入力は、StreamLiveのメディアストリーム入力チャネルであり、通常はセキュリティグループとStreamLiveチャネルに関連付けられています。チャネル入力は現在、RTP、RTP-FEC、RTMP、UDP、HLS、HTTP-MP4などのプロトコル入力をサポートしており、PULLとPUSHという2つの入力方法を提供しています。

各チャネル入力は1つのセキュリティグループと1つのチャネルに関連付けることができ、チャネルに関連付けられた入力のステータスはattachedで表示されます。

![](https://main.qcloudimg.com/raw/eed9a73cc25fc646b1f601ac545ccc0e.png)

>?
>- コンソールは、デフォルトで最大5つのinputの存在のみをサポートします。
>- 入力のメディアソースには、現在、少なくとも1つのビデオデータチャネルが含まれている必要があります。
>- MPEG-TS多重化チャネルを使用する場合、最大8チャネルを同時に送信できます。

### 4.   StreamLiveチャネルの作成

1. 【Channel Management】メニューを選択し、【Create Channel】をクリックしてチャネル入力を作成します。

2. カスタムチャネル名。作成したさまざまなチャネルを識別するために用いられます。【Next Step】をクリックして、次のステップに進みます。

![](https://main.qcloudimg.com/raw/824d8ad80106fb65f69df5dffae7bd0b.png)

3. 入力ソースを追加します。作成済みのチャネル入力から1つまたは複数を入力ソースとして選択してStreamLiveチャネルに追加します。**通常、デフォルトでは最初の入力を入力ソースとして使用します**。その他の入力ソースはフェイルオーバー（Failover）やタイムプラン（Plan）で使用されることがあります。1つのチャネルには、最大5つの入力ソースをバインドすることができ、そのうちPUSH入力は最大2つとなります。

![](https://main.qcloudimg.com/raw/72974873310b8f07ea0acc09ce3c3f64.png)

さまざまなタイプの入力ソースについて、【settings】をクリックして以下の設定を行うことができます。

a. 【オーディオセレクター】RTP_PUSH / RTP-FEC_PUSH / UDP_PUSH入力ソースに複数のオーディオストリームがある場合、MEPGTSにおいてカプセル化されたオーディオPIDに基づいてここでセレクターを作成し、後で出力設定画面で複数のオーディオ言語を設定できるようにすることが可能です。

![](https://main.qcloudimg.com/raw/8ea9e3a78e57242e446f4ab2f4cd6850.png)

>!
>- ここのPIDは、必ず入力オーディオストリームのPIDと同じである必要があります。同じでない場合、トランスコードタスクが失敗する可能性があります。
>- 最初の入力（1行目の入力）のみ、オーディオセレクターの設定を行うことができます。その他の状況では設定は無効になります。Planの入力切り替えにより入力ソースが使用されている場合、システムはデフォルトで1つのオーディオトラックを選択し、トランスコードを行います。
>- 入力ソースがフェイルオーバーを設定している場合、バックアップストリームは自動的にメインストリームと一致するオーディオセレクターの設定を維持し、メイン/バックアップの切り替え時にオーディオトランスコードの可用性を確保できるようにします。

b. 【プル設定】MP4_PULL / HLS_PULL入力ソースに、プルリツイートのソース側の動作を設定することができます。2つのモード：LOOPは繰り返しプルします。ONCEは1回プルした後、自動的に入力ストリームを切断します。

![](https://main.qcloudimg.com/raw/a721d60a7263dddeab3927b3331cfaa2.png)

c. 【フェイルオーバーの設定】RTMP_PUSH / RTP_PUSH入力ソースにフェイルオーバーを設定し、メインストリームに異常が生じたときに自動的にバックアップストリームに切り替えて入力できるようにすることができます。フェイルオーバーの有効化を選択した後、1つの入力ソースを現在の入力ストリームのバックアップストリームとして選択することができ、また障害検出時間（メインストリームの異常がどれほど続いたらフェイルオーバーを起動するか。デフォルトは3000ms）や入力ソースの優先順位（メインストリームの回復後にメインストリームの入力へ優先的に切り替えるかどうか、PRIMARY_PREFERREDをメインストリームの優先とするか、EQUAL_PREFERREDをメイン/バックアップの同一優先順位とするかなど）を設定することができます。

![](https://main.qcloudimg.com/raw/588efa49ee40b158793421c6ced77319.png)

![](https://main.qcloudimg.com/raw/ebc0d3305a94534edaf97d09ecf18f9c.png)

>?
>- 最大で1組のメインストリームとバックアップストリームしか設定できず、メインストリームとバックアップストリームは入力ソースタイプが同一、チャネル数も同一であることが必要です。
>- メイン/バックアップ関係の確定後、バックアップストリームのフェイルオーバースイッチは自動的にOFFにロック（自分でバックアップストリームを追加し続けることができないことを示す）されます。メイン/バックアップ関係の調整が必要な場合（メイン/バックアップの交換など）は、まず現在のメイン/バックアップ関係を解除/変更した後に新たに設定することが必要です。
>- フェイルオーバーの設定完了後、メインストリームとバックアップストリームの入力名の横に「Primary」と「Backup」の表示フィールドが出現することがあります。
>- バックアップストリームは自動的にメインストリームの下に位置づけられます。

以上の設定以外に、各入力について、以下の操作を行うことができます。

- 【details】をクリックして、入力アドレスなど、入力ソースの基本情報を確認します。
- 【Set as First】をクリックして入力をトップに置き、この設定をデフォルト入力とします。注意：バックアップストリームをトップに置くことはできません
- 【delete】をクリックして特定の入力ソースを削除します。

【Next Step】をクリックして次のステップに進みます。

4. 出力グループを設定します。

a. 複数の出力グループを設定します。StreamLiveは、1つのチャネルに対して複数のOutput Groupの出力をサポートします。右上のプラス記号をクリックして、複数のOutput Groupを追加します。

![](https://main.qcloudimg.com/raw/e6af7ba8a52e288e0d02dc3bea54871e.png)

b. 出力グループ名とタイプです。現在のOutput Groupの名称とタイプを設定します。 現在、StreamLiveをサポートし、HLSおよびDASHタイプの出力をサポートするとともに、HLSファイルのTencent Cloud COSへの出力、アーカイブをサポートしています（具体的な操作についてはセクション6を参照）。また、Tencent Cloud StreamPackageと直接組み合わせて一緒に使用し、HLS/DASH形式のCSSストリームを同じアカウントのStreamPackageへ直接出力することもサポートしています（具体的な操作についてはセクション7を参照）。これにより、お客様が独自のオリジンサーバーを構築し、ライブストリーミングの大規模かつ安定的な配信を行うお手伝いをします。

>?
>- Tencent CloudのCOSの詳細は、下記をご覧ください。[COSの詳細](https://intl.cloud.tencent.com/document/product/436/6222)
>- Tencent Cloud StreamPackageの詳細は、下記をご覧ください。[StreamPackageの詳細](https://intl.cloud.tencent.com/document/product/1063/41786)

![](https://main.qcloudimg.com/raw/6b87cbe42011cc98c045af99369348a3.png)

c. CDNのプッシュアドレスの設定です。HLSまたはDASHプロトコルタイプの出力を選択した場合は、ここにCDNのプッシュアドレスを入力できます。プッシュアドレスに検証要件がある場合は、検証情報を入力できます。

![](https://main.qcloudimg.com/raw/8fb39dfab5a32ea34444b9a6f1e4edab.png)

d. セグメントの設定です。ManifestファイルのSegment長とSegment数を設定します。タグファイルにutc時間を挿入する必要がある場合は、Pdtスイッチをオンにして、utc時間を挿入する間隔を設定できます。

![](https://main.qcloudimg.com/raw/36b16a1dda37c530d7b8f497688a93d9.png)

e. DRMの設定です。Tencent Cloud StreamLiveはユーザー定義のDRMをサポートしており、お客様は実際のニーズに応じて選択することができます。

![](https://main.qcloudimg.com/raw/fbb528cc453be167497d4d7eca823d43.png)

>? Output Group SettingのOutput Group Typeにおいて、HLS/HLS_ARCHIVE/HLS_StreamPackageを選択し、DRMを有効にした場合、デフォルトでFairplay暗号化が用いられます。Output Group SettingのOutput Group Typeにおいて、DSAH/DASH_StreamPackageを選択し、DRMを有効にした場合、デフォルトではWidevineにより暗号化が行われます。
>-  Fairplayキーの設定です。出力タイプとしてHLS/HLS_ARCHIVE/HLS_StreamPackageを選択した場合、その時点での暗号化方法はFairplay暗号化であり、FairplayのContentId（KeyId）、Key、Ivを入力する必要があります。KeyとIvは32ビットの16進文字列です。
![](https://main.qcloudimg.com/raw/e172623be22b4397d9f4964d90e8eb03.png)
>-  Widevineキーの設定です。出力タイプとしてDSAH/DASH_StreamPackageを選択した場合、そのときの暗号化方法はWidevineになります。WidevineのContentIdとそのTrack Settingのうち、TrackタイプはSD/HD/UHD1/UHD2/AUDIOに分かれます。
>- All Trackを選択することは、5つのTrackタイプで同一のKeyIdとKeyを指定することを意味します。
![](https://main.qcloudimg.com/raw/06b22ae97702570f7bdfac4161219ece.png)
>- Select Trackを選択すると、Trackタイプ毎にKeyIdとKeyをカスタマイズできます。
![](https://main.qcloudimg.com/raw/9c9e6b56980d6c87aea64c2b3b426ad5.png)

f. オーディオの設定です。StreamLiveは、1つの出力ユニットをサポートして、複数のオーディオトランスコードを構成します。ここでは、オーディオ名、オーディオトランスコード形式、オーディオビットレート、対応するオーディオ言語などのオーディオテンプレートを構成することができます。オーディオセレクターが関連付けられていない場合は、Input入力ストリームからデフォルトのストリームが選択され、トランスコードの出力が行われます。現在サポートされているオーディオトランスコードのビットレートの範囲は、6000～1024000ビットです。言語コードはISO639規格に準拠しており、3文字の言語コードの入力が必要です。

![](https://main.qcloudimg.com/raw/c092adee1a2aeca7f9e98f18659b4aef.png)

g. ビデオの設定です。StreamLiveは、ビデオテンプレート名、エンコーダタイプの選択（現在H264をサポート）、ビデオトランスコードのビットレート（サポート範囲は50000～40000000ビット）解像度、フレームレート構成などを含むビデオテンプレートの構成をサポートします。「Top Speed Codec Transcoding」は、Tencent Cloudビデオチームによって開発された高性能ビデオトランスコードサービスです。この機能をオンにすると、AIアルゴリズム機能を使用して、ビジネスシナリオに適した最適な動的コーデックパラメータをリアルタイムに算出し、低ビットレートかつ高品質のトランスコーディングサービスを実現することができます。「Bitrate compression ratio」とは、低減が必要と思われるビデオビットレートのパーセンテージのことです。

![](https://main.qcloudimg.com/raw/92242c0a054e342a1071794db28600de.png)

>? インテリジェントなビデオ圧縮アルゴリズムを備えたより優れたコーデックが必要な場合は、「超高速HD（TESHD）」トランスコーディングを選択できます。この機能を有効にすると、AIアルゴリズムはビジネスシナリオに応じて、最適な動的コーデックパラメータをリアルタイムに算出し、低ビットレートかつ高品質なトランスコーディングサービスを実現することができます。

h. 出力の組み合わせです。Outputsを構成し、作成済みのオーディオトランスコードテンプレートとビデオトランスコードテンプレートを組み合わせて関連付けます。また、HLSまたはDASHのファイルタグにおけるScte35関連情報の伝送をサポートします。

![](https://main.qcloudimg.com/raw/9e2db2401085804c20ea520364f43c3a.png)

i. 下の【Done】をクリックして、設定を保存します。

![](https://main.qcloudimg.com/raw/1874e5ebae643cddbe8f41c00bc92731.png)

j. この時点で、チャネル全体の構成が完了しています。【Start】をクリックすれば、実行できます。

![](https://main.qcloudimg.com/raw/ec0fe249551d5db6d80697a1c5d47d36.png)

### 5.   StreamLiveを介したTencent CloudのCOSアーカイブへのエクスポート

StreamLiveは、HLSファイルのTencent Cloud COSへのエクスポート、アーカイブをサポートします。お客様はあらかじめCOSでバケットの作成を完了し、StreamLiveのバケットへのアクセス権を付与する必要があります。

1. COSサービスのアクティブ化とCOSバケットの作成

COSにエクスポートしてアーカイブする前に、あらかじめ[Tencent Cloud COSサービスのアクティブ化](https://console.cloud.tencent.com/cos5)を確実に行ってください。COSサービスのアクティブ化が完了したら、[COSバケットコンソール](https://console.cloud.tencent.com/cos5)で【バケットリスト】を選択し、【バケットの作成】をクリックして、近くのリージョンのCOSバケットを作成します。

![](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. 出力タイプとしてHLS_ARCHIVEを選択します。StreamLiveコンソールに戻り、出力を設定するときに、出力タイプとしてHLS_ARCHIVEを選択します。

![](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. StreamLiveのCOSバケットへのアクセス権を付与します。StreamLiveにCOSバケットへのアクセス権を付与していない場合、COS宛先フィールドはグレー表示になり、入力ができません。プロンプトで【click here】をクリックして、権限付与プロンプトボックスにジャンプします。【Authorize Now】をクリックして、権限付与インターフェースに移動します。【Grant】をクリックして権限付与を完了します。

![](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png)

![](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

権限付与が完了したら、StreamLiveインターフェースに戻り、【Authorization completed】を選択します。この時点で、COS Destinationフィールドに入力できるようになります。

![](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png)

![](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. COSアーカイブアドレスを入力します。作成したCOSバケットに基づいてCOSアーカイブアドレスを入力できます。形式は次のとおりです。http://<BucketName-APPID>.cos.<Region>.myqcloud.com/path

5. 設定を保存して送信します。この時点で、引き続きセクション【四-4】の残りのchannel構成を完了し、送信・保存することができます。

### 6.   StreamLiveを介したTencent Cloud StreamPackageへの出力

StreamLiveは、Tencent Cloud StreamPackageと直接組み合わせて一緒に使用し、HLS/DASH形式のCSSストリームを同じアカウントのStreamPackageへ直接出力します。これにより、ユーザーは独自のオリジンサーバーを構築することで、次のステップのビデオ配信と再生を行うことができます。

1. StreamPackageのアクティブ化

StreamPackageへエクスポートする前に、[StreamPackageサービスをアクティブ化して](https://console.cloud.tencent.com/mdp/channel)、Channelを作成してください。

2. StreamPackageのChannel作成の完了

左上の【Create Channel】をクリックしてチャネルを作成し、チャネル名とStreamLiveの出力タイプに合わせたプロトコルを入力します。例えば、StreamLiveが出力タイプとしてHLS_StreamPackageを選択する場合、ここではHLSを選択します。

>! StreamLiveとStreamPackageは同じリージョンにある必要があります。

![](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

3. Endpointの作成

Channelの作成を完了した後、Channelの詳細画面に進みます。この時点で、Endpointノードを作成します。業務上の実際のニーズに応じて、IPブラックリスト/ホワイトリストまたは認証機能を有効にするかどうか選択することもできます。

![](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

4. EndpointアドレスとChannel IDの取得

作成完了後のEndpointのURLは、再生/オリジンサーバーのアドレスになります。

![](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>? Channel IDは、StreamLive出力の入力に用いられます。
![](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

5. 出力タイプをHLS_STREAMPACKAGまたはDASH_STREAMPACKAGEに選択

StreamLiveコンソールに戻り、出力を設定するときに、出力タイプとしてHLS_STREAMPACKAGEまたはDASH_STREAMPACKAGEを選択します（これは業務上の実際のニーズや作成したばかりのStreamPackageのChannelタイプによって異なります）。次に、StreamPackageにChannel IDを入力すれば完了です。

![](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

6. 設定を保存して送信します。この時点で、セクション【四-4】の残りのChannel構成を完了し、送信・保存が可能になります。

### 7.   チャネルのインポート・エクスポート、クローン作成および編集・削除

StreamLiveは、チャネル構成ファイルのエクスポート/インポートとチャネルのクローン機能により、チャネルの作成をすばやく完了する業務をサポートしています。

1. チャネルのエクスポート

StreamLiveの【Channel Management】インターフェースには、作成したすべてのチャネルとそのステータスが表示されます。右側の【Export】ボタンをクリックすると、チャネル構成jsonファイルをすばやくエクスポートできます。

![](https://main.qcloudimg.com/raw/764c7eea7b0ea222364a5b4dad88eb41.png)

![](https://main.qcloudimg.com/raw/e67829bbee59c2148ba68ae1e652f8da.png)

2. チャネルのインポート

【Channel Management】インターフェースを開き、【Create Channel】ボタンをクリックして【Import Configuration】を選択し、変更したチャネル構成jsonファイルを選択して保存します。

jsonファイルを送信した後、チャネル編集ステータスに入るので、続いて通常の構成プロセスに従ってチャネルを保存して送信すれば完了です。

![](https://main.qcloudimg.com/raw/1fe8fdf4c50c5be5a6fe1dc820f5469f.png)

>?
>- チャネルインポート機能とは、実際はクイック入力プロセスです。インポートしたjsonファイルに基づいて、【Basic Information】、【Output Group Setting】という2つの部分の内容が自動的に入力されます。【Input Setting】部分は無視されますので、Inputを再選択する必要があります。従って、この方法ですばやくChannelを作成する必要がある場合は、あらかじめ新しいinputを作成できます。
>- チャネルの編集時に新しい構成ファイルをインポートすると、元のチャネル構成情報が上書きされます。

3. チャネルクローン

チャネルクローンの本質とは、特殊なチャネルのエクスポート/インポートのすばやい操作です。【Channel Management】インターフェースを開き、【Operation】の下の【Clone】をクリックすれば、クローンチャネルの構成ステータスに進めます。

このとき、チャネルは作成されたクローンチャネルの基本情報（【Input Setting】部分を除く）を自動的に入力し、通常の構成プロセスに従ってチャネルを保存して送信します。

![](https://main.qcloudimg.com/raw/92bf580af5c4f013363915688744f1f6.png)

4. チャネルの編集と削除

【RUNNING】プロセスではチャネルの編集・削除はできませんので、まず【Stop】チャネルの編集/削除操作を行ってください。

![](https://main.qcloudimg.com/raw/57923bc62f83d99ee10df572bebbb6e3.png)

### 8.   チャネル品質のモニタリング

【Channel Management】インターフェースを開き、チャネル名をクリックしてチャネル詳細画面に進みます。チャネルの詳細画面には、チャネル情報、入力、出力、Alerts、Healthなどの詳細情報が表示されます。

![](https://main.qcloudimg.com/raw/c97468a3a9fbeb51e9c15ae552d53efd.png)

いずれかのチャネルのいずれかのパイプラインで問題または潜在的な問題が発生すると、StreamLiveはそのチャネルのアラームを生成します。Set timeはアラーム発生時のイベント、Cleared timeはアラームがキャンセルされた時間です。 同じアラーム記録にステータスが更新されます。アラーム記録がSETステータスの場合、Set time、Stateは赤で表示されます。アラーム記録が削除されると、ステータスがCLEAREDになると同時に、上記の赤い表示は消えます。アラームは、問題が発生したパイプライン、アラームタイプおよび詳細情報を明確に記録します。データクエリーは過去5日間のみクエリーを実行でき、クエリー期間は24時間未満です。

キャンセル前：

![](https://main.qcloudimg.com/raw/a76c4bb27dd86c6e2d06f2dd6ccbb42e.png)

キャンセル後：

![](https://main.qcloudimg.com/raw/4a986687ccdf97ce0e222aac2b936fb6.png)

Heathはユーザーに対し、チャネル入力（帯域幅・入力ビデオフレームレート・入力オーディオフレームレート）と出力（帯域幅）の情報および対応するグラフを提供して、現在のチャネルが正しく機能しているかどうか判断します。データクエリーは過去5日間のみクエリーを実行でき、クエリー期間は24時間未満です。

![](https://main.qcloudimg.com/raw/e49e312b0d134d0d9fb1c8dccbcee00b.png)

![](https://main.qcloudimg.com/raw/de84757254338b428e55695b4b3a2170.png)

 

### 9.   タイムプランの設定

StreamLiveチャネルにタイムプランを設定し、プッシュ中の予定時間に特定イベントをトリガーする設定を実装することができます（例：15:00:00に入力ソースをinput2に切り替える）。

【Channel Management】インターフェースを開き、チャネル名をクリックしてチャネル詳細画面に進み、【Plan】を選択し、【Add】をクリックしてイベントを追加します。

1. 2種類のトリガー時間のモードを選択することができます。Fixed Timeは手動で日付と時間の設定が必要で、イベントは設定された時間に実行されます。Immediateは現在のセットアップタイムをトリガー時間とし、すぐにイベントが開始されます。

2. イベントタイプは現在「入力ソースの切り替え」機能のみをサポートしており、その対象となる入力ソースを選択することができます。

【create】をクリックして、時間-イベントの作成を完了します。

![](https://main.qcloudimg.com/raw/b45ec0b7275bc1c4363bd683652dd541.png)

![](https://main.qcloudimg.com/raw/cb4c8a9d4f289072476364297346fb4d.png)

>!
>- 入力する時間はお客様が所在する現地時間です。現在より早い時間を入力することはできません。
>- 切り替えたMP4_PULL (またはHLS_PULL)入力ソースのストリーム設定がONCEの場合、一度プルした後で入力ストリームは自動的に切断され、その後のイベントはトリガーされません。

作成されたすべてのイベントが「トリガー時間」の時系列によって上から順に並べられ、イベントを閲覧、削除、追加することができます。

>! 作成済みイベントの編集操作はサポートしていません。

 

