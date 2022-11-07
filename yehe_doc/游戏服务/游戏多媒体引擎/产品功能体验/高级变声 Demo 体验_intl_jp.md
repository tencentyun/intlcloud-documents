## ユースケース
Tencent Cloud Game Multimedia Engine (GME)は高品質のワンストップ音声ソリューションを提供し、ゲーム業界のユースケースを全面的にカバーしています。複数人のリアルタイム音声、3D位置音声、音声メッセージ、ボイスツーテキスト変換と音声コンテンツのセキュリティなどの機能をサポートします。GME高級ボイスチェンジ効果を使用すると、ゲーム内のボイスチャット中に声を自由に変換し、さまざまなサウンドを運ぶことができます。
>!Demoを体験するには、Windowsプラットフォームのコンピュータが必要です。

## 前提条件

- このデモプログラムはWindowsプラットフォームで実行してください。
- デモプログラムは、同じマシン上で2つのプログラムを同時に動作させ、または同じローカルネットワーク上の2つのマシンで別々のプログラムを動作させてください。
- ヘッドフォンとマイクが使用可能な状態になっていることを確認してください。
- 事前にGMEリアルタイム音声サービスをお申し込みいただき、AppIdとKeyを取得してください。GMEサービスを申し込むには、詳細については、[初心者向けガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。**appIdはコンソールのAppIDに対応し、authKeyはコンソールの権限キーに対応します。**費用の詳細については、[購入ガイド](https://intl.cloud.tencent.com/document/product/607/50009)をご参照ください。

## 操作手順
### 1. プログラムを開く

[高級ボイスチェンジ体験プログラム](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GMEDemoWithVoicemod_1.0.zip)をクリックしてダウンロードし、ダウンロードしたら解凍します。**TMGSDK_For_Audio_ApiExample.exe**というタイトルの実行可能ファイルをダブルクリックして開き、プログラムを実行します。

実行画面は次のとおりです：

<img src="https://qcloudimg.tencent-cloud.cn/raw/ced85aa2b117bad61fe538c2e3a1252e.png" width=80%/><img>

### 2. AppIDとKeyを入力する

プログラムを初期化するには、[GMEコンソール](https://console.cloud.tencent.com/gamegme)サービス管理のAppIDと権限キーを入力する必要があります。GMEサービスを申し込むには、詳細については[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。**AppIDはコンソールのAppIDに対応し、Keyはコンソールの権限キーに対応します。**

<dx-alert infotype="explain" title="">

- AppIDを保存し、権限キーが漏洩しないように注意してください。
- このときのuserIdの数値に注意してください。開いた別のデモプログラムのuserIdがこのuserIdと異なることを確認してください。
  </dx-alert>

### 3. プログラムを初期化する

**Init**ボタンをクリックして初期化します。

### 4. ルームに入る

**EnterRoom**をクリックして音声ルームに入ります。

### 5. デバイスをオンにする

**EnableMic**、**EnableSpeaker**、**EnableLoopback**をクリックして、デバイスとインイヤーモニターをオンにします。

### 6. 効果を体験する

マイクに向かって話しかけ、ボイスチェンジ効果を体験できます。

ボイスチェンジ設定の説明：

<img src="https://qcloudimg.tencent-cloud.cn/raw/791e556855f15dfb3005040a8c4d1d27.png" width=80%/><img>

### 7. ルームから退出する

テストが完了したら**ExitRoom**をクリックして退室してください。不必要な費用を避けます。



