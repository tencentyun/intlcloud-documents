このドキュメントでは、Gaming Multimedia Engine (GME)を始めたばかりのユーザーに学習方法を提供します。
## 1. GMEを知ります
- [GMEはどのようなサービスを提供していますか、主な機能はなんですか](https://intl.cloud.tencent.com/document/product/607/10835)
- [GMEのメリットは何ですか。](https://intl.cloud.tencent.com/document/product/607/10837)
- [GMEはどのような場面で使用できますか。](https://www.tencentcloud.com/zh/document/product/607/51558)

## 2. GMEの課金モード
GMEはリアルタイム音声サービス、ボイスメッセージサービスなど、さまざまなサービスがあります。課金の詳細については、[購入ガイド](https://intl.cloud.tencent.com/document/product/607/50009)をご参照ください。

## 3. 体験サービス
GMEを使用する前に、製品の効果を体験することができます。

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="37.5%"/></img>


- [基本機能体験Demo](https://intl.cloud.tencent.com/document/product/607/50219)：体験機能には、リアルタイム音声、音声メッセージ、ボイスツーテキスト変換、リアルタイム音声3D効果音、リアルタイム音声基礎ボイス・チェンジなどがあります。
- [3Dリアルタイム音声体験Demo](https://intl.cloud.tencent.com/document/product/607/50220)：リアルタイム音声3Dサウンド機能を体験します。
- [高度なボイス・チェンジ機能Demo](https://intl.cloud.tencent.com/document/product/607/50221)：リアルタイム音声の高度なボイス・チェンジ機能を体験します。


## 4 サービスの有効化
-　Tencent Cloud GMEを使用する前に、[Tencent Cloudアカウントを登録](https://intl.cloud.tencent.com/document/product/378/17985)する必要があります。
- [Tencent Cloud Game Multimedia Console](https://console.cloud.tencent.com/gamegme)でサービスを開始し、必要な機能に応じて、対応する機能サービスを有効化することができます。詳細については[サービスの有効化](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。

## 5 導入パラメータの取得

### クライアント導入パラメータ


1. [Tencent Cloud Game Multimedia Console](https://console.cloud.tencent.com/gamegme)で、作成したアプリケーションを探し、**操作**列で**設定**をクリックして、アプリケーション設定ページに移動します。

2. ページで対応するAppIDと権限キーを取得できます。コンソールでの必要なパラメータのスクリーンショットは次のとおりです。

	- Sample Projectを使用するときは、AppIDと権限キーをパラメータとしてSample Projectに入力する必要があります。
	- SDKを利用する場合、初期化インターフェースInitにはAppIDをパラメータとして、認証インターフェースQAVAuthBuffer.GenAuthBufferには権限キーをパラメータとして渡す必要があります。

### クラウドAPI導入パラメータ
クラウドAPIを使用している場合はSecretIdおよびSecretKeyが必要です。[APIキー管理](https://console.cloud.tencent.com/cam/capi)ページから入手してください。[セキュリティのベストプラクティス](https://www.tencentcloud.com/document/product/598/10592)を参照してアカウントのアクセス管理を行うことをお勧めします。



## 6. Sample Projectのクイック実行
GMEの各プラットフォームにはSDKとSample Projectが用意されています。SampleProjectのクイック実行により、開発者はGME SDKへの導入方法を知ることができます。
### 6.1 Sample Projectのダウンロード
[ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)で必要なプラットフォームのSample Projectをダウンロードできます。


### 6.2 Sample Projectのクイック実行
ご使用のプラットフォームにあわせたドキュメントをご参照ください。
[UnrealEngine Sample Projectのクイック実行](https://intl.cloud.tencent.com/document/product/607/46014)

## 7. 導入基礎機能
### 7.1 SDKのダウンロード
[ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)で必要なプラットフォームのSDKファイルをダウンロードできます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b04f51788ab7bd527ef1662c5c5f7675.png"  width="50%"/></img>

### 7.2 プロジェクトの構成
各プラットフォームドキュメントを参照してプロジェクトを設定し、インターフェースを呼び出してGMEサービスを使用するには、設定が完了してください。

| プラットフォーム | 構成ファイル |
|---------|---------|
| Unity | [統合SDK](https://intl.cloud.tencent.com/document/product/607/10783) |
| Unreal Engine | [統合SDK](https://intl.cloud.tencent.com/document/product/607/44549) |
| Cocos 2D | [プロジェクトの構成](https://intl.cloud.tencent.com/document/product/607/15216) |
| Windows | [プロジェクトの構成](https://intl.cloud.tencent.com/document/product/607/19068) |
| Android | [統合SDK](https://intl.cloud.tencent.com/document/product/607/40859) |
| iOS | [統合SDK](https://intl.cloud.tencent.com/document/product/607/15219) |
| Mac | [プロジェクトの構成](https://intl.cloud.tencent.com/document/product/607/18617) |
| H5 | [プロジェクトの構成](https://intl.cloud.tencent.com/document/product/607/30261) |

### 7.3 SDKのクイック導入
クイック導入ドキュメントにより、導入手順を簡素化し、体験機能の迅速な導入を可能にします。クイック導入ドキュメントで説明されている機能には、リアルタイム音声、ストリーミングボイスツーテキスト変換などがあります。

| プラットフォーム | クイック導入ドキュメント |
|---------|---------|
| Unity | [Unity SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/44544) |
| Unreal Engine | [Unreal SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/44545) |
| Windows、iOS、Mac、Android | [Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858) |



###　7.4　基本機能の詳細導入
ご使用のプラットフォームに合わせて、[クリック](https://www.tencentcloud.com/document/product/607/10780)して適切なドキュメントを探して導入を行います。


###　7.5　支援ドキュメントの導入
使用される可能性のあるドキュメント：

| ドキュメント | いつ使用する |
|---------|---------|
| [音質選択](https://intl.cloud.tencent.com/document/product/607/18522) | リアルタイムな音声ルームタイプを選択するのは困難である場合、このドキュメントをご参照ください。 |
| [認証キー](https://intl.cloud.tencent.com/document/product/607/12218) | ご使用するアプリケーションGMEサービスに関する認証配置の安全性を高くする場合。 |
| [SDKバージョンアップガイド](https://intl.cloud.tencent.com/document/product/607/32363) | GMEの以前のバージョンから新しいバージョンにアップグレードするにはインターフェースの変更点についてこのドキュメントを参照する必要があります。|
| [エラーコード](https://intl.cloud.tencent.com/document/product/607/33223) | SDK導入・デバッグでインターフェースまたはコールバックからエラーコードが返された場合、このドキュメントで解決してください。|

##　8.ステップアップ機能の導入


<table>
<thead>
<tr>
<th>次のことをする場合</th>
<th>これを読むことができます</th>
</tr>
</thead>
<tbody>
<tr>
<td>リアルタイム音声サービスにおいて、範囲音声効果（PUBGのようなゲームのグローバル・チーム音声効果など）を実装します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/17972" target="_blank">範囲音声</a></td>
</tr>
<tr>
<td>ゲームキャラクターの位置移動に応じてキャラクタの発話音声に方位によるステレオ効果が感じられ、距離に応じた遠近の音声にも減衰効果があり、ゲーム音声に没入感を持たせることができます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3Dサウンド</a></td>
</tr>
<tr>
<td>ゲーム中のリーダーがルームの他のプレイヤーのマイクをオフにしようとしたり、ゲームのキャスターが聴衆にマイクをオンにしようとしたりするなど、ルームメンバーの管理やルームメンバーのマイクオン/マイクオフ、マイクミュートの管理をSDKインターフェースで実現します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/51115" target="_blank">ルーム管理機能</a></td>
</tr>
<tr>
<td>GMEを利用してリアルタイム音声ルームで伴奏を再生し、伴奏のEQを調整し、ローカル効果音を再生します。</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">リアルタイム音声伴奏</a>、<a href="https://intl.cloud.tencent.com/document/product/607/31503" target="_blank">リアルタイム音声効果音</a>、<a href="https://www.tencentcloud.com/document/product/607/46716" target="_blank">リアルタイム音声イコライザ</a></td>
</tr>
<tr>
<td>リアルタイムの音声を変声化し、「オヤジ音」や「ロリ音」などに音色を調整して面白さを増すことができます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/44995" target="_blank">ボイス・チェンジ</a></td>
</tr>
<tr>
<td>リアルタイム音声ルームでは、すでに自チームがあり、他のプレイヤー達が組んだマッチングチームにマッチングした場合、自分の話を自チームの人しか聞こえながら、マッチングチームのプレイヤーの声を聞きたいと思っている場合。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/39525" target="_blank">オーディオ転送ルーティング</a></td>
</tr>
<tr>
<td>音声認識を通じて、未成年人のゲーム内でのボイスチャットを認識し、実名認証と中毒防止システムをバイパスする問題を解決します</td>
<td>未成年人音声認識</td>
</tr>
<tr>
<td>リアルタイム音声、音声ファイルおよび音声メッセージに含まれる、わいせつ、暴力、暴言、広告、その他の機密情報または好ましくない情報を認識します。</td>
<td>リアルタイム音声の審査、音声メッセージ審査、サードパーティの音声ストリーミングまたは音声ファイルの審査</td>
</tr>
<tr>
<td>プレイヤーのリアルタイム音声ストリームをテキストに変換し、リアルタイムの字幕の効果を演出します。</td>
<td>リアルタイム音声からテキストへ変換</td>
</tr>
</tbody></table>


## 9. コンソール運用ガイド
リアルタイムの音声、音声メッセージなどサービスの使用量データの確認については、[使用量確認](https://intl.cloud.tencent.com/document/product/607/44548)をご参照ください。

## 10. よくあるご質問
####　機能に関する質問
[GMEのリアルタイム音声を使用するときのトラフィック消費量はどのくらいですか。](https://intl.cloud.tencent.com/document/product/607/39519)
[GMEにはどのような機能がありますか。](https://intl.cloud.tencent.com/document/product/607/39520)
[GMEリアルタイム音声のルーム数と人数には制限がありますか？](https://intl.cloud.tencent.com/document/product/607/39523)

#### 開発プロセスの問題
[GMEはOpenIdを1つだけ使用できますか。](https://intl.cloud.tencent.com/document/product/607/39521)
[ダウンロードしたDemoの使用方法。](https://intl.cloud.tencent.com/document/product/607/39521)
[GME SDKを統合してApkをエクスポートすると、起動プログラムに黒画面が表示されます。どうすれば解決できますか？](https://intl.cloud.tencent.com/document/product/607/39522)
[Xcodeが実行可能ファイルをエクスポートするときにGMESDK.frameworkライブラリが追加されました。コンパイル時にコンパイルエラーが報告されました。どうすれば解決できますか？](https://intl.cloud.tencent.com/document/product/607/39522)
[GME SDKのpoll関数はいつから呼び出されますか？](https://intl.cloud.tencent.com/document/product/607/30254)



## 11. 導入問題の出現

申し訳ありませんが、導入プロセスで問題が発生した場合は、次の点を参考にして解決してください。

### 判断問題
まず、問題の種類を判断します。問題の種類に応じて、[認証問題](https://intl.cloud.tencent.com/document/product/607/39824)、[Demo使用問題](https://intl.cloud.tencent.com/document/product/607/39521)、[ネットワーク問題](https://intl.cloud.tencent.com/document/product/607/39519)、または[プロジェクトエクスポートの問題](https://intl.cloud.tencent.com/document/product/607/39522)をご参照ください。

また、使用しているサービスに応じて、問題の関連ドキュメントを判断します。

| 使用しているサービス  | 閲覧できるドキュメント |
|---------|---------|
| リアルタイム音声サービス | [リアルタイム音声の入室失敗問題](https://intl.cloud.tencent.com/document/product/607/39523)、[リアルタイム音声の無音とオーディオ問題](https://intl.cloud.tencent.com/document/product/607/39524) |
| 音声メッセージサービス | [音声メッセージサービス問題](https://intl.cloud.tencent.com/document/product/607/39716)|
| ボイスツーテキスト変換サービス | [ボイスツーテキスト変換問題](https://intl.cloud.tencent.com/document/product/607/39716)|

###　エラーコード
[エラーコード](https://intl.cloud.tencent.com/document/product/607/33223)を使用して解決します。呼び出しエラーが発生した場合は、対応するエラーコード値の原因と解決方法を確認できます。

例：SDKを使用する際に、3Dサウンド関連インターフェースを呼び出した後、インターフェースから7003のエラーが返されました。エラーコードのドキュメントを確認すると、このエラーコードの原因がInitSpatializerが呼び出されていないためであることがわかります。この推奨事項に基づいて、コード内でInitSpatializerが呼び出されているかどうか、および呼び出された順序が正しいかどうかを調べてください。



###　助けを求める
ドキュメントとエラーコードで問題を解決できない場合は、[問題解決ガイド](https://www.tencentcloud.com/document/product/607/51562)を参照して開発者に問い合わせてください。


## 12.　交流と提案
GMEの製品およびサービスを使用する上で何らかの質問やアドバイスがある場合は、以下の方法でフィードバックをお願いします。後ほど専門スタッフがお客様の質問に回答します。
- 製品のドキュメントの間違い等を発見した場合（リンク先、内容、APIエラーなど）は、ドキュメントのページ右側の**ドキュメントに関するフィードバック**をクリックするか、または問題が存在するコンテンツを選択してフィードバックしてください。
-　製品に関する問題について、[オンラインカスタマーサービス](https://intl.cloud.tencent.com/contact-sales)にお問い合わせください。
