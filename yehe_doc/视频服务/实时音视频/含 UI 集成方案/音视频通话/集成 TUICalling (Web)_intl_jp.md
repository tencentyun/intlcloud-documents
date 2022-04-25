## コンポーネントの説明
TUICallingコンポーネントはオープンソースのオーディオビデオコンポーネントです。デスクトップブラウザで**ビデオ通話**機能をスピーディーに統合でき、オンライン診療、オンラインカスタマーサービス、リモート査定などのシーンに最適です。
<table class="tablestyle">
<tbody><tr>
<td style="vertical-align: top;"><img src="https://qcloudimg.tencent-cloud.cn/raw/4bac4a925d537c29f1540fa90d570552.png"></td>
<td style="vertical-align: top;"><img src="https://qcloudimg.tencent-cloud.cn/raw/eb1bcfd34409315b3bda70e72d5420f4.png"></td></tr><tr>
<td style="vertical-align: top;"><img src="https://qcloudimg.tencent-cloud.cn/raw/83e4ec55c1feb43c2ef68863a6b4beae.png"></td>
<td style="vertical-align: top;"><img src="https://qcloudimg.tencent-cloud.cn/raw/17bb3c8f1f49a4c1f100536bee37caef.png"></td>
</tr>
</tbody></table>


#### その他のプラットフォーム
Web版のTUICallingのほか、Android、iOS、Flutter、Uniappなどのプラットフォーム用のソースコードも同時リリースしています。このうちAndroid、iOS版のTUICallingは「着信通知」機能をサポートしています。

>?
>- **Web版のTUICallingのほか、Android、iOS、Flutter、Uniappなどのプラットフォーム用のソースコードも同時リリースしています。このうちAndroid、iOS版のTUICallingは「着信通知」機能をサポートしています。** 
ご質問やご提案がありましたら、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)までお願いいたします。

## コンポーネントの統合

[](id:step1)
### ステップ1：SdkAppIdと署名キーの取得
- Tencent Cloudアカウントをまだお持ちでない場合は、Tencent Cloudアカウントをご登録の上、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了してください。完了すると、TRTC管理コンソールの[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)画面にリダイレクトされます。
- アプリケーションリストが空の場合は、**アプリケーションの作成**ボタンをクリックして新しいアプリケーションを作成し、**アプリケーション管理**をクリックしてアプリケーション管理画面を開きます。この画面で**クイックマスター**タブを開くと、次のような画面を見ることができます。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png" width="700">
- **SDKAppID**：TRTCのアプリケーションIDです。業務の分離、すなわち異なるSDKAppIDの通話が互いに接続できないようにするために用いられます。
- **Secretkey**：TRTCのアプリケーションキーです。SDKAppIDとペアで使用する必要があり、TRTCサービスを正当に使用するための認証用証明書UserSigの算出に用いられます。このKeyは次のステップ5で使用します。

[](id:step2)
### ステップ2：TRTCCallingコンポーネントのダウンロードと統合
クリックして[Github](https://github.com/tencentyun/TUICalling)に進み、コードのクローン/ダウンロードを選択します。Webディレクトリ下の実装をご参照ください。

>?
>- 0.6.0以降は、[trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk)、[tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk)および[tsignaling](https://www.npmjs.com/package/tsignaling)の依存関係を手動でインストールする必要があります。
>- trtc-calling-js.jsのボリュームを縮小し、アクセス側で使用されているtrtc-js-sdk、tim-js-sdkおよびtsignalingのバージョン競合を回避するために、trtc-calling-js.jsは、外部依存関係としてtrtc-js-sdk、tim-js-sdk、tsignalingをパッケージ化しているので、使用する前に依存関係を手動でインストールする必要があります。

<dx-codeblock>
::: javascript javascript
// npm方式でのインストール
  npm install trtc-js-sdk --save

  npm install tim-js-sdk --save

  npm install tsignaling --save

  npm install trtc-calling-js --save
:::
</dx-codeblock>

<dx-codeblock>
::: html html
//スクリプト方式によってtrtc-calling-jsを使用する必要がある場合は、順序どおりに次のリソースをインポートする必要があります。

<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tsignaling.js"></script>
<script src="./trtc-calling-js.js"></script>
:::
</dx-codeblock>

[](id:step3)
### ステップ3：TRTCCallingオブジェクトの新規作成
TRTCCallingオブジェクトを新規作成し、SDKAppIDパラメータをお客様のSDKAppIDに設定します。
```javascript
// Web/src/trtc-calling/index.jsをご参照ください
import TRTCCalling from 'trtc-calling-js';

let options = {
	SDKAppID: 0, // アクセスするときは、0をお客様のSDKAppIDに置き換える必要があります。
	// v0.10.2から、timパラメータを追加します
	// timパラメータはサービス内にすでに存在するTIMインスタンスに使用され、TIMインスタンスの一意性を保証します。
	tim: tim
};
const trtcCalling = new TRTCCalling(options);
```

[](id:step4)
### ステップ4：ログインとイベント監視
```javascript
// Web/src/components/login/index.vueをご参照ください
trtcCalling.login({
	userID,
	userSig,
});

// Web/src/App.vueをご参照ください

export default {
	name: "App",
	components: {
	},
	async created() {
		this.initListener();
	},
	data() {
		return {};
	},
	destroyed() {
		this.removeListener();
	},
	methods: {
		initListener: function() {
			// リモートユーザーが呼び出し
			trtcCalling.on(trtcCalling.EVENT.INVITED, this.handleNewInvitationReceived);
			// リモートユーザーが応答
			trtcCalling.on(trtcCalling.EVENT.USER_ACCEPT, this.handleUserAccept);
			// リモートユーザーが拒否
			trtcCalling.on(trtcCalling.EVENT.REJECT, this.handleInviteeReject);
			// ...
		},
		removeListener: function() {
			trtcCalling.off(trtcCalling.EVENT.INVITED, this.handleNewInvitationReceived);
			trtcCalling.off(trtcCalling.EVENT.USER_ACCEPT, this.handleUserAccept);
			trtcCalling.off(trtcCalling.EVENT.REJECT, this.handleInviteeReject);
		},
		handleNewInvitationReceived: async function(payload) {
		},
		handleUserAccept: function() {
		},
		handleInviteeReject: function() {
		}
	}
}
```

[](id:step5)
### ステップ5：1v1通話の実現
- **発呼者：特定ユーザーを呼び出す**
```javascript
// Web/src/components/video-call/index.vueまたはWeb/src/components/audio-call/index.vueをご参照ください
trtcCalling.call({
  userID,  //ユーザーID
  type: 2, //通話タイプ。0-不明、1-音声通話、2-ビデオ通話
  timeout  //招待タイムアウト時間、単位s（秒）
});
```
- **着呼者：新しい呼び出しに応答**
```javascript
// Web/src/App.vue handleAcceptCallメソッドをご参照ください
// 応答
trtcCalling.accept();
// 拒否します
trtcCalling.reject()
```
- **ローカルカメラのオン**
```javascript
trtcCalling.openCamera()
```
- **リモートビデオ画面の表示**
```javascript
trtcCalling.startRemoteView({
  userID, //リモートユーザーID
  videoViewDomID //このユーザーデータはDOM IDノードにレンダリングされます
})
```
- **ローカルプレビュー画面の表示**
```javascript
trtcCalling.startLocalView({
  userID, //ローカルユーザーID
  videoViewDomID //このユーザーデータはDOM IDノードにレンダリングされます
})
```
- **通話の終了**
```javascript
trtcCalling.hangup()
```

## よくあるご質問

### 通話がつながらなかったり、強制オフラインになったりするのはなぜですか。
コンポーネントは現在、マルチインスタンスのログインや**オフラインプッシュのシグナリング**機能をサポートしていません。現在のログインアカウントの一意性をご確認ください。
> ?
> - **マルチインスタンス**：1つのUserIDで繰り返しログインしたり、異なるターミナルからログインしたりすると、シグナリングの混乱が生じます。
> - **オフラインプッシュ**：インスタンスはオンラインの場合にのみメッセージを受信できます。インスタンスがオフラインのときに受信したシグナリングは、オンラインになった後は再度プッシュされません。

### 環境についてはどのような要件がありますか。
最新バージョンのChromeブラウザをご使用ください。現在、デスクトップのChromeブラウザはTRTC Web SDKをサポートしており、関連機能は比較的整っていますので、Chromeブラウザを使用して体験することをお勧めします。

- TRTCCallingは以下のポートに依存してデータ送信を行っていますので、これらをファイアウォール・ホワイトリストに追加してください。設定が完了したら、[公式サイト Demo](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html)にアクセスして体験していただけば、設定が有効かどうかチェックすることができます。
- **TCPポート**：8687
- **UDPポート**：8000，8080，8800，843，443，16285
- **ドメイン名**：qcloud.rtc.qq.com。より詳細な説明をご覧になる場合は、[ファイアウォール制限の対応関連](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。
- **プラットフォームサポート**：現在、このソリューションは次のプラットフォームをサポートしています。
<table>
<thead><tr><th>オペレーティングシステム</th><th>ブラウザタイプ</th><th>ブラウザの最小バージョン要件</th></tr></thead>
<tbody><tr>
<td>Mac OS</td>
<td>デスクトップ版Safariブラウザ</td>
<td>11+</td>
</tr><tr>
<td>Mac OS</td>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
</tr><tr>
<td>Mac OS</td>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
</tr><tr>
<td>Mac OS</td>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版QQブラウザ（クイックコア）</td>
<td>10.4+</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
</tr>
</tbody></table>

>? 詳細な互換性の照会については、[ブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)をご参照ください。また、[TRTC検査ページ](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)でオンライン検査することも可能です。

- **URLドメイン名プロトコルの制限**：
<table>
<thead><tr><th>ユースケース</th><th>プロトコル</th><th>受信（再生）</th><th>送信（マイク・オン）</th><th>画面共有</th><th>備考</th></tr></thead>
<tbody><tr>
<td>本番環境</td>
<td>HTTPSプロトコル</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>推奨</td>
</tr><tr>
<td>本番環境</td>
<td>HTTPプロトコル</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>-</td>
</tr><tr>
<td>ローカル開発環境</td>
<td>http://localhost</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>推奨</td>
</tr><tr>
<td>ローカル開発環境</td>
<td>http://127.0.0.1</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>-</td>
</tr><tr>
<td>ローカル開発環境</td>
<td>http://[ローカルマシンIP]</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>-</td>
</tr><tr>
<td>ローカル開発環境</td>
<td align="left">file:///</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>-</td>
</tr>
</tbody></table>

### その他のよくあるご質問
[TRTCCalling webに関するご質問](https://intl.cloud.tencent.com/document/product/647/43096)をご参照ください。
