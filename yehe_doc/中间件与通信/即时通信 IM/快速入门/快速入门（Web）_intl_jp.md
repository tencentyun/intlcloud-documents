# [クイックスタート(Web)](https://www.tencentcloud.com/document/product/1047/45912)
>Chat UIKitはTencent Cloud IM SDKに基づいたUIコンポーネントライブラリで、会話、チャット、リレーショナルチェーン、グループ、オディオ・ビデオ通話などの機能を含む汎用的なUIコンポーネントを提供しています。
UIコンポーネントに基づいて、独自のビジネスロジックを積み木のようにすばやく構築できます。
Chat UIKitのコンポーネントはUI機能を実現すると同時に、IM SDKの対応するインターフェースを呼び出してIM関連のロジックとデータの処理を実現するため、開発者はChat UIKitを使用する際に自分の業務やパーソナライズされた拡張に注目すればよいです。

<img align="right" src="https://qcloudimg.tencent-cloud.cn/raw/4562be8179a1534efb17d33428239c82.png?auto=format,enhance" width="50%" />

### Quick Links
- [Demo App](https://web.sdk.qcloud.com/im/demo/intl/index.html)
- [Client API](https://www.tencentcloud.com/document/product/1047/33999)
- [Free Demos](https://www.tencentcloud.com/document/product/1047/34279)
- [FAQ](https://www.tencentcloud.com/document/product/1047/34455)
- [GitHub Source](https://github.com/TencentCloud/chat-uikit-react)
- [Generating UserSig](https://www.tencentcloud.com/document/product/1047/34385)
## Example App
チャット機能を示すためのインスタンスデモプログラムを構築しています。これらの[demo](https://web.sdk.qcloud.com/im/demo/intl/index.html)は弊社のWebサイトでプレビューできます。また、関連する[オープンソース](https://github.com/TencentCloud/chat-uikit-react)もGitHubに用意されています。

![img.png](https://web.sdk.qcloud.com/im/demo/TUIkit/react-static/images/home.png)

## demoのクイックスタート

### 手順1：ソースコードのダウンロード
```
# Run the code in CLI
$ git clone https://github.com/TencentCloud/chat-uikit-react
# Go to the project  
$ cd chat-uikit-react
# Install dependencies of the demo
$ npm install && cd examples/sample-chat && npm install
```
### 手順2：demoの設定
1. `examples/sample-chat`プロジェクトを開き、パス`./examples/sample-chat/src/debug/GenerateTestUserSig.js`で`GenerateTestUserSig.js`ファイルを探します。
2.　`GenerateTestUserSig.js`ファイルに`SDKAPPID`と`SECRETKEY`を設定します。これらの値は[IMコンソール](https://console.tencentcloud.com/im)で取得できます。対象のアプリカードをクリックすると、設定ページに移動します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
3.　**Basic Information**領域で**Display key**をクリックし、キー情報をコピーしてGenerateTestUserSigファイルに保存します。
>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します。**
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/1047/34385)をご参照ください。

### ステップ3：プロジェクトの起動
```
# Launch the project
$ cd examples/sample-chat
$ npm run start
```

###　手順4：最初のメッセージを送信
1.　プロジェクトの起動に成功したら、「+」アイコンをクリックして、セッションを作成します。
2.　入力ボックスで別のユーザーのuserIDを検索します。
3.　ユーザーのプロファイル画像をクリックしてセッションを開始します。
4.　入力ボックスにメッセージを入力し、「enter」キーを押して送信します。
   ![](https://web.sdk.qcloud.com/im/demo/TUIkit/react-static/images/chat.gif)

## chat-uikit-reactの統合

### 手順1：Installation
```
$ npm install @tencentcloud/chat-uikit-react
```
### 手順2：Usage
```tsx
import React, { useEffect, useState } from 'react';
import { TUIKit } from '@tencentcloud/chat-uikit-react';
import '@tencentcloud/chat-uikit-react/dist/cjs/index.css';
import TIM, { ChatSDK } from 'tim-js-sdk/tim-js-friendship';
import TIMUploadPlugin from 'tim-upload-plugin';

//　timインスタンスオブジェクトを生成してログインを完了
const init = async () => {
   return new Promise((resolve, reject) => {
      const tim = TIM.create({ SDKAppID: 000 });
      tim?.registerPlugin({ 'tim-upload-plugin': TIMUploadPlugin });
      const onReady = () => { resolve(tim); };
      tim.on(TIM.EVENT.SDK_READY, onReady);
      tim.login({
         userID: 'xxx',
         userSig: 'xxx',
      });
   });
}

export function SampleChat() {
   const [tim, setTim] = useState<ChatSDK>();
   useEffect(() => {
      (async ()=>{
         const tim = await init()
         setTim(tim)
      })()
   }, [])

   return (
           <div style={{height: '100vh',width: '100vw'}}>
              <TUIKit tim={tim}></TUIKit>
           </div>
   );
}
```
