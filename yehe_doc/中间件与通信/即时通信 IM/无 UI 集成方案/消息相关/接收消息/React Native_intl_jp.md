## 機能説明

- `addAdvancedMsgListener`で受信したすべてのタイプのメッセージ（テキスト、カスタム、リッチメディアメッセージ）を監視します。関連のコールバックは`V2TimAdvancedMsgListener`プロトコルに定義されています。

## メッセージリスナーの設定

### 高度なメッセージリスナー

#### メッセージリスナーの追加

受信側が`addAdvancedMsgListener` ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/addAdvancedMsgListener.html))を呼び出して、高度なメッセージリスナーを追加します。一般的には、比較的早い時点で呼び出すことをお勧めします。例えば、チャットメッセージ画面を初期化した後。これでは、Appがタイムリーにメッセージを受信することを確保できます。

サンプルコードは以下の通りです：

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

TencentImSDKPlugin.v2TIMManager.getMessageManager().addAdvancedMsgListener(
        {
          onRecvC2CReadReceipt: ( receiptList) {},// C2C セッション既読通知（相手がmarkC2CMessageAsReadを呼び出すと、この通知は自分に届く）
          onRecvMessageModified: ( message) {},// メッセージが変更された
          onRecvMessageReadReceipts: ( receiptList) {},// メッセージ既読確認通知（自分から送信したメッセージでは既読確認がサポートされている場合、メッセージの受信側でsendMessageReadReceiptsが呼び出されると、この通知は自分に届く）
          onRecvMessageRevoked: ( messageid) {},// メッセージ取消しの通知を受信した
          onRecvNewMessage: ( message) {},// 新しいメッセージを受信した
          onSendMessageProgress: ( message,  progress) {},// メッセージアップロード進捗イベント
        }
);
```

#### リスナーのリムーブ

メッセージを受信したくない場合、受信側で`removeAdvancedMsgListener` ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/removeAdvancedMsgListener.html))を呼び出して、高度なメッセージリスナーを削除できます。

サンプルコードは以下の通りです：

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

// listenerを作成する
const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {},
    onSendMessageProgress: (message, progress) {},
  };
// listenerを登録する
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
// listenerを削除する
TencentImSDKPlugin.v2TIMManager.getMessageManager().removeAdvancedMsgListener(listener);
```

## テキストメッセージの受信

受信側で高度なリスナーを使用して、1対1チャットとグループチャットのテキストメッセージを受信するには、以下を実施してください：

1. `addAdvancedMsgListener`を呼び出してイベントリスナーを設定します。
2. `onRecvNewMessage` ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Callback/OnRecvNewMessage.html))コールバックを監視し、その中でテキストメッセージを受信します。
3. メッセージを受信したくない場合、`removeAdvancedMsgListener`を呼び出してリスナーを削除します。このステップは必須ではありません。必要に応じて呼び出してください。

サンプルコードは以下の通りです：

```javascript

import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT){
        const text = message.textElem.text;
      }
    },
    onSendMessageProgress: (message, progress) {},
  };
TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
```

## カスタムメッセージの受信

受信側で高度なリスナーを使用して、1対1チャットとグループチャットのカスタムメッセージを受信するには、以下を実施してください：

1. `addAdvancedMsgListener`を呼び出してイベントリスナーを設定します。
2. `onRecvNewMessage` ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Callback/OnRecvNewMessage.html))コールバックを監視し、その中でカスタムメッセージを受信します。
3. メッセージを受信したくない場合、`removeAdvancedMsgListener`を呼び出してリスナーを削除します。このステップは必須ではありません。必要に応じて呼び出せばよいです。

サンプルコードは以下の通りです：

```javascript
import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM){
        const text = message.textElem.text;
        const data = message.customElem.data;
        const desc = message.customElem.desc;
        const ext = message.customElem.extension;
      }
    },
    onSendMessageProgress: (message, progress) {},
  };
TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
```

## リッチメディアメッセージの受信

リッチメディアメッセージを受信するには、高度なリスナー**しか使用できません**。以下を実施してください：

1. 受信側で`addAdvancedMsgListener`インターフェースを呼び出して、高度なメッセージリスナーを設定します。
2. 受信側で`onRecvNewMessage` ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Callback/OnRecvNewMessage.html))コールバックを監視し、メッセージV2TimMessageを取得します。
3. 受信側でメッセージV2TIMMessage中のelemType属性を解析し、そのタイプによって二次解析を行い、メッセージ内部のElemの中身を取得します。
4. メッセージを受信したくない場合、`removeAdvancedMsgListener`を呼び出してリスナーを削除します。このステップは必須ではありません。必要に応じて呼び出せばよいです。

### 画像メッセージ

1つの画像メッセージには、３種類のサイズの画像が含まれます。それぞれオリジナル画像、標準画像、縮小画像です（SDKが画像メッセージを送信する時、自動的に標準画像と縮小画像を作成する。お客様はそれを意識しない）
標準画像：オリジナル画像を同じ比率で圧縮します。圧縮後に、幅と高さのうち比較的小さい方が720画素になります。
縮小画像：オリジナル画像を同じ比率で圧縮します。圧縮後に、幅と高さのうち比較的小さい方が198画素になります。

リッチメディアメッセージはメッセージリストを取得する時にメッセージのurlを返さないため、getMessageOnlineUrl ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html))を使用して取得する必要があります。
リッチメディアメッセージはデフォルトではlocalurlを返しません。downloadMessage ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html))でメッセージを正常にダウンロードした後、localurlが返されます。

以下のサンプルコードでは、V2TimMessageから画像メッセージの中身を解析する方法を示します。

```javascript
import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE){
        const path = message
            .imageElem.path; // 画像のアップロードパス。メッセージの送信者だけにこのフィールドがある。メッセージの送信者はこのフィールドを使用し、画像を事前に表示し、表示効果を最適化できる。
        message.imageElem.imageList.map(item => { // 標準画像、オリジナル画像、縮小画像をトラバース
          // 画像の属性を解析する
          const height = item.height;
          const localUrl = item.localUrl;
          const size = item.size;
          const type = item.type; // 標準画像、縮小画像、オリジナル画像
          const url = item.url;
          const uuid = item.uuid;
          const width = item.width;
        })
      }
    TencentImSDKPlugin.v2TIMManager
       .getMessageManager()
       .getMessageOnlineUrl(message.msgID);

    TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(message, 3, 0, false);
    },
    onSendMessageProgress: (message, progress) {},
  };
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);


```

### ビデオメッセージ

受信側でビデオメッセージを受信した後、通常チャット画面にビデオのプレビューが表示されます。メッセージをクリックしないと、ビデオを再生しません。
この場合、以下の処理が必要です：

リッチメディアメッセージはメッセージリストを取得する時にメッセージのurlを返さないため、getMessageOnlineUrl ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html))を使用して取得する必要があります。
リッチメディアメッセージはデフォルトではlocalurlを返しません。downloadMessage ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html))でメッセージを正常にダウンロードした後、localurlが返されます。

以下のサンプルコードでは、V2TimMessageからビデオメッセージの中身を解析する方法を示します：

```javascript
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO){
  // ビデオメッセージの属性、サムネイル、再生アドレス、幅と高さ、サイズなどを解析する
  message.videoElem.UUID;
  message.videoElem.duration;
  message.videoElem.localSnapshotUrl;
  message.videoElem.localVideoUrl;
  message.videoElem.snapshotHeight;
  message.videoElem.snapshotPath;
  // ...
  TencentImSDKPlugin.v2TIMManager
     .getMessageManager()
     .getMessageOnlineUrl(message.msgID);

  TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(message, 5, 0, true);
}
```

### 音声メッセージ

リッチメディアメッセージはメッセージリストを取得する時にメッセージのurlを返さないため、getMessageOnlineUrl ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html))を使用して取得する必要があります。
リッチメディアメッセージはデフォルトではlocalurlを返しません。downloadMessage ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html))でメッセージを正常にダウンロードした後、localurlが返されます。

以下のサンプルコードでは、V2TimMessageから音声メッセージの中身を解析する方法を示します：

```javascript
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND){
  // 音声メッセージの再生アドレス、ローカルアドレス、サイズ、時間の長さなどを解析する
  message.soundElem.UUID;
  message.soundElem.dataSize;
  message.soundElem.duration;
  message.soundElem.localUrl;
  message.soundElem.url;
  // ...
  TencentImSDKPlugin.v2TIMManager
     .getMessageManager()
     .getMessageOnlineUrl(message.msgID);

  TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(message, 4, 0, true);
}
```

### ファイルメッセージ

React Native SDKはアイドル時に音声メッセージをAppローカルにダウンロードします。開発者はそのまま利用できます。ローカルファイルメッセージはAPPをアンインストールする時にクリアされます

以下のサンプルコードでは、V2TimMessageからファイルメッセージの中身を解析する方法を示します：

```javascript
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE){
  // ファイルメッセージのファイル名、サイズ、urlなどを解析する
  message.fileElem.UUID;
  message.fileElem.fileName;
  message.fileElem.fileSize;
  message.fileElem.localUrl;
  message.fileElem.path;
  message.fileElem.url;

  TencentImSDKPlugin.v2TIMManager
     .getMessageManager()
     .getMessageOnlineUrl(message.msgID);

  TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(message, 6, 0, true);
}
```

### 地理的位置メッセージ

地理的位置メッセージを受信した後、受信側で`locationElem`から直接緯度と経度の情報を解析できます。
以下のサンプルコードでは、V2TimMessageから地理的位置メッセージの中身を解析する方法を示します：

```javascript
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION){
  // 地理的位置メッセージの緯度・経度、詳細などを解析する
  message.locationElem.desc;
  message.locationElem.latitude;
  message.locationElem.longitude;
}
```

### スタンプメッセージ

SDKはスタンプメッセージにパススルーのコネクションを提供するだけです。メッセージの中身フィールドは、`faceElem` ([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Interface/Message/V2TimFaceElem.html))の定義をご参照ください。そのうち、`index`と`data`はお客様が設定します。

例えば、送信側でindex = 1、data = "x12345"を「微笑」スタンプとして設定した場合、「微笑」スタンプを表示します。
受信側でスタンプメッセージを受信し1と「x12345」に解析し、事前に設定されたルールに従って、「微笑」スタンプを表示します。

以下のサンプルコードでは、V2TIMMessageからスタンプメッセージの中身を解析する方法を示します：

```javascript
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE){
  message.faceElem.data;
  message.faceElem.index;
}
```

### グループtipsメッセージ

グループtipsメッセージは、グループの中でユーザが受信する一般メッセージ以外の通知メッセージを指します。例えば、「管理者がaliceさんからグループチャットから削除しました」 「bobさんがグループ名を○○に変更しました」など。

> ? グループtipsメッセージはグループチャットのメンバーだけが受信し、1対1チャット
> のメンバーは受信しません。

グループtipsメッセージには複数のタイプがあります。詳しくは、`V2TIMGroupTipsElem`([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Interface/Message/V2TimGroupTipsElem.html)) の定義をご参照ください。


受信側でグループtipsメッセージを受信した後、通常以下の処理を実行します：

1. `V2TIMGroupTipsElem`の各フィールドを解析します
2. typeでこのtipsメッセージのタイプを判断します
3. タイプによって、他のフィールドを合わせて表示する内容を組み立てます。

以下に例を挙げます。
受信側でtype = `V2TIM_GROUP_TIPS_TYPE_GROUP_INFO_CHANGE`が解析されたため、グループプロフィール変更の通知だと分かります。
受信側で`opMember`から操作者、`groupChangeInfoList`から変更後のグループ名を取得できます。
すると、「操作者」と「変更後のグループ名」を組み立てて、グループ通知を構成できます。例えば、「aliceさんがグループ名をgroup123に変更しました」。

以下のサンプルコードでは、V2TIMMessageからグループtipsメッセージの中身を解析する方法を示します：

```javascript
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS){
  message.groupTipsElem.groupID; // 所属するグループ
  message.groupTipsElem.type; // グループTipsのタイプ
  message.groupTipsElem.opMember; // 操作者のプロフィール
  message.groupTipsElem.memberList; // 操作対象となる者のプロフィール
  message.groupTipsElem.groupChangeInfoList; // グループ情報の変更詳細
  message.groupTipsElem.memberChangeInfoList; // グループメンバーの変更情報
  message.groupTipsElem.memberCount; // 現在のオンライングループメンバー数
}
```

## 複数Elemのメッセージの受信

1. `Message`オブジェクトから1番目の`Elem`オブジェクトを解析します。
2. 1番目のElemオブジェクトのnextElemメソッドから次のElemオブジェクトを解析します。次のElemオブジェクトがあれば、Elemオブジェクトインスタンスが返されます。存在しなければ、nullが返されます。

サンプルコードは以下の通りです：

```javascript
if (message.textElem.nextElem != null) {
  // 次のメッセージがある
}
```
