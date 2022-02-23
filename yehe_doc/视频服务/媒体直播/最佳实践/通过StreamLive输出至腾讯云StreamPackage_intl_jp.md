StreamLiveは、Tencent Cloud StreamPackageと直接組み合わせて一緒に使用し、HLS/DASH形式のCSSストリームを同じアカウントのStreamPackageへ直接出力します。これにより、ユーザーは独自のオリジンサーバーを構築することで、次のステップのビデオ配信と再生を行うことができます。

### StreamPackageのアクティブ化

StreamPackageへ出力する前に、[StreamPackageサービスをアクティブ化](https://console.cloud.tencent.com/mdp/channel)して、Channelを作成してください。

### StreamPackageのChannel作成の完了

左上の【Create Channel】をクリックしてチャネルを作成し、チャネル名とStreamLiveの出力タイプに合わせたプロトコルを入力します。例えば、StreamLiveが出力タイプとしてHLS_StreamPackageを選択する場合、ここではHLSを選択します。

>! StreamLiveとStreamPackageは同じリージョンにある必要があります。

![img](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

### Endpointの作成

Channelの作成を完了した後、Channelの詳細画面に進みます。この時点で、Endpointノードを作成します。業務上の実際のニーズに応じて、IPブラックリスト/ホワイトリストまたは認証機能を有効にするかどうか選択することもできます。

![img](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

### EndpointアドレスとChannel IDの取得

作成完了後のEndpointのURLは、再生/オリジンサーバーのアドレスになります。

![img](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>? Channel IDは、StreamLive出力の入力に用いられます。

![img](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

### 出力タイプの選択

StreamLiveコンソールに戻り、出力を設定するときに、出力タイプとしてHLS_STREAMPACKAGEまたはDASH_STREAMPACKAGEを選択します（これは業務上の実際のニーズや作成したばかりのStreamPackageのChannelタイプによって異なります）。次に、StreamPackageにChannel IDを入力すれば完了です。

![img](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

### 設定の保存と送信

設定を保存して送信します。このとき、続けて[StreamLiveチャネル管理](https://intl.cloud.tencent.com/document/product/1048/45214)セクションのその他のChannel設定を完了し、送信し保存することができます。
