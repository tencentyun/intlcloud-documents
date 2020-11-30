## Demo 体験
<table style="text-align:center;vertical-align:middle;width: 300px">
  <tr>
    <th width="150px">Mac OS</th>
    <th width="150px">Windows</th>
  </tr>
  <tr>
<td>
		<a href="https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/electron_sdk/solution/education/TRTC_Education_Demo-1.1.0.dmg" >
		<span style="width:125px;height: 125px;background-image:url(https://main.qcloudimg.com/raw/d03160ca4e5342a96464aaba1de97923.png);background-size: cover;display:block;">
</span></a></td>
<td>
<a href="https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/electron_sdk/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe">
<span style="width:125px;height: 125px;background-image:url(https://main.qcloudimg.com/raw/d03160ca4e5342a96464aaba1de97923.png);background-size: cover;display:block;">
</span></a></td>
  </tr>
</table>



## デモンストレーション
当社のDemoをダウンロードし、インストールして リアルタイム双方向対話型授業の機能の効果をご体験いただけます。これには、音声、ビデオ、画面共有などの授業方式が含まれ、教師のQAの開始、学生の挙手、教師が学生を招待して皆の前で回答させる、回答の終了などの関連機能もパッケージングしています。

迅速にリアルタイム双方向対話型授業の機能にアクセスしたい場合は、当社が提供するDemoをもとに直接修正を加えてフィットさせることも、当社が提供する[trtc-electron-education](https://intl.cloud.tencent.com/document/product/647/37279) コンポーネントを使用し、カスタマイズしたUIを実現することも可能です。

## Demo の UI の再利用
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestEduDemo`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

>?説明：本機能はTencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、請求ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

<span id="ui.step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. 【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCScenesDemo/TRTCEducation)】をクリックすると、Githubにジャンプし、関連SDKとセットの Demoソースコードがダウンロードされます。
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

### 手順3：Demoプロジェクトファイルの設定
1．[手順2](#ui.step2) でダウンロードしたソースコードパッケージを解凍します。
2. `TRTCEducation/app/debug/GenerateTestUserSig.js` のファイルを探して開きます。
3. `GenerateTestUserSig.js`のファイルの関連するパラメータを設定します。
  <ul style="margin:0;"><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
  <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：Demoの動作

```typescript
// yarnをインストールし、demoをyarnに基づき管理します。
npm install yarn -g
// 必要な依存をインストールします。
yarn install
// 開発デバック
yarn dev
// パッケージ化
yarn package
```

>!
>- Macでパッケージ化したMacパッケージング、Windows PCでパッケージ化したWindowsパッケージのみ使用できます。


### 手順5：Demo ソースコードの修正
Demoで使用するアーキテクチャの技術は次のとおりです。
- typescript
- react & react hooks
- electron & electron-react-boilerplate
- element-ui

以下の表にはファイルまたはフォルダ及び対応する UIをリストアップして、二次調整を行いやすくしています。

| ファイル |機能説明|
| ----- | ----- |
| app/containers/HomePage.tsx|教室参加のUIの実装コード|
| app/containers/ClassRoomPage.tsx|教室のUIの実装コード|
| app/components/TeacherClass.tsx|教室-教師側UIの実装コード|
| app/components/StudentClass.tsx|教室-学生側UIの実装コード|
| app/components/Chat.tsx|教室-チャットルームのUIの実装コード|
| app/components/UserList.tsx|教室-メンバーリストのUIの実装コード|

## UIカスタマイズの実装
Demoの中で実現したデフォルトのUIが自分の予想と合わない場合は、必要に応じて自分独自のユーザーインターフェースを実現することができます。即ち当社がパッケージングした [trtc-electron-education](https://www.npmjs.com/package/trtc-electron-education) コンポーネントで提供する音声・ビデオの機能のみを使用し、独自にUIの部分を実現することが可能です。
![](https://main.qcloudimg.com/raw/cba4f331a811dd5dbf31cce80bd1d826.png)

### 手順1： SDKへの統合

```
// yarn方式の導入
yarn add trtc-electron-education
// npm方式の導入
npm i trtc-electron-education --save
```

### 手順2：コンポーネントの初期化
コンポーネントを初期化します。そのうち、入力必須となる主要パラメータを下表で紹介します。

| パラメータ |タイプ|説明|
| ----- | ----- | ----- |
|sdkAppId|number|入力必須のパラメータ。<a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> の中でSDKAppIDを確認できます。|
|userID|string|入力が必要なパラメータ。ユーザーIDは、お客様のアカウント体系から指定することが可能です。|
|userSig|string|入力が必要なパラメータ。ID署名（ログインパスワードに相当）は、userIDから算出します。具体的な計算方法は、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。|

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
   sdkAppId: 1400***803,
   userID: '123'
   userSig: 'eJwtzM9****-reWMQw_'
 });
```

### 手順3：教師側の授業の実現
1. 教師側がコンポーネント [createRoom](https://intl.cloud.tencent.com/document/product/647/37279#createRoom)のメソッドを呼び出し、教室を作成します。
```typescript
const params = {
      classId, // 教室 ID
      nickName // ニックネーム
}
rtcClient.createRoom(params).then(() => {
	//教室の作成の成功
})
```
2. 教師側がコンポーネント [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)のメソッドを呼び出し、授業を開始します。
```typescript
rtcClient.enterRoom({
      role: 'teacher', // ロール
      classId // 教室 ID
})
```
3. 教師側がコンポーネント [openCamera](https://intl.cloud.tencent.com/document/product/647/37279#openCamera)のメソッドを呼び出し、自分のカメラを立ち上げます。
```typescript
const domEle = document.getElementById('test');
rtcClient.openCamera(domEle)
```
4. 教師側は自分の画面を学生側に共有させ、PPT、教材の再生などを視聴させることができます。
 a. 先にコンポーネント [getScreenShareList](https://intl.cloud.tencent.com/document/product/647/37279#getScreenShareList)のメソッドを呼び出し、ウィンドウのリストを取得する必要があります。
```typescript
const screenList = rtcClient.getScreenShareList()
```
b. コンポーネントの[startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37279#startScreenCapture)を呼び出し、画面を共有するストリームのプッシュを開始します。
```typescript
rtcClient.startScreenCapture({
      type,// キャプチャソースタイプ
      sourceId,// ソースIDの収集。ウィンドウについては、当該フィールドにウィンドウのハンドルを表示します。画面については、当該フィールドに画面IDを表示します。
      sourceName // ソース名の収集、UTF8 エンコーディング
 })
```
5. 授業中、教師が学生と質問による交流を行いたい場合、コンポーネント [startQuestionTime](https://intl.cloud.tencent.com/document/product/647/37279#startQuestionTime)のメソッドを呼び出し、QAの時間を始動させることができます。学生側は、このコマンドの受信後、挙手にて回答を申請できるようになります。
```typescript
rtcClient.startQuestionTime(classId) // classId は教室IDです
```
6. 学生の挙手の後、教師側はコンポーネント [inviteToPlatform](https://intl.cloud.tencent.com/document/product/647/37279#inviteToPlatform)のメソッドを呼び出し、学生を皆の前での発言に招待することができます。招待された学生はマイクが自動的に起動します。
```typescript
rtcClient.inviteToPlatform(userID) // 発言に招待された学生のuserID
```
7. 教師側は、コンポーネント [finishAnswering](https://intl.cloud.tencent.com/document/product/647/37279#finishAnswering)のメソッドを呼び出して、学生のマイクを禁止することができます。
```typescript
rtcClient.finishAnswering(userID)// マイク禁止の学生のuserID
```

### 手順4：学生側の聴講の実現
1. 学生側は、コンポーネント [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)のメソッドを呼び出して、教室に入り、聴講のための準備をします。
```typescript
rtcClient.enterRoom({
      role: 'student', // ロール
      classId // 教室 ID
})
```
2. 教師側が挙手による質問の回答をオープンにすると、学生側はコンポーネント [raiseHand](https://intl.cloud.tencent.com/document/product/647/37279#raiseHand)のメソッドを呼び出し、発言を申請できます。
```typescript
rtcClient.raiseHand()
```

### 手順5：チャットルーム機能の実現

教師側と学生側は、チャットルームを利用してテキストメッセージを相互に送信することができます。
```typescript
const params = {
   classId: classId, // 教室 ID
   message: 'こんにちは' // メッセージのテキスト
}
rtcClient.sendTextMessage(params) // チャットルームのメッセージの送信
```
