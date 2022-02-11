## Tencent Real-Time Communicationの簡単な紹介

- [サポートされているプラットフォーム](https://intl.cloud.tencent.com/document/product/647/35078)
- [サポートされている機能](https://intl.cloud.tencent.com/document/product/647/35428)
- [ユースケース](https://intl.cloud.tencent.com/document/product/647/37713)
- [基本コンセプト](https://intl.cloud.tencent.com/document/product/647/37714)

## 課金モード

Tencent Real-Time Communicationは、サービスタイプに応じて**基本サービス**と**付加価値サービス**の2つのタイプに分かれます。 

<table>
<tr><th>サービスタイプ</th><th>ユースケース</th><th>課金説明</th></tr>
<tr>
<td rowspan="4">基本サービス</td>
<td>音声ILVB</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/647/34610">音声ILVBの課金説明</a></td>
</tr><tr>
<td>ビデオILVB</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/647/34610">ビデオILVBの課金説明</a></td>
</tr><tr>
<td>音声通話</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/647/34610">音声通話の課金説明</a></td>
</tr><tr>
<td>ビデオ通話</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/647/34610">ビデオ通話の課金説明</a></td>
</tr><tr>
<td rowspan="2">付加価値サービス</td>
<td>クラウドレコーディング</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38385">クラウドレコーディングの課金説明</a></td>
</tr><tr>
<td>Cloud MixTranscoding</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38929">Cloud MixTranscodingの課金説明</a></td>
</tr>
</table>



## 開発サポート

## Demo 体験

Tencent Real-Time Communicationでは、**iOS**、**Android**、**Mac OS**、**Windows**、**デスクトップブラウザ**の体験Demoを提供します。詳細については、[Demo 体験](https://intl.cloud.tencent.com/document/product/647/35076)をご参照ください。

### SDKのダウンロード

Tencent Real-Time Communicationは、以下に示すように、**簡易版**、**プロフェッショナル版**、**エンタープライズ版**という3つのSDKバージョンを提供しています。

| バージョンタイプ                                                     | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [簡易版（TRTC）](https://intl.cloud.tencent.com/document/product/647/34615) | TRTCとライブストリーミング（TXLivePlayer）の2つの機能のみが含まれ、アプリパッケージを最小化し、TRTC機能だけを希望されるユーザー向けです。 |
| [プロフェッショナル版（Professional）](https://intl.cloud.tencent.com/document/product/647/34615) | [ MLVB](https://intl.cloud.tencent.com/zh/product/mlvb)や[UGSV](https://intl.cloud.tencent.com/zh/product/ugsv)など、TRTCを含む複数の音声・ビデオ関連のコア機能が含まれます。基盤となるモジュールの多くがサービス間で共有されるため、アプリパッケージのサイズは2つの独立したSDKよりも小さくなります。またシンボルの重複問題もなくなります。|
| [エンタープライズ版（Enterprise）](https://intl.cloud.tencent.com/document/product/647/34615) | プロフェッショナル版のすべての機能に加えて、AIフェイスエフェクトコンポーネント（付加価値サービス）も統合して、デカ目、小顔、美肌、アニメーションステッカー、ウイジェットなどのエフェクトをサポートします。 |

> 各バージョンの違いの比較については、[SDKダウンロード](https://intl.cloud.tencent.com/document/product/647/34615)をご参照ください。



### APIの統合

- **クライアントAPI：** [iOS](https://intl.cloud.tencent.com/document/product/647/35119)、[Mac](https://intl.cloud.tencent.com/document/product/647/35119)、[Android](https://intl.cloud.tencent.com/document/product/647/35125)、[Windows（C++）](https://intl.cloud.tencent.com/document/product/647/35131)、[Unity](https://intl.cloud.tencent.com/document/product/647/40139)、[デスクトップブラウザ](https://intl.cloud.tencent.com/document/product/647/35143)、[Electron](https://intl.cloud.tencent.com/document/product/647/35141)、Flutterを含むプラットフォームでの機能の統合のためにSDKインターフェースの呼び出しをサポートします。
- **サーバーAPI：** [通話品質の監視](https://intl.cloud.tencent.com/zh/document/product/647/36754)、[MixTranscoding](https://intl.cloud.tencent.com/document/product/647/37760)、[ルーム管理](https://intl.cloud.tencent.com/document/product/647/34268)といった機能の統合のためのAPI 3.0インターフェースの呼び出しをサポートします。



## 初心者向け（入門編）

### Demoクイックスタート

Tencent Real-Time Communicationコンソールは、さまざまなプラットフォーム用のDemoソースコードを提供します。具体的な実行方法については、以下をご参照ください。

| プラットフォーム       | 関連ドキュメント                                                     |
| ---------- | ------------------------------------------------------------ |
| iOSおよびMac    | [Demoクイックスタート(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086) |
| Android    | [Demoクイックスタート(Android)](https://intl.cloud.tencent.com/document/product/647/35084) |
| Windows    | [Demoクイックスタート(Windows)](https://intl.cloud.tencent.com/document/product/647/35085) |
| デスクトップブラウザ | [Demoクイックスタート（デスクトップブラウザ）](https://intl.cloud.tencent.com/document/product/647/35607) |
| Electron   | [Demoクイックスタート(Electron)](https://intl.cloud.tencent.com/document/product/647/35089) |
| Flutter | [Demoクイックスタート(Flutter)](https://intl.cloud.tencent.com/zh/document/product/647/39243) |

### SDKクイックインテグレーション

SDKのダウンロードが完了したら、次の方法でTRTC SDKをお客様のプロジェクトにすばやく統合することができます。

| プラットフォーム       | 関連ドキュメント                                                     |
| ---------- | ------------------------------------------------------------ |
| iOS        | [クイックインテグレーション(iOS)](https://intl.cloud.tencent.com/document/product/647/35092) |
| Mac        | [クイックインテグレーション(Mac)](https://intl.cloud.tencent.com/document/product/647/35094) |
| Android    | [クイックインテグレーション(Android)](https://intl.cloud.tencent.com/document/product/647/35093) |
| Windows    | [クイックインテグレーション(Windows)](https://intl.cloud.tencent.com/document/product/647/35095) |
| デスクトップブラウザ | [クイックインテグレーション（デスクトップブラウザ）](https://intl.cloud.tencent.com/document/product/647/35096) |
| Electron   | [クイックインテグレーション(Electron)](https://intl.cloud.tencent.com/document/product/647/35097) |
| Flutter | [クイックインテグレーション(Flutter)](https://intl.cloud.tencent.com/zh/document/product/647/35098) |

### TWebLiveクイックスタート

Tencent Real-Time Communicationは、完全なTWebLive体験Demoを提供します。具体的な統合方法については、[TWebLiveクイックスタート](https://intl.cloud.tencent.com/document/product/647/38172)をご参照ください。

## シーンの実践

Tencent Real-Time Communicationとその他のTencent Cloud製品を組み合わせ、さまざまなタイプのライブストリーミングシーンの体験Demoを提供します。

<table>
<tr><th width="17%">シーンタイプ</th><th>サポートされる機能</th><th width="20%">関連ドキュメント</th>
</tr><tr>
<td>多人数ビデオ通話</td>
<td>インタラクティブなマイク接続、オフライン応答、その他関連機能</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36065" target="_blank">リアルタイムビデオ通話</a></td>
</tr><tr>
<td>多人数音声通話</td>
<td>インタラクティブなマイク接続、オフライン応答、その他関連機能</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36067" target="_blank">リアルタイム音声通話</a></td>
</tr><tr>
<td>ILVB</td>
<td>インタラクティブマイク接続、キャスターPK、低遅延視聴、弾幕チャット、その他関連機能</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36060" target="_blank">ビデオILVB</a></td>
</tr><tr>
<td>リアルタイムインタラクティブ授業</td>
<td>音声、ビデオ、画面共有などの授業方法を含み、さらに教師による質問、学生の挙手、教師による学生の招待、学生の回答、回答の終了、などの関連機能もカプセル化</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37278" target="_blank">リアルタイムインタラクティブ授業</a></td>
</tr><tr>
<td>多人数ビデオミーティング</td>
<td>画面共有、フェイスエフェクト、低レイテンシーでのミーティング、その他関連機能</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37284" target="_blank">多人数ビデオミーティング</a></td>
</tr><tr>
<td>ボイスチャットルーム</td>
<td>マイク管理、低レイテンシーの音声インタラクション、テキストチャット、その他関連機能</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37287" target="_blank">ボイスチャットルーム</a></td>
</tr></table>




入門者のよくあるご質問

-  [クライアントのネイティブSDKは、どのポートまたはドメイン名をホワイトリストに設定する必要がありますか？](https://intl.cloud.tencent.com/document/product/647/35164)
-  [iOS/Androidのインストールパッケージのボリュームを縮小する方法とは？](https://intl.cloud.tencent.com/document/product/647/35165)
-  [UserSigキーを取得する方法とは？](https://intl.cloud.tencent.com/document/product/647/35166)
-  [TRTC簡易版、プロフェッショナル版、エンタープライズ版の違いとは？](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [Tencent Real-Time CommunicationのRoomIDとは？値の範囲は？](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [AndroidとWebの相互通信はサポートされていますか？](https://intl.cloud.tencent.com/document/product/647/37341) 
-  [デスクトップブラウザSDKはどのブラウザをサポートしていますか？](https://intl.cloud.tencent.com/document/product/647/37340) 

> ? その他の質問については、[よくあるご質問](https://intl.cloud.tencent.com/document/product/647/36058)にアクセスしてドキュメントをご確認ください。


## フィードバックおよび助言

Tencent Real-Time Communicationの製品やサービスの使用中にご質問やご提案がある場合は、次のチャネルを通じてフィードバックすることができます。

- 製品のドキュメントの間違い等を発見した場合（リンク先、内容、など）は、ドキュメントのページ右側の【ドキュメントに関するフィードバック】をクリックするか、または問題が存在するコンテンツを選択してフィードバックしてください。
- 製品関連の質問がある場合には、[チケットを提出](https://console.intl.cloud.tencent.com/workorder/category?level1_id=29&level2_id=801&source=14&data_title=Tencent%20Real%20Time%20Communication&step=1) してサポートを求めることができます。
