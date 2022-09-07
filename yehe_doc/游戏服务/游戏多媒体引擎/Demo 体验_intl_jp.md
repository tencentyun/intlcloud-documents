
<table>
  <tbody><tr>
    <th style="text-align:center;" width="150px"><b>Android<br></b>はカメラでコードをスキャンします</th>
    <th style="text-align:center;" width="150px"><b>iOS<br></b>はカメラでコードをスキャンします</th>
  </tr>
  <tr>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
  </tr>
</tbody></table>

## Android/iOS Unity Demo基本機能の説明

<span id="test"></span>

### ログイン

UserIdと入力して、**Login**をクリックすると、システムで設定したUserIdを使用してログインします。ログインすると、**Voice Chat**ボタンと**Voice Message**ボタンが画面に追加されます。
<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="80%" /></img><br>
- **Voice Chat**をクリックすると、[ボイスチャット](#test1)機能に入ります。
- **Voice Message**をクリックすると、[ボイスメッセージ](#test2)機能に入ります。

<span id="test1"></span>

### ボイスチャット


1. [ログイン](#test)したら、**Voice Chat**をクリックしてボイスチャット画面に進みます：
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="80%"/></img><br>
 - RoomId：ルームIDです。同じルーム番号のメンバーが同じルームに入ります。
 - RoomType：音声品質を制御します。
    - Fluency：スムーズな音質。なめらかさ優先、超低遅延リアルタイム音声は、ゲーム内のボイスチャットシーンに使用され、FPSやMOBAなどのタイプのゲームに適しています。
    - Standard：標準音質。音質が良く、レイテンシーも適度なので、人狼ゲームやチェス・カードゲームなどのカジュアルなゲームのリアルタイム会話シナリオに適しています。
    - High Quality：高音質。高音質で、遅延が比較的大きく、音楽ダンスゲームおよびボイスSNSなどのAPPに適します。また音楽の再生、オンラインカラオケなど、高音質が要求されるシナリオに適しています。


2. ボイスチャット画面で**JoinRoom**をクリックしてルームに入ります。
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="80%"/><br>
 - Talking Members：ルーム内で話しているメンバ。画面には話しているメンバIDが表示されます。
 - Mic：マイクです。チェックマークが付いているとオン状態になります。 
 - Speaker：スピーカーです。チェックマークが付いているとオン状態になります。
 - 3D Voice Effect：3Dサウンドです。チェックマークが付いているとオン状態になります。次のパラメータで設定できます：
    - Range：音声受信範囲をゲームエンジン単位で設定します。
    - X：自分のX軸。
    - Y：自分のY軸。
    - Z：自分のZ軸。
    - XR：X軸を中心に回転する方向。
    - YR：Y軸を中心に回転する方向。
    - ZR：Z軸を中心に回転する方向。
 - Voice Change：リアルタイム音声サウンドです。さまざまなパラメーターの種類を選択することで、再生される音声サウンドの特性を変更できます。詳細については[リアルタイム音声サウンド](https://intl.cloud.tencent.com/document/product/607/31503#k-.E6.AD.8C.E9.9F.B3.E6.95.88.E7.89.B9.E6.95.88)をご参照ください。


<span id="test2"></span>

### ボイスメッセージのテキスト変換

[ログイン](#test)したら、**Voice Message**をクリックして言語メッセージ画面に進みます。
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="80%"/></img><br>
- Language：使用する言語。
- Audio：録音された音声メッセージと音声の長さ。<img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img>をクリックして録音を再生し、再生中にもう一度クリックして再生を終了します。
- Audio-to-Text：音声から変換されたテキストです。**Push To Talk**を長押しすると録音を開始します。**Push To Talk**をボタンを離すと録画を終了します。


## Windowsプラットフォーム3D音声体験Demo


### 前提条件
- このデモプログラムはWindowsプラットフォームで実行してください。
- デモプログラムは、同じマシン上で2つのプログラムを同時に動作させ、または同じローカルネットワーク上の2つのマシンで別々のプログラムを動作させてください。
- ヘッドフォンとマイクが使用可能な状態になっていることを確認してください。
- GMEリアルタイム音声サービスの有効化は事前にお申し込みください。

### 1. ダウンロード

[3D音声デモプログラムのダウンロード](https://picture-1256313114.cos.ap-beijing.myqcloud.com/GMEDemo.zip)をクリックして、ダウンロードしたら解凍します。

### 2. Demoを開く

**GMEDemo.exe**というタイトルの実行可能ファイル（Demoプログラム）をダブルクリックして開きます。同じマシン上で2つのデモプログラムを同時に開くことができます。

### 3. 初期化

初期化プログラムでは、[GMEコンソール](https://console.cloud.tencent.com/gamegme/detail/1400391524)サービス管理のAppIDと権限キーを入力する必要があります。GMEサービスを申し込みます。詳細ついては[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。**appIdはコンソールのAppID、authKeyはコンソールの権限キーに対応します。**


<dx-alert infotype="explain" title="">
- AppIDを保存し、権限キーが漏洩しないように注意してください。
- このときのuserIdの数値に注意してください。開いた別のデモプログラムのuserIdがこのuserIdと異なることを確認してください。
</dx-alert>



<img src="https://main.qcloudimg.com/raw/f27ce333719f70f03447dcd97c5c9f3a.png"  width="80%"><br>
入力したら、**初期化**>**リアルタイム音声**をクリックして、リアルタイムボイスルームの入力画面に進みます。

### 4. 音声ルームに参加します

ここで音声ルーム選択画面に入り、入ったルーム番号を入力します。この時点で別のデモプログラムを開いている場合は、同じルーム番号を入力し、**JoinRoom**をクリックして**同じボイスルーム**に入ります。

<img src="https://main.qcloudimg.com/raw/8774bd52027febc15582e3d9f700eff8.jpg"  width="80%">

### 5. ゲーム画面の紹介

画面情報の説明は次のとおりです：
- 終了ボタン：クリックすると音声ルーム選択画面に戻ります。
- マイクのオン/オフ：ルームに入るときにはデフォルトでマイクがオフになっています。通話を行うにはマイクをオンにしてください。
- 使用ヘルプ：クリックすると使用ヘルプ画面が開きます。
- 伴奏オン：クリックすると伴奏を再生します。
- 画面の右下：ルームログ情報です。音声ルームに入室したユーザーと退室したユーザーが表示されます。
- 画面の左：ローカル接続ボタンです。ゲームがスタートする前に設定を行ってください。
<img src="https://main.qcloudimg.com/raw/ae3f7726b2669c57466194a6e3e1e567.png"  width="80%"/></img>

### 6. ローカル接続

**このデモプログラムにはローカルLAN接続の基本が必要です**。
<img src="https://main.qcloudimg.com/raw/7779b1359844c1465d613586aab2c06d.png" width="80%" /></img>

- 最初にルームに入った人
最初にルームに入ったは、ネットワーク接続のHostです。そのため、<b>LAN Host(H)</b>をクリックする必要があります。クリックすると、コインの横に人物が生成されます。


- ルームに入った最初の人ではありません
最初に入室した人以外はHostに接続するので、<b>LAN Client(C)</b>をクリックする必要があります。クリックすると、コインの横に人物が生成されます。この場合、最初にルームに入った人が表示されます。


### 7. マイクをオンにする

<img src="https://main.qcloudimg.com/raw/1fd9f4e3f35cfc166e04bd26fb520abf.png" width="3%"></img>クリックするとマイクがオンになり、ルームにいる人と通話できるようになります。

### 8. 操作方式

キーボードの「W」、「S」、「A」、「D」はそれぞれ「前進」、「後退」、「左に回転」、「右に回転」に対応し、マウスを回すことで画角を調整できます。接続されたクライアントには、別のクライアントで操作されているキャラクターが表示されます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/23cd82f978016559de9c40a413dc23b9.png"  width="80%"/></img>

### 9. 体験方法

ローカルで2つのデモプログラムを同時に動作させる場合、まず片方のデモプログラムの画角をコインの横に移動させ、マイクをオンにします。もう1つのデモプログラムのキャラクターはできるだけ遠くまで走り、走りながら話をします。そうすると、3Dの音声効果を体験できます。マップの境界まで走るとき、ボイスは聞こえなくなるまで小さくなります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/01cfbded69436d29042ba1a14cc0e737.png"  width="80%"/></img>


## 高級ボイスチェンジ体験

GMEの高級ボイスチェンジを使用すると、ゲームのボイスチャット中に音声を自由に変換して、さまざまな効果音を再生します。

### 前提条件
- このデモプログラムはWindowsプラットフォームで実行してください。
- ヘッドフォンとマイクが使用可能な状態になっていることを確認してください。
- GMEリアルタイム音声サービスの有効化は事前にお申し込みください。

### プログラムを開く

[高級ボイスチェンジ体験プログラム](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GMEDemoWithVoicemod_1.0.zip)をクリックしてダウンロードし、ダウンロードしたら解凍します。**TMGSDK_For_Audio_ApiExample.exe**というタイトルの実行可能ファイルをダブルクリックして開き、プログラムを実行します。

### 実行画面



### 1. AppIDとKeyを入力

初期化プログラムでは、[GMEコンソール](https://console.intl.cloud.tencent.com/gamegme)サービス管理のAppIDと権限キーを入力する必要があります。GMEサービスをお申し込みます。詳細ついては[アクセスガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。**AppIDはコンソールのAppIDに対応し、Keyはコンソールの権限キーに対応します。**


<dx-alert infotype="explain" title="">
- AppIDを保存し、権限キーが漏洩しないように注意してください。
- このときのuserIdの数値に注意してください。開いた別のデモプログラムのuserIdがこのuserIdと異なることを確認してください。
</dx-alert>

### 2. 初期化
**Init**ボタンをクリックして初期化します。

### 3. 入室
**EnterRoom**をクリックして音声ルームに入ります。

### 4. デバイスをオンにする

**EnableMic**、**EnableSpeaker**、**EnableLoopback**をクリックして、デバイスとインイヤーモニターをオンにします。

### 5. 体験

マイクに向かって話しかけ、ボイスチェンジ効果を体験できます。

ボイスチェンジ設定の説明：
<img src="https://qcloudimg.tencent-cloud.cn/raw/97aa3d6feabc0d4e79fe4ac689271c6b.png"  width="80%"/></img>

### 6. ルームからの退出
テストが完了したら**ExitRoom**をクリックして退室してください。不必要な費用を避けます。
