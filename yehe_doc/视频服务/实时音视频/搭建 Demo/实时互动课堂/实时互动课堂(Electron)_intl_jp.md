## Demo体験
<input type="button" value="Windows版" style="height: 30px;width: 150px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;margin-right:10px;"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe')" />

<input type="button" value="MacOS版" style="height: 30px;width: 150px;margin-top: 5px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo-1.1.0.dmg')" />

## DemoのUIの再利用
[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援**>**[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2. `TestEduDemo`などのアプリケーション名を入力して、**作成**をクリックします。

>?本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPAASサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### ステップ2：SDKおよびDemoソースコードをダウンロード
1. 実際のビジネスニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、**ダウンロードしました。次のステップ**をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### ステップ3：Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2.  `Electron/js/GenerateTestUserSig.js` ファイルを見つけて開きます。
3. `GenerateTestUserSig.js` のファイルの関連するパラメータを設定します。
<ul>
 <li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
 <li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
 <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>
4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：Demoの動作

```typescript
// yarnをインストールし、demoをyarnに基づき管理します
npm install yarn -g
// 必要な依存をインストールします
yarn install
// 開発デバック
yarn dev
// パッケージ化
yarn package
```

>! 
>- 依存関係のインストール中に、Electronのダウンロードが遅い、またはスタックするなどの問題が発生した場合は、[お問い合わせ]（https://intl.cloud.tencent.com/contact-us）を参照して問題を解決できます。
>- Macでパッケージ化したMacパッケージング、Windows PCでパッケージ化したWindowsパッケージのみ使用できます。


### 手順5：Demoソースコードの修正
Demoで使用するアーキテクチャの技術は次のとおりです。
- typescript
- react & react hooks
- electron & electron-react-boilerplate
- element-ui

以下の表にはファイルまたはフォルダおよび対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイル |機能説明|
| ----- | ----- |
| app/containers/HomePage.tsx|教室参加のUIの実装コード|
| app/containers/ClassRoomPage.tsx|教室のUIの実装コード|
| app/components/TeacherClass.tsx|教室-教師側UIの実装コード|
| app/components/StudentClass.tsx|教室-学生側UIの実装コード|
| app/components/Chat.tsx|教室-チャットルームのUIの実装コード|
| app/components/UserList.tsx|教室-メンバーリストのUIの実装コード|

## UIカスタマイズの実装
Demoにデフォルトで実装されているUIが期待どおりでない場合は、必要に応じて独自のユーザーインターフェースを実装することができます。すなわち、当社がパッケージングした[trtc-electron-education](https://www.npmjs.com/package/trtc-electron-education)コンポーネントで提供する音声・ビデオの機能のみを使用し、UI部分を単独で実装します。
![](https://main.qcloudimg.com/raw/cba4f331a811dd5dbf31cce80bd1d826.png)

### 手順1：SDKの統合 

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
|sdkAppId|number|入力必須のパラメータ。<a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>の中でSDKAppIDを確認できます。|
|userID|string|入力必須のパラメータ。ユーザーIDは、お客様のアカウントシステムから指定できます。ビジネスの実際のアカウントシステムを組み合わせて設定することをお勧めします。|
|userSig|string|入力必須のパラメータ。ID署名（ログインパスワードに相当）は、userIDから算出します。具体的な計算方法については、[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。|

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
      classId, // 教室ID
      nickName // ニックネーム
}
rtcClient.createRoom(params).then(() => {
  //教室の作成の成功
})
```
2. 教師側がコンポーネント[enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)のメソッドを呼び出し、授業を開始します。
```typescript
rtcClient.enterRoom({
      role: 'teacher', // ロール
      classId // 教室ID
})
```
3. 教師側がコンポーネント[openCamera](https://intl.cloud.tencent.com/document/product/647/37279#openCamera)のメソッドを呼び出し、自分のカメラを立ち上げます。
```typescript
const domEle = document.getElementById('test');
rtcClient.openCamera(domEle)
```
4. 教師側は自分の画面を学生側に共有させ、PPT、教材の再生などを視聴させることができます。
 a. 先にコンポーネント[getScreenShareList](https://intl.cloud.tencent.com/document/product/647/37279#getScreenShareList)のメソッドを呼び出し、ウィンドウのリストを取得する必要があります。
```typescript
const screenList = rtcClient.getScreenShareList()
```
 b. コンポーネントの[startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37279#startScreenCapture)を呼び出し、画面を共有するストリームのプッシュを開始します。
```typescript
rtcClient.startScreenCapture({
      type,// キャプチャソースタイプ
      sourceId,// ソースIDの収集。ウィンドウについては、当該フィールドにウィンドウのハンドルを表示します。画面については、当該フィールドに画面IDを表示します
      sourceName // ソース名の収集、UTF8エンコーディング
 })
```
5. 授業中、教師が学生と質疑応答の交流を行いたい場合、コンポーネント[startQuestionTime](https://intl.cloud.tencent.com/document/product/647/37279#startQuestionTime)のメソッドを呼び出し、質疑応答時間をオンにすることができます。学生側は、このコマンドの受信後、挙手にて回答を申請できるようになります。
```typescript
rtcClient.startQuestionTime(classId) // classIdは教室IDです
```
6. 学生の挙手の後、教師側はコンポーネント[inviteToPlatform](https://intl.cloud.tencent.com/document/product/647/37279#inviteToPlatform)のメソッドを呼び出し、学生を皆の前での発言に招待することができます。招待された学生はマイクが自動的に起動します。
```typescript
rtcClient.inviteToPlatform(userID) // 発言に招待された学生のuserID
```
7. 教師側は、コンポーネント[finishAnswering](https://intl.cloud.tencent.com/document/product/647/37279#finishAnswering)のメソッドを呼び出して、学生のマイク使用を禁止することができます。
```typescript
rtcClient.finishAnswering(userID)// マイク使用を禁止された学生のuserID
```

### 手順4：学生側の聴講の実現
1. 学生側は、コンポーネント[enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)のメソッドを呼び出して、教室に入室して聴講の準備をします。
```typescript
rtcClient.enterRoom({
      role: 'student', // ロール
      classId // 教室ID
})
```
2. 教師側が挙手による質疑応答をオープンにすると、学生側はコンポーネント[raiseHand](https://intl.cloud.tencent.com/document/product/647/37279#raiseHand)のメソッドを呼び出し、発言を申請できます。
```typescript
rtcClient.raiseHand()
```

### 手順5：チャットルーム機能の実装

教師側と学生側は、チャットルームを利用してテキストメッセージを相互に送信することができます。
```typescript
const params = {
   classId: classId, // 教室ID
   message: 'こんにちは' // メッセージのテキスト
}
rtcClient.sendTextMessage(params) // チャットルームのメッセージの送信
```

## 技術的なお問い合わせ
詳細については、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)にご連絡をいただくか、colleenyu@tencent.comにメールでご連絡ください。

## 参考ドキュメント

- [SDK APIマニュアル](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demoソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCSimpleDemo)
- [API Exampleソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTC-API-Example)
- [Electronについてのよくあるご質問](https://intl.cloud.tencent.com/document/product/647/43093)
