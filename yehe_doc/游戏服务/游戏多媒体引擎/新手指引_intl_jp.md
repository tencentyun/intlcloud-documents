このドキュメントでは、Gaming Multimedia Engine (GME)を始めたばかりのユーザーに学習方法を提供します。

## 1. GMEを知ります

- [GMEはどのようなサービスを提供しています。](https://intl.cloud.tencent.com/document/product/607/10835)
- [GMEのメリットは何ですか。](https://intl.cloud.tencent.com/document/product/607/10837)
- [GMEの様々なユースケースをご紹介します。](https://intl.cloud.tencent.com/document/product/607/10838)
- [音声のよく使われるコンセプト](https://intl.cloud.tencent.com/document/product/607/30259)

## 2. GMEの課金モード

GMEはリアルタイム音声、ボイスツーテキスト変換、音声分析など、さまざまなサービスがあります。課金の詳細については、[後払いモード](https://intl.cloud.tencent.com/document/product/607/36276)をご参照ください。

## 3. 体験サービス

GMEを使用する前に、Tencent Cloudの製品サービスを体験してください。[Demo体験ドキュメント](https://intl.cloud.tencent.com/document/product/607/38535)でQRコードをスキャンしてモバイル端末のプログラムをダウンロードし、またはWindowsプラットフォームの実行可能プログラムをダウンロードして3D音声効果を体験します。

## 4. 初心者向け（入門編）

#### 4.1 サービスの有効化

GMEを使用する前に、[Tencent Cloudアカウントを登録](https://intl.cloud.tencent.com/document/product/378/17985)し、GMEサービスを有効にする必要があります。詳細については、[音声サービス設定ガイド](https://intl.cloud.tencent.com/document/product/607/39698)をご参照ください。

#### 4.2 アクセスパラメータの取得

GMEを使用してサービスを有効にすると、作成されたアプリ詳細ページで必要なAppIDと権利キーを取得することができます。
- Demoを使用するときは、AppIDと権限キーをパラメータとしてDemoに入力してください。
- SDKを利用する場合、初期化インターフェースInitにはAppIDをパラメータとして、認証インターフェースQAVAuthBuffer.GenAuthBuffer（リアルタイム音声サービス）、ApplyPTTAuthbuffer（ボイスツーテキスト変換サービス）には権限キーをパラメータとする必要があります。

![](https://main.qcloudimg.com/raw/a63f14a7092169c8c9b54cfd21ce4c12.png)
#### 4.3 SDKのダウンロード

[ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)で必要なプラットフォームのSDKファイルをダウンロードできます。**現在、GMEはWindows、Mac、Android、およびiOSプラットフォームに対応し、ゲームエンジンはUnrealEngine4、Unity3D、およびCocos2DX**に対応しています。

現在はH5側でのリアルタイム音声通話に対応しています。

#### 4.4 SDKへのアクセス
各プラットフォームのSDKにアクセスするには、まず各プラットフォームの[プロジェクト設定](https://intl.cloud.tencent.com/document/product/607/10783)ドキュメントをご参照ください。プロジェクト設定が完了したら、対応するプラットフォームの[インターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/15228)のインターフェースを呼び出してGMEサービスを利用いただけます。リアルタイム音声サービスインターフェースの呼び出し順序は、通常【Init初期化】>【Pollによるコールバックのトリガー】>【EnterRoomによる音声ルームへの参加】>【EnableMicによるマイクオン】>【EnableSpeakerによるスピーカーオン】>【ExitRoomによる退室】>【Unitによる初期化解除】となります。

**リアルタイム音声サービスは次のような手順でルームに入ります：**
<img src="https://main.qcloudimg.com/raw/d23fd88b9d0ff2f044f7549168be9d79.png"  width="60%" /></img>

## 5. コンソール運用ガイド
リアルタイムの音声、音声メッセージ、音声分析のバックグラウンドデータについては、[運用ガイド](https://intl.cloud.tencent.com/document/product/607/17448)をご参照ください。

## 6. ドキュメント機能の概要

<table>
<thead>
<tr>
<th>必要であれば、</th>
<th>こちらの</th>
</tr>
</thead>
<tbody><tr>
<td>SDKファイルをダウンロードできます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18521" target="_blank">ダウンロードガイドを読みください</a></td>
</tr>
<tr>
<td>QRコードをスキャンしてアプリをダウンロードし、GMEサービスを体験できます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/38535" target="_blank">Demo体験ドキュメント</a></td>
</tr>
<tr>
<td>プロジェクトにSDKを導入し、プロジェクトからSDKをエクスポートするために必要な設定を確認します。（Unityプラットフォームの例）</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/10783" target="_blank">Unityプロジェクト設定</a></td>
</tr>
<tr>
<td>SDKをプロジェクトに導入し、すべてのインターフェースを調べ、リアルタイム音声サービス、ボイスツーテキスト変換サービスを実装します。（Unityプラットフォームの例）</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/15228" target="_blank">Unityインターフェースドキュメント</a></td>
</tr>
<tr>
<td>SDKをプロジェクトに導入し、リアルタイム音声サービスへのアクセスを迅速に行います。（Unityプラットフォームの例）</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18248" target="_blank">Unityクイックスタート</a></td>
</tr>
<tr>
<td>リアルタイム音声サービスにおいて、範囲音声効果（PUBGのようなゲームのグローバル・チーム音声効果など）を実装します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/17972" target="_blank">範囲音声</a></td>
</tr>
<tr>
<td>ゲームにおける3Dリアルタイム会話効果音を実装します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3Dサウンド</a></td>
</tr>
<tr>
<td>GMEを利用してリアルタイム音声ルーム内で伴奏を再生します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">リアルタイム音声伴奏</a></td>
</tr>
<tr>
<td>リアルタイム音声サービスにおけるルームタイプ別の違いを確認します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18522" target="_blank">音質選択</a></td>
</tr>
<tr>
<td>認証の詳細と、バックグラウンドデプロイプランをさらに理解します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/12218" target="_blank">認証キー</a></td>
</tr>
<tr>
<td>SDKを使用した場合のエラーコードを解析し、解決策を調べます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/33223" target="_blank">エラーコード</a></td>
</tr>
<tr>
<td>GMEに関する製品の問題を確認します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30254" target="_blank">一般的な質問</a></td>
</tr>
<tr>
<td>サービスを購入する前に、課金ルールの詳細を確認します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30255" target="_blank">課金に関する質問</a></td>
</tr>
<tr>
<td>リアルタイム音声サービス利用における音声ルームに関する問題の解決策。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/35611" target="_blank">リアルタイム音声ルーム失敗に関する質問</a></td>
</tr>
<tr>
<td>SDKを使用する際のオーディオに関する問題の解決策を調べます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30257" target="_blank">リアルタイム音声の無音とオーディオに関する質問</a></td>
</tr>
</tbody></table>


## 7. 初心者のよくある質問
#### お問い合わせに関する質問
[GMEのリアルタイム音声を使用するときのトラフィック消費量はどのくらいですか。](https://intl.cloud.tencent.com/document/product/607/39519)
[GMEにはどのような機能がありますか。](https://intl.cloud.tencent.com/document/product/607/39520)


#### Demo関連問題
[GMEはOpenIdを1つだけ使用できますか。](https://intl.cloud.tencent.com/document/product/607/30256)
[ダウンロードしたDemoの使用方法。](https://intl.cloud.tencent.com/document/product/607/30256)
[ログの取得方法は](https://intl.cloud.tencent.com/document/product/607/39521)
[GME SDKを統合してApkをエクスポートすると、起動プログラムに黒画面が表示されます。どうすれば解決できますか？](https://intl.cloud.tencent.com/document/product/607/39522)
[Xcodeが実行可能ファイルをエクスポートするときにGMESDK.frameworkライブラリが追加されました。コンパイル時にコンパイルエラーが報告されました。どうすれば解決できますか？](https://intl.cloud.tencent.com/document/product/607/39522)


#### リアルタイム音声サービスに関する問題
[GME SDKのpoll関数はいつから呼び出されますか？](https://intl.cloud.tencent.com/document/product/607/30254)
[GMEリアルタイム音声のルーム数と人数には制限がありますか？](https://intl.cloud.tencent.com/document/product/607/35611)
[EnterRoomインターフェースを呼び出しても戻り値が0ですが、ルームに入れないのはなぜですか？](https://intl.cloud.tencent.com/document/product/607/39523)
[ネットワークの問題が発生したら、どのように対処すればいいですか？](https://intl.cloud.tencent.com/document/product/607/39519)
[ユーザーがリアルタイム音声ルームにいるが、クライアントがネットワーク接続が切断した場合、どのように対処すればいいですか？](https://intl.cloud.tencent.com/document/product/607/35611)
[リアルタイム音声の範囲音声機能を使用して、範囲音声は正常に使用できますが、減衰効果はありません。3Dサウンドファイルを設定しても、戻り値は0でした。](https://intl.cloud.tencent.com/document/product/607/39523)
[ルームに入ると、携帯電話の音量が小さくなります。マイクをオンにすると音量が大きくなりますが、どのように対処しますか？](https://intl.cloud.tencent.com/document/product/607/39524)
[ Androidの携帯でマイクをオンしたら、音はスピーカーの代わりに受話器から出てきますが、どのように対処すればいいですか？](https://intl.cloud.tencent.com/document/product/607/30257)

## 8. フィードバックと要望
GMEの製品およびサービスを使用する上で何らかの質問やアドバイスがある場合は、以下の方法でフィードバックをお願いします。後ほど専門スタッフがお客様の質問に回答します。
- 製品のドキュメントの間違い等を発見した場合（リンク先、内容、API エラーなど）は、ドキュメントのページ右側の【ドキュメントに関するフィードバック】をクリックするか、または問題が存在するコンテンツを選択してフィードバックしてください。
- 製品関連の質問がある場合には、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してサポートを求めることができます。

>? チケットを提出してサポートを求める際には、SDKのバージョンと使用するプラットフォームを教えてください。
