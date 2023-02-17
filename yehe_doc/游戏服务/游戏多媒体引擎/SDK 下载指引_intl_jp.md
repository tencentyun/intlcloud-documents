開発者がGME製品を手軽に導入するように、本書では、GME向けSDKのダウンロード方法を説明します。

## 更新履歴
SDKの更新履歴については、[リリースノート](https://intl.cloud.tencent.com/document/product/607/35323)をご参照ください。

## 初心者向け（入門編）

SDKを初めて使用する場合、ダウンロードする前に、[初心者ガイド](https://intl.cloud.tencent.com/document/product/607/39696)を参照してサービスを登録してください。

## Sample Projectガイド

### Sample Projectの使用

SDKとSample Projectをダウンロードした後、使用上の問題がある場合、[Sample Project使用についての質問](https://www.tencentcloud.com/document/product/607/39521)を確認するか、[オンラインお問い合わせ](https://intl.cloud.tencent.com/contact-sales)でTencent Cloudの担当者に連絡してください。

>?ダウンロードしたSample Projectコードに対して、申し込んだSDKAppidとKeyで置き換えてからコンパイルしてください。例えば、Unity Demoでは**UserConfig.cs**ファイルを変更する必要があります。申請サービスの詳細については、[音声サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。

### Sample Projectでのデバッグ

Sample Projectを使用しデバッグを行います。問題が発生した場合、以下のドキュメントをご参照ください。

- ルーム参加失敗に関する問題については、[リアルタイム音声ルーム参加失敗に関する質問](https://intl.cloud.tencent.com/document/product/607/39523)をご参照ください。
- 音声がない問題については、[リアルタイム音声なし及びオーディオに関する質問](https://intl.cloud.tencent.com/document/product/607/39524)をご参照ください。
- サービス呼出しエラーについては、[エラーコード](https://intl.cloud.tencent.com/document/product/607/33223)をご参照ください。
- 解決できなければ、ログを取得し、[お問い合わせ](https://intl.cloud.tencent.com/document/product/607/49702)でGME開発者に連絡してください。



### Sample Projectのエクスポート

Sample Projectを実行可能ファイルとしてエクスポートする際に問題が発生した場合、[プロジェクトエクスポートの問題](https://intl.cloud.tencent.com/document/product/607/39522)をご参照ください。



## バージョン更新

v2.9.6の正式版の更新は以下の通りです：

<table>
<thead>
<tr>
<th width="18%">リリース名称</th>
<th width="44%">リリース詳細</th>
 <th width="14%">リリース時間</th>  
<th width="24%">関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>SDK v2.9.6の正式版のリリース</td>
<td ><ul style="margin:0;">
<li >国戦、SLGに関連するゲームへのサポートを強化するために、リアルタイム音声にロール設定が新規に追加されたました</li>
<li >2チャネルの伴奏を同時に再生するのをサポートします</li>
<li >オンラインMP3ファイルを伴奏とする場合、伴奏の進捗を設定することをサポートします</li>
<li >テキスト翻訳に言語のチェック結果を返す機能が新規に追加されました。</li>
<li >ボイスツーテキスト変換インターフェースに翻訳機能が新規に追加されました。</li>
<li >VRシーンによりよく対応するために、ローカル3D位置入力インターフェースが新規に追加されました。</li>
<li >3Dサウンドブラックリストインターフェースが新規に追加されました。呼び出した場合、相手の音声に3Dエフェクトがかけられません。</li>
<li >3Dサウンド機能の最適化です。3Dオーディオモデルをビルドインすることで、モデルパスに渡す必要をなくします</li>
<li >SDKにUnity WebGLプラットフォーム、xbox gamecoreプラットフォーム、UnrealEngine5エンジンへのサポートが新規に追加されました</li>
<li >SDKがPlaystation 5の新しいバージョンをサポートするようになりました。</li>
<li >Mac向けSDKにM1 Arm64アーキへのサポートが新規に追加されました</li>
<li >Android 12ブルートゥース権限の最適化</li>
<li >Android 5.1の互換性問題が修正されました</li>
<li >音声メッセージのループ再生によって発生するメモリ問題が修正されました</li>
<li >SDKメモリ使用量の削減です。</li>
<li >ハードウェアデバイスの起動時間の最適化です。リアルタイム音声が有効になっている場合のルーム参加までの時間が短縮されます。</li>
</ul ></td>
<td>2023-01-18</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218">3Dサウンド</a></td>
</tr>
</tbody></table>



<dx-alert infotype="notice" title="更新注意">
-  古いバージョンから2.9.6に更新する場合、[更新ガイド](https://intl.cloud.tencent.com/document/product/607/32363)をご参照ください。
</dx-alert>



## SDKのダウンロード

| プラットフォーム/エンジン  |   バージョン          | 更新時間   | SDKダウンロード| Sample Projectダウンロード| クイックスタートドキュメント|
| ----------------- | ---------- | ---------- | ---------------------------- | ---------------------------- | -------------------------------- |
| Unity   | v2.9.6    | 2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_SDK_2.9.6.09d06620.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_Demo_2.9.6.09d06620.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/44544) |
| Unreal Engine 4.x | v2.9.6 | 2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_SDK_2.9.6.09d06620.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_Demo_2.9.6.09d06620.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/44545) |
| Unreal Engine 5.x | v2.9.6 |  2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_SDK_2.9.6.97b107ed.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_Demo_2.9.6.97b107ed.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/44545) |
| Cocos2D      |v2.9.6       |  2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_SDK_2.9.6.09d06620.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_Demo_2.9.6.09d06620.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/18292) |
| Windows      | v2.9.6       | 2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_sdk_2.9.6.92a797e4.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_example_project_2.9.6.92a797e4.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/40858) |
| iOS        | v2.9.6         | 2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_sdk_2.9.6.92a797e4.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_example_2.9.6.92a797e4.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/40858) |
| Android    | v2.9.6        | 2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_sdk_2.9.6.92a797e4.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_example_2.9.6.92a797e4.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/40858) |
| macOS     | v2.9.6          | 2023-01-18 | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_sdk_2.9.6.92a797e4.zip) | [ダウンロード](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_demo_2.9.6.92a797e4.zip) | [クイックスタート](https://intl.cloud.tencent.com/document/product/607/40858) |
| Web      | -          | 2022-06-20 | [ダウンロード](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.1/H5/GME_Web_SDK_2.8.1.47.zip) | [ダウンロード](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.1/H5/GME_Web_Demo_2.8.1.47.zip) | [インターフェースドキュメント](https://intl.cloud.tencent.com/document/product/607/30263) |





> ?
> - GME SDKは**コンシューマーゲームプラットフォーム**（PlayStation、Xbox、Nintendo Switch）もサポートします。必要に応じて、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してGME開発者に連絡してください。
>- プラットフォームごとのSDKのコンパイルツールチェーンは、[コンパイルツールチェーンドキュメント](https://intl.cloud.tencent.com/document/product/607/46711)をご参照ください。
> - デフォルトではITMG_ROOM_TYPE_FLUENCY音質を提供します。標準音質またはHD音質を使用する場合、[チケットを提出](https://www.tencentcloud.com/document/product/607/18521#:~:text=%E6%97%A5%E5%BF%97%E5%90%8E%EF%BC%8C%E9%80%9A%E8%BF%87-,%E6%8F%90%E4%BA%A4%E5%B7%A5%E5%8D%95,-%E8%81%94%E7%B3%BB%20GME%20%E5%BC%80%E5%8F%91)してGME開発者に連絡してください。



