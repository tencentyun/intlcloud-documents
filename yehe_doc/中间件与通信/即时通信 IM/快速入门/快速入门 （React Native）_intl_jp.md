ここでは、主にTencent CloudのInstant Messaging（IM）Demo（React Native）を素早く実行する方法をご紹介します。

## 環境要件

|              | バージョン                                                                 |
| ------------ | -------------------------------------------------------------------- |
| React Native | 0.63.4バージョン以降                                                      |
| Android      | Android Studio 3.5以降のバージョン。Appの要件はAndroid 4.1以降のバージョンのデバイスです。 |
| iOS          | Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。        |

##  前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## その1：テストユーザーの作成

[IMコンソール](https://console.cloud.tencent.com/im)でご自分のアプリケーションを選択し、左側ナビゲーションバーで**支援ツール**->**UserSig生成&検証**の順にクリックし、2つのUserIDおよびそれに対応するUserSigを作成します。`UserID`、`署名（Key）`、`UserSig`の3つをコピーし、その後のログインで使用します。

> ? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、サーバーで生成し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:part2)

## その2：React Native SDKの統合

### 前提条件

React Nativeプロジェクトの作成が完了しているか、またはベースになるReact Nativeプロジェクトがすでにあること。

### 統合の手順

#### IM SDKのインストール
次のコマンドを使用して、React Native IM SDKの最新バージョンをインストールします。コマンドラインで次を実行します。
```shell
// npm
npm install react-native-tim-js

// yarn
yarn add react-native-tim-js
```

#### SDKの初期化完了
`initSDK`を呼び出して、SDKの初期化を完了します。`sdkAppID`を渡します。
```javascript
import { TencentImSDKPlugin, LogLevelEnum } from 'react-native-tim-js';

TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
);
```

この手順ではIM SDKにいくつかのリスナーをマウントすることができます。これには主に、ネットワーク状態およびユーザー情報の変更などが含まれます。詳細については、[このドキュメント](https://comm.qq.com/im/doc/RN/zh/Interface/Listener/V2TimSDKListener.html)をご参照ください。

#### テストユーザーのログイン
1. この時点で、最初にコンソール上で作成したテストアカウントを使用して、ログイン検証を完了することが可能です。
2. `TencentImSDKPlugin.v2TIMManager.login`メソッドを呼び出し、テストアカウントにログインします。戻り値`res.code`が0であれば、ログインは成功です。
```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';
 const res = await TencentImSDKPlugin.v2TIMManager.login(
    userID: userID,
    userSig: userSig,
  );
```
> ? このアカウントは開発テストのみに使用します。アプリケーションのリリース前の`UserSig`の正しい発行方法は、`UserSig`の計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。`UserSig`が必要なときは、Appから業務サーバーにリクエストを送信し動的に`UserSig`を取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

#### メッセージの送信

ここでは、テキストメッセージの送信を例に挙げます。そのフローは次のとおりです：
1. `createTextMessage(String)`を呼び出してテキストメッセージを作成します。
2. 戻り値に基づいて、メッセージIDを取得します。
3. `sendMessage()`を呼び出して、このIDのメッセージを送信します。`receiver`には、その前に作成した別のテストアカウントIDを入力できます。シングルチャットメッセージを送信する場合は`groupID`の入力は不要です。

サンプルコード：

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

const createMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createTextMessage("The text to create");

const id = createMessage.data!.id!; // The message creation ID

const res = await TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .sendMessage(
          id: id, // Pass in the message creation ID to
          receiver: "The userID of the destination user",
          groupID: "The groupID of the destination group",
          );
```

> ?送信に失敗した場合は、sdkAppIDが知らない人宛てのメッセージ送信をサポートしていないことが原因の可能性があります。コンソールで有効にしてからテストに使用してください。
>
> [このリンクをクリック](https://console.cloud.tencent.com/im/login-message)して、フレンドリレーションシップチェーンのチェックを無効にしてください。

#### セッションリストの取得

前の手順でテストメッセージの送信が完了しましたので、別のテストアカウントでログインし、セッションリストをプルできるようになりました。

セッションリストの取得には次の2つの方法があります：

1. 長時間接続コールバックを監視し、セッションリストをリアルタイムに更新します。
2. APIをリクエストし、ページごとに一括でセッションリストを取得します。

一般的なユースケースは次のようなものです：

アプリケーションの起動後すぐにセッションリストを取得し、その後は長時間接続を監視して、セッションリストの変更をリアルタイムに更新します。

##### セッションリストの一括リクエスト

セッションリストを取得するためには`nextSeq`を保守し、現在の位置を記録する必要があります。

```typescript
import { useState } from "react";
import { TencentImSDKPlugin } from "react-native-tim-js";

const [nextSeq, setNextSeq] = useState<string>("0");

const getConversationList = async () => {
  const count = 10;
  const res = await TencentImSDKPlugin.v2TIMManager
    .getConversationManager()
    .getConversationList(count, nextSeq);
  setNextSeq(res.data?.nextSeq ?? "0");
};
```

この時点で、前の手順で別のテストアカウントを使用して送信したメッセージのセッションを見ることができるようになりました。

##### 長時間接続の監視によるセッションリストのリアルタイム取得

この手順では、先にSDKにリスナーをマウントしてからコールバックイベントを処理し、UIを更新する必要があります。

1. リスナーをマウントします。
```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const addConversationListener = () => {
  TencentImSDKPlugin.v2TIMManager
    .getConversationManager()
    .addConversationListener({
      onNewConversation: (conversationList) => {
        // new conversation created callback
        _onConversationListChanged(conversationList);
      },
      onConversationChanged: (conversationList) => {
        // conversation changed callback
        _onConversationListChanged(conversationList);
      },
    });
};
```

2. コールバックイベントを処理し、最新のセッションリストをインターフェース上に表示します。
```javascript
const _onConversationListChanged = (list) => {
  // you can use conversation list to update UI
};
```

#### メッセージの受信

Tencent Cloud IM React Native SDKによるメッセージの受信には2つの方法があります。

1. 長時間接続コールバックを監視し、メッセージの変更をリアルタイムに取得し、メッセージ履歴リストを更新してレンダリングします。
2. APIをリクエストし、ページごとに一括でメッセージ履歴を取得します。

一般的なユースケースは次のようなものです。

1. インターフェースが新しいセッションに入ると、まず一定量のメッセージ履歴を一括でリクエストし、メッセージ履歴リストの表示に用います。
2. 長時間接続を監視し、新しいメッセージをリアルタイムに受信してメッセージ履歴リストに追加します。

##### メッセージ履歴リストの一括リクエスト

ページごとに取得するメッセージ数が多すぎると取得速度に影響しますので、多すぎてはなりません。20通前後に設定することをお勧めします。

次のリクエストの際に使用できるよう、現在のページ数を動的に記録しなければなりません。

サンプルコードは次のとおりです：

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const getGroupHistoryMessageList = async () => {
  const groupID = "";
  const count = 20;
  const lastMsgID = "";
  const res = await TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .getGroupHistoryMessageList(groupID, count, lastMsgID);
  const msgList = res.data ?? [];
  // here you can use msgList to render your message list
};
```

##### 長時間接続の監視による新メッセージのリアルタイム取得

メッセージ履歴リストを初期化すると、新しいメッセージは長時間接続`V2TimAdvancedMsgListener.onRecvNewMessage`から受信します。

`onRecvNewMessage`コールバックがトリガーされると、必要に応じて新しいメッセージをメッセージ履歴リストに追加することができます。

リスナーをバインドするサンプルコードは次のとおりです：

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const adVancesMsgListener = {
  onRecvNewMessage: (newMsg) => {
    _onReceiveNewMsg(newMsg);
    /// ... other listeners related to message
  },
};

const addAdvancedMsgListener = () => {
  TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .addAdvancedMsgListener(adVancesMsgListener);
};
```

この時点で、IMモジュールの開発は基本的に完了し、メッセージの送受信や様々なセッションに入ることが可能になりました。
続いて、グループ、ユーザープロファイル、リレーションシップチェーン、オフラインプッシュ、ローカル検索などの関連機能の開発を完了することができます。詳細については、[SDK APIドキュメント](https://comm.qq.com/im/doc/RN/zh/)をご参照ください。

## よくあるご質問

#### demoを実行すると`Undefined symbols for architecture x86_64 [duplicate]`が表示されます。どうすればいいですか？

[ドキュメント](https://stackoverflow.com/questions/71933392/react-native-ios-undefined-symbols-for-architecture-x86-64)をご参照ください。

#### demoを実行すると`Failed to resolve: react-native-0.71.0-rc.0-debug`が表示されます。どうすればいいですか？

[ドキュメント](https://blog.csdn.net/weixin_44132277/article/details/127731985)をご参照ください。
