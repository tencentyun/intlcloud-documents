ここではTUICallKitのクラウドレコーディングを起動し、重要な通話の保存、審査などに役立てる方法についてご説明します。[自動レコーディングソリューション](#Option1)と[REST APIレコーディングソリューション](#Option2)という2つのソリューションをご用意しています。

>? TUICallKitはTencent Cloudの基本的なPaaSサービスを複数統合しています。このうち、オーディオビデオ関連機能は[TRTC](https://www.tencentcloud.com/document/product/647/35078)に依存しています。このためTUICallKitのクラウドレコーディング機能は[TRTCコンソール](https://console.tencentcloud.com/trtc/app)で設定する必要があります。

[](id:Option1)
### 方法1：自動レコーディングソリューション（推奨）

自動レコーディングソリューションの使用を推奨します。業務側でレコーディングを起動および停止する必要がなく、レコーディングタスクはTencent Cloud TRTCバックエンドが管理します。通話中にオーディオビデオストリームのアップストリームがあれば自動的にレコーディングし、**スピーディーかつ簡単にアクセスできます**。次のいくつかの手順で完成させることができます。 

1. [TRTCコンソール > アプリケーション管理](https://console.tencentcloud.com/trtc/app)でSDKAppIdに対応するアプリケーションを見つけ、機能設定ページに進みます。

2. 機能設定ページでクラウドレコーディング設定のカードを確認できます。**クラウドレコーディング機能を有効に**した後、**Global Auto-Recordingテンプレートの作成**をクリックします。![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. オーディオビデオ通話の業務シナリオ（1v1通話、グループ通話）に応じて、次のようにパラメータを設定することを推奨しますが、ご自身の業務ニーズに応じてカスタムレコーディングテンプレートを設定することも可能です。![img](https://qcloudimg.tencent-cloud.cn/raw/8f8a9d9d029d63fa2d70c1105630aa20.png)

>! グローバルレコーディングがサポートする最大ミクスストリーミング人数は8人です。通話人数が8人を超える場合（自分を含めて）、最後のユーザーのストリームはレコーディングされません。

Global Auto-Recording機能を有効にすると、通話応答後かつオーディオビデオアップストリームが存在する場合にレコーディングタスクの自動起動がトリガーされ、通話終了後に自動的にレコーディングが停止します。ネットワークまたはその他の異常によって退室になった場合、ご自身の設定したMaxIdleTime値（アイドル状態の待機時間。デフォルトでは5秒）に基づいてバックエンドが自動的にレコーディングタスクを停止し、それ以上の料金ロスが発生しないようにします。

4. **テンプレートの作成が完了した後、**Global Auto-Recordingにチェックを入れれば完了です。 

[](id:Option2)

## 方法2：REST APIレコーディングソリューション

自動レコーディングソリューションで業務ニーズを満たせない場合は、よりフレキシブルなREST APIレコーディングソリューションを使用することもできます。レコーディングサブスクリプションルーム内のキャスターの指定、ミクスストリーミングレイアウトのカスタマイズ、レコーディング中のレイアウトおよびサブスクリプション更新などが可能ですが、**業務バックエンドサービスとの組み合わせが必要で、接続がより複雑になり、機能は強力になります。重要な手順は次のとおりです**。

1. [TRTCコンソール > アプリケーション管理](https://console.tencentcloud.com/trtc/app)でSDKAppIdに対応するアプリケーションを見つけ、機能設定ページに進みます。

2. 機能設定ページでクラウドレコーディング設定のカードを確認できます。**クラウドレコーディング機能を有効にする**と、この時点で**レコーディングを手動でカスタマイズ**、すなわちREST APIモードにデフォルトでチェックが入っています。![img](https://qcloudimg.tencent-cloud.cn/raw/8ea4cb2a816edfdc7e26816505a75eca.png)

3. その後、REST API（[CreateCloudRecording](https://www.tencentcloud.com/document/product/647/46960)）を呼び出してクラウドレコーディングを起動することができます。ここでは[TUICallObserver](https://www.tencentcloud.com/document/product/647/51007)の通知イベントを監視することで、オーディオビデオ通話の開始時にレコーディングを起動できるようにすることをお勧めします。Javaコードの例を挙げます。

```java
TUICallEngine.createInstance(context).addObserver(new TUICallObserver() {
    @Override
    public void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole) {
        // REST APIを使用してレコーディングタスクを起動することを業務バックエンドに通知します。
    }
});
```

4. クライアントにネットワーク不良、プロセスキルなどが発生して通話が異常終了する可能性を考慮し、レコーディング終了の方法については、TRTCルームステータスのコールバック（詳細については[サーバーイベントコールバックの監視](https://www.tencentcloud.com/document/product/647/39558)をご参照ください）をサブスクライブし、TRTCルームのステータスが解散となったコールバックを受信した時点でREST API （[DeleteCloudRecording](https://www.tencentcloud.com/document/product/647/46959)）を呼び出してクラウドのレコーディングタスクを停止するようにすることをお勧めします。

## よくあるご質問

### 1. レコーディング時間の明細を確認するにはどうすればよいですか。

[TRTCコンソール > クラウドレコーディング](https://console.tencentcloud.com/trtc/statistics/cloud-record)でレコーディングの時間明細を確認できます。

### 2. レコーディングしたファイルを確認するにはどうすればよいですか。

[VODコンソール](https://console.tencentcloud.com/vod)にログインし、左側ナビゲーションバーで**メディア資産管理**を選択し、リスト上方の**プレフィックス検索**をクリックして**プレフィックス検索**を選択し、検索ボックスにキーワードを入力します。レコーディングファイルの命名ルールは次のとおりです。

- シングルストリーミングレコーディングMP4ファイル名のルール： `<SdkAppId>_<RoomId>_UserId_s_<UserId>_UserId_e_<MediaId>_<Index>.mp4`
- ミクスストリーミングレコーディングMP4ファイル名のルール： `<SdkAppId>_<RoomId>_<Index>.mp4`