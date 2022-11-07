Tencent Cloud Game Multimedia Engine (GME)は高品質のワンストップ音声ソリューションを提供し、ゲーム業界のユースケースを全面的にカバーしています。複数人のリアルタイム音声、3D位置音声、音声メッセージ、ボイスツーテキスト変換と音声コンテンツのセキュリティなどの機能をサポートします。
>!ここで紹介するDemoを体験するには、AndroidまたはiOS携帯電話が必要です。

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


## Demo機能
Demoで示すGME基本機能は次のとおりです：

<table>
   <tr>
      <th>基本機能</th>
      <th>体験可能な機能</th>
   </tr>
   <tr>
      <td  rowspan="4">リアルタイム音声機能</td>
      <td>音質体験：滑らかな音質、標準的な音質、HD音質</td>
   </tr>
   <tr>
      <td>ルーム内のリアルタイム会話音声機能</td>
   </tr>
	    <tr>
      <td>3Dサウンド機能</td>
   </tr>
      <td>リアルタイム音声のボイスチェンジサウンド機能（基本ボイスチェンジ）</td>
   </tr>
      <td>音声メッセージ機能</td>
			<td>レコーディングを長押しして、音声メッセージをアップロードし、クリックして音声メッセージを再生します</td>
   </tr>
      <td>音声テキスト変換機能</td>
			<td>Demoでアップロードされた音声メッセージは自動的にテキストに変換され、複数の言語を選択できます</td>
   </tr>
</table>

<span id="test"></span>

## ログインインターフェース

### 1. システムへのログイン

UserIdと入力して、**Login**をクリックすると、システムで設定したUserIdを使用してログインします。ログインすると、**Voice Chat**ボタンと**Voice Message**ボタンが画面に追加されます。

<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="50%" /></img><br>

### 2. 使用する機能の選択

- **Voice Chat**をクリックすると、[リアルタイム音声](#test1)機能に入ります。
- **Voice Message**をクリックすると、[音声メッセージ](#test2)機能に入ります。

<span id="test1"></span>


## リアルタイム音声機能の体験

### 1. 音声ルームに入る 

 [ログイン](#test)したら、**Voice Chat**をクリックしてボイスチャット画面に進みます：

 <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="50%"/></img><br>

- **RoomId**：ルームIDです。同じルーム番号のメンバーが同じルームに入ります。
- **RoomType**：音声品質を制御します。
  - Fluency：滑らかな音質。滑らかさ優先、超低遅延リアルタイム音声は、ゲーム内の暗いシーンを開くために使用され、FPSやMOBAなどのタイプのゲームに適しています。
  - Standard：標準音質。音質が良く、遅延も適度なので、人狼ゲームやチェス・カードゲームなどのカジュアルなゲームのリアルタイム会話シーンに適しています。
  - Hign Quality：HD音質。超高音質、比較的大きな遅延、音楽の再生など高音質要件のゲームシーンに適しています。

### 2. ボイスチャット操作

ボイスチャット画面で**JoinRoom**をクリックしてルームに入ります。

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="50%"/><br>

- **Talking Members**：ルーム内で話しているメンバー。画面には話しているメンバーIDが表示されます。
- **Mic**：マイクです。チェックマークが付いているとオン状態になります。 
- **Speaker**：スピーカーです。チェックマークが付いているとオン状態になります。
- **3D Voice Effect**：3Dサウンドです。チェックマークが付いているとオン状態になります。次のパラメータで設定できます：
  - Range：音声受信範囲をゲームエンジン単位で設定します。
  - X：自分のX軸。
  - Y：自分のY軸。
  - Z：自分のZ軸。
  - XR：X軸を中心に回転する方向。
  - YR：Y軸を中心に回転する方向。
  - ZR：Z軸を中心に回転する方向。
- **Voice Change**：リアルタイム音声サウンドです。さまざまなパラメータの種類を選択することで、再生される音声サウンドの特性を変更できます。詳細については[リアルタイム音声サウンド](https://intl.cloud.tencent.com/document/product/607/31503)をご参照ください。
- **QuitRoom**：リアルタイム音声ルームを退出して、前の画面に戻ります。

<span id="test2"></span>

## 音声メッセージ機能とテキスト変換機能の体験

### 1. 音声メッセージ機能画面へ進み

[ログイン](#test)したら、**Voice Message**をクリックして言語メッセージ画面に進みます。

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="50%"/></img><br>

### 2. 画面操作

- **Language**：レコーディングされた言語を選択すると、レコーディング後に対応する言語のテキストに変換されます。**Audio-to-Text**欄に表示されます。
- **Push To Talk**：**Push To Talk**を長押しして、レコーディングを開始します。**Push To Talk**を放して、レコーディングを終了します。
- Audio：レコーディングされた音声メッセージと音声の長さ。<img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img>ボタンをクリックして録音を再生し、再生中にもう一度クリックして再生を終了します。
- **Audio-to-Text**：音声から変換されたテキストです。

