## 機能説明
`addAdvancedMsgListener`を介してすべてのタイプのメッセージ（テキスト、カスタム、リッチメディアメッセージ）をリッスンして受信し、関連するコールバックは`V2TimAdvancedMsgListener`プロトコルで定義されます。


## メッセージリスナーの設定

### 高度なメッセージリスナー

#### リスナーの追加
受信側は、`addAdvancedMsgListener` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html))を呼び出して、高度なメッセージリスナーを追加します。一般的には、Appがチャットメッセージインターフェースの初期化後など、時間内にメッセージを確実に受信できるように、比較的早い時点で呼び出すことをお勧めします。

サンプルコードは次のとおりです：


```dart
    // メッセージリスナーの作成
    V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
      onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {
        //シングルチャット開封確認コールバック
      },
      onRecvMessageModified: (V2TimMessage message) {
        // msg変更後のメッセージオブジェクト
      },
      onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {
        //グループチャット開封確認コールバック
        receiptList.forEach((element) {
          element.groupID; // グループid
          element.msgID; // 開封確認されたメッセージID
          element.readCount; // グループメッセージの開封確認の数
          element.unreadCount; // グループメッセージの最新の未読数
          element.userID; //  C2Cメッセージ相手ID
        });
      },
      onRecvMessageRevoked: (String messageid) {
        // ローカルのメンテナンスメッセージで相手によって撤回されたメッセージを処理します
      },
      onRecvNewMessage: (V2TimMessage message) async {
        // テキストメッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT) {
          message.textElem?.text;
        }
        // カスタムメッセージを使用します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM) {
          message.customElem?.data;
          message.customElem?.desc;
          message.customElem?.extension;
        }
        // 画像メッセージを使用します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE) {
          message.imageElem
              ?.path; // 画像がアップロードされたときのパスです。このフィールドはメッセージの送信者のみ持ちます。メッセージの送信者はこのフィールドを使用して画像を画面に事前表示し、画面表示の体験を最適化できます。
          message.imageElem?.imageList?.forEach((element) {
            // 拡大図、オリジナル画像、サムネイルのトラバーサル
            // 画像属性を解析します
            element?.height;
            element?.localUrl;
            element?.size;
            element?.type; // 拡大図、オリジナル画像、サムネイル
            element?.url;
            element?.uuid;
            element?.width;
          });
        }
        // ビデオメッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO) {
          // カバー、再生アドレス、幅と高さ、およびサイズなどのビデオメッセージの属性を解析します。
          message.videoElem?.UUID;
          message.videoElem?.duration;
          message.videoElem?.localSnapshotUrl;
          message.videoElem?.localVideoUrl;
          message.videoElem?.snapshotHeight;
          message.videoElem?.snapshotPath;
          // ...
        }
        // オーディオメッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND) {
          // 再生アドレス、サイズ、時間などの音声メッセージを解析します。
          message.soundElem?.UUID;
          message.soundElem?.dataSize;
          message.soundElem?.duration;
          message.soundElem?.localUrl;
          message.soundElem?.url;
          // ...
        }
        // ファイルメッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE) {
          // ファイル名、ファイルサイズ、urlなどのファイルメッセージを解析します
          message.fileElem?.UUID;
          message.fileElem?.fileName;
          message.fileElem?.fileSize;
          message.fileElem?.localUrl;
          message.fileElem?.path;
          message.fileElem?.url;
        }
        // 位置メッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION) {
          // 緯度と経度、説明などの地理位置メッセージを解析します
          message.locationElem?.desc;
          message.locationElem?.latitude;
          message.locationElem?.longitude;
        }
        // 絵文字メッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
          message.faceElem?.data;
          message.faceElem?.index;
        }
        // グループtipsテキストメッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS) {
          message.groupTipsElem?.groupID; // 属するグループ
          message.groupTipsElem?.type; // グループTipsタイプ
          message.groupTipsElem?.opMember; // オペレーターデータ
          message.groupTipsElem?.opMember; // オペレーション対象のデータ
          message.groupTipsElem?.groupChangeInfoList; // グループメッセージ変更の詳細
          message.groupTipsElem?.memberChangeInfoList; // グループメンバーの変更情報
          message.groupTipsElem?.memberCount; // グループの現在オンライン人数
        }
        // マージされたメッセージを処理します
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_MERGER) {
          message.mergerElem?.abstractList;
          message.mergerElem?.isLayersOverLimit;
          message.mergerElem?.title;
          V2TimValueCallback<List<V2TimMessage>> download =
              await TencentImSDKPlugin.v2TIMManager
                  .getMessageManager()
                  .downloadMergerMessage(
                    msgID: message.msgID!,
                  );
          if (download.code == 0) {
            List<V2TimMessage>? messageList = download.data;
          }
        }
        if (message.textElem?.nextElem != null) {
          //最初のElemオブジェクトのnextElemメソッドを介して次のElemオブジェクトを取得します。次のElemオブジェクトが存在する場合はElemオブジェクトのインスタンスが返され、存在しない場合はnullが返されます。
        }
      },
      onSendMessageProgress: (V2TimMessage message, int progress) {
        //ファイルアップロード進行状況のコールバック
      },
    );
    // 高度なメッセージのイベントリスナーを追加します
    TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .addAdvancedMsgListener(listener: listener);
```


#### リスナーの削除
メッセージの受信を停止したい場合、受信側は、`removeAdvancedMsgListener` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/removeAdvancedMsgListener.html))を呼び出して、高度なメッセージリスナーを削除できます。

サンプルコードは次のとおりです：


```dart
// listenerを作成します
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {},
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
// listenerを登録します
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
// listenerを削除します
TencentImSDKPlugin.v2TIMManager.getMessageManager().removeAdvancedMsgListener(listener: listener);
```



## テキストメッセージの受信

受信側は高度なメッセージリスナーを使用して、シングルチャット、グループチャット、およびテキストメッセージを受信するには、次の手順が必要です：
1. `addAdvancedMsgListener`を呼び出して、イベントリスナーを設定します。
2. `onRecvNewMessage` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html))コールバックをリッスンし、その中でカスタムメッセージを受信します。
3. メッセージの受信を停止したい場合、`removeAdvancedMsgListener`を呼び出して、リスナーを削除します。この手順は必須ではなく、お客様は業務のニーズに応じて呼び出すことができます。

サンプルコードは次のとおりです：


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // テキストメッセージを処理します
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT){
        String text = message.textElem.text;
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



## カスタムメッセージの受信

受信側は高度なメッセージリスナーを使用して、シングルチャット、グループチャット、およびカスタムメッセージを受信するには、次の手順が必要です：
1. `addAdvancedMsgListener`を呼び出して、イベントリスナーを設定します。
2. `onRecvNewMessage` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html))コールバックをリッスンし、その中でカスタムメッセージを受信します。
3. メッセージの受信を停止したい場合、`removeAdvancedMsgListener`を呼び出して、リスナーを削除します。この手順は必須ではなく、お客様は業務のニーズに応じて呼び出すことができます。

サンプルコードは次のとおりです：


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // カスタムメッセージを使用します
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM){
        String data = message.customElem.data;
        String desc = message.customElem.desc;
        String ext = message.customElem.extension;
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



## リッチメディアメッセージの受信
リッチメディアメッセージを受信するには、高度なメッセージリスナーのみを**使用できます**。次の手順が必要です：
1. 受信側は`addAdvancedMsgListener`インターフェースを呼び出して、高度なメッセージリスナーを設定します。
2. 受信側は`onRecvNewMessage` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html))をリッスンしてコールバックすることによって、V2TimMessageメッセージを取得します。
3. 受信側はV2TIMMessageメッセージのelemType属性を解析し、そのタイプに従って二次解析を実行し、メッセージ内のElemの具体的な内容を取得します。
4. メッセージの受信を停止したい場合、`removeAdvancedMsgListener`を呼び出して、リスナーを削除します。この手順は必須ではなく、お客様は業務のニーズに応じて呼び出すことができます。




### 画像メッセージ

画像メッセージには、オリジナル画像、拡大図、サムネイルの3つの形式とサイズの画像が含まれます（SDKは、画像メッセージを送信するときにサムネイルと拡大図を自動的に生成します。お客様はそれを気にする必要はありません）。
拡大図：オリジナル画像を同じ比率で圧縮して、圧縮後に幅と高さの小さい方を720画素にしたもの。
サムネイル：オリジナル画像を同じ比率で圧縮して、圧縮後に幅と高さの小さい方を198画素にしたもの。

Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはメッセージリストの取得時にメッセージのurlが返されず、getMessageOnlineUrl ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))を使用して取得する必要があります。
Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはデフォルトでlocalurlが返されず、downloadMessage ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))を使用して、メッセージを正常にダウンロードした後でのみ、返されます。

サンプルコードは、V2TimMessageから画像メッセージの内容を解析する方法を示します。



```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) async {
      // 画像メッセージを使用します
      if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE) {
        String path = message
            .imageElem.path; // 画像がアップロードされたときのパスです。このフィールドはメッセージの送信者のみ持ちます。メッセージの送信者はこのフィールドを使用して画像を画面に事前表示し、画面表示の体験を最適化できます。
        for (var item in message.imageElem.imageList) { // 拡大図、オリジナル画像、サムネイルのトラバーサル
          // 画像属性を解析します
          int height = item.height;
          String localUrl = item.localUrl;
          int size = item.size;
          int type = item.type; // 拡大図、オリジナル画像、サムネイル
          String url = item.url;
          String uuid = item.uuid;
          int width = item.width;
        }
      }
      // マルチメディアメッセージURLを取得します
      V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
          await TencentImSDKPlugin.v2TIMManager
              .getMessageManager()
              .getMessageOnlineUrl(
                msgID: '', // メッセージid
              );
      if (getMessageOnlineUrlRes.code == 0) {
        // 取得に成功しました
      }

      // マルチメディアメッセージをダウンロードします
      V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(
              msgID: '', // メッセージid
              messageType: 3, // メッセージタイプ
              imageType: 0, // 画像タイプです。messageTypeが画像メッセージの場合のみ、有効です
              isSnapshot: false // ビデオカバーであるかどうか。messageTypeがビデオカバーメッセージの場合のみ、有効です
              );
      if (downloadMessageRes.code == 0) {
        // ダウンロードに成功しました
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



### ビデオメッセージ

受信側は通常、ビデオメッセージを受信した後にビデオプレビューイメージをチャットインターフェースに表示する必要があります。ビデオ再生は、ユーザーがメッセージをクリックした後でのみ、トリガーされます。

Flutter SDKは、アイドル時間中にビデオメッセージをAppローカルにダウンロードし、開発者はそれを直接使用できます。ローカルビデオとビデオカバーは、Appをアンインストールするときにクリアされます。サンプルコードは、V2TimMessageからビデオメッセージの内容を解析する方法を示します。

Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはメッセージリストの取得時にメッセージのurlが返されず、getMessageOnlineUrl ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))を使用して取得する必要があります。
Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはデフォルトでlocalurlが返されず、downloadMessage ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))を使用して、メッセージを正常にダウンロードした後でのみ、返されます。


```dart
     if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO){
  			// カバー、再生アドレス、幅と高さ、およびサイズなどのビデオメッセージの属性を解析します。
        message.videoElem.UUID;
        message.videoElem.duration;
        message.videoElem.localSnapshotUrl;
        message.videoElem.localVideoUrl;
        message.videoElem.snapshotHeight;
        message.videoElem.snapshotPath;
        // ...
      }

      // マルチメディアメッセージURLを取得します
      V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
          await TencentImSDKPlugin.v2TIMManager
              .getMessageManager()
              .getMessageOnlineUrl(
                msgID: '', // メッセージid
              );
      if (getMessageOnlineUrlRes.code == 0) {
        // 取得に成功しました
      }

      // マルチメディアメッセージをダウンロードします
      V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(
              msgID: '', // メッセージid
              messageType: 5, // メッセージタイプ
              imageType: 0, // 画像タイプです。messageTypeが画像メッセージの場合のみ有効です
              isSnapshot: false // ビデオカバーであるかどうか。messageTypeがビデオカバーメッセージの場合のみ有効です
              );
      if (downloadMessageRes.code == 0) {
        // ダウンロードに成功しました
      }
```


### 音声メッセージ

Flutter SDKは、アイドル時間中に音声メッセージをAppローカルにダウンロードし、開発者はそれを直接使用できます。ローカルの音声メッセージは、Appをアンインストールするときにクリアされます。サンプルコードは、V2TimMessageから音声メッセージの内容を解析する方法を示します。

Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはメッセージリストの取得時にメッセージのurlが返されず、getMessageOnlineUrl ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))を使用して取得する必要があります。
Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはデフォルトでlocalurlが返されず、downloadMessage ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))を使用して、メッセージを正常にダウンロードした後でのみ、返されます。

```dart
    if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND){
  			// 再生アドレス、サイズ、時間などの音声メッセージを解析します。
        message.soundElem.UUID;
        message.soundElem.dataSize;
        message.soundElem.duration;
        message.soundElem.localUrl;
        message.soundElem.url;
        // ...
        // マルチメディアメッセージURLを取得します
        V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
            await TencentImSDKPlugin.v2TIMManager
                .getMessageManager()
                .getMessageOnlineUrl(
                  msgID: '', // メッセージid
                );
        if (getMessageOnlineUrlRes.code == 0) {
          // 取得に成功しました
        }

        // マルチメディアメッセージをダウンロードします
        V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(
                msgID: '', // メッセージid
                messageType: 4, // メッセージタイプ
                imageType: 0, // 画像タイプです。messageTypeが画像メッセージの場合のみ有効です
                isSnapshot: false // ビデオカバーであるかどうか。messageTypeがビデオカバーメッセージの場合のみ有効です
                );
        if (downloadMessageRes.code == 0) {
          // ダウンロードに成功しました
        }
    }
```


### ファイルメッセージ

Flutter SDKは、アイドル時間中にファイルメッセージをAppローカルにダウンロードし、開発者はそれを直接使用できます。ローカルのファイルメッセージは、Appをアンインストールするときにクリアされます。サンプルコードは、V2TimMessageからファイルメッセージの内容を解析する方法を示します。

Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはメッセージリストの取得時にメッセージのurlが返されず、getMessageOnlineUrl ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))を使用して取得する必要があります。
Flutter SDK 5.0.4以降のバージョンでは、マルチメディアメッセージはデフォルトでlocalurlが返されず、downloadMessage ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))を使用して、メッセージを正常にダウンロードした後でのみ、返されます。

```dart

    if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE){
  			// ファイル名、ファイルサイズ、urlなどのファイルメッセージを解析します
        message.fileElem.UUID;
        message.fileElem.fileName;
        message.fileElem.fileSize;
        message.fileElem.localUrl;
        message.fileElem.path;
        message.fileElem.url;
        // マルチメディアメッセージURLを取得します
        V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
            await TencentImSDKPlugin.v2TIMManager
                .getMessageManager()
                .getMessageOnlineUrl(
                  msgID: '', // メッセージid
                );
        if (getMessageOnlineUrlRes.code == 0) {
          // 取得に成功しました
        }

        // マルチメディアメッセージをダウンロードします
        V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(
                msgID: '', // メッセージid
                messageType: 6, // メッセージタイプ
                imageType: 0, // 画像タイプです。messageTypeが画像メッセージの場合のみ有効です
                isSnapshot: false // ビデオカバーであるかどうか。messageTypeがビデオカバーメッセージの場合のみ有効です
                );
        if (downloadMessageRes.code == 0) {
          // ダウンロードに成功しました
        }
    }
```


### 地理的位置メッセージ

地理位置メッセージを受信した後、受信側は`locationElem`から緯度と経度メッセージを直接解析できます。
サンプルコードは、V2TimMessageから地理位置メッセージの内容を解析する方法を示します。



```dart

if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION){
  			// 緯度と経度、説明などの地理位置メッセージを解析します
        message.locationElem.desc;
        message.locationElem.latitude;
        message.locationElem.longitude;
}
```


### 顔絵文字メッセージ

SDKは、絵文字メッセージにのみメッセージのパススルーコネクションを提供します。メッセージ内容フィールドについては、`faceElem` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimFaceElem.html))をご参照ください。その中で、`index`および`data`の内容は、お客様にカスタマイズされます。

たとえば、送信側は、index = 1, data = "x12345"を設定すると、絵文字「笑顔」を示します。
受信側は、絵文字メッセージを受信した後に1と"x12345"を解析し、事前に設定されたルールに従って絵文字"笑顔"として表示します。

サンプルコードは、V2TIMMessageから絵文字メッセージの内容を解析する方法を示します。


```dart
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
        message.faceElem.data;
        message.faceElem.index;
}
```


### グループtipsメッセージ

グループtipsメッセージは、グループ内で通常のメッセージ以外に、ユーザーがプロンプトメッセージを受信することを示します。たとえば、「管理者がaliceをグループチャットから削除した」、「bobがグループ名をxxxxに変更した」などです。

> ? グループチャットメンバーのみがグループtipsメッセージを受信できます。シングルチャットメンバーは受信できません。

グループtipsメッセージにはさまざまなタイプがあります。`V2TIMGroupTipsType` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Group/V2TimGroupTipsElem.html))の定義をご参照ください。

受信側は、グループtipsメッセージを受信した後、次のことを行う必要があります：
1. `V2TIMGroupTipsElem`の各フィールドを解析します
2. typeに基づいてtipsメッセージがどのタイプであるかを判断します
3. タイプに応じて、他のフィールドと合わせて表示される内容を組み合わせます。

例：
受信側は、type = `V2TIM_GROUP_TIPS_TYPE_GROUP_INFO_CHANGE`を解析した場合は、これがグループデータの変更通知であることを示します。
受信側は、`opMember`からオペレーター情報を取得し、さらに`groupChangeInfoList`から変更されたグループ名を取得できます。
このとき、受信側は、「オペレーター」および「変更されたグループ名」を組み合わせて、グループプロンプトを作成できます。たとえば、「aliceは、グループ名をgroup123に変更した」。

サンプルコードは、V2TIMMessageからグループtipsメッセージの内容を解析する方法を示します。



```dart
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS){
        message.groupTipsElem.groupID; // 属するグループ
        message.groupTipsElem.type; // グループTipsタイプ
        message.groupTipsElem.opMember; // オペレーターデータ
        message.groupTipsElem.memberList; // オペレーション対象のデータ
        message.groupTipsElem.groupChangeInfoList; // グループメッセージ変更の詳細
        message.groupTipsElem.memberChangeInfoList; // グループメンバーの変更情報
        message.groupTipsElem.memberCount; // グループの現在オンライン人数
}
```


## 複数のElemメッセージの受信

1. `Message`オブジェクトによって、最初の`Elem`オブジェクトを正常に解析します。
2. 最初のElemオブジェクトのnextElemメソッドを介して次のElemオブジェクトを取得します。次のElemオブジェクトが存在する場合はElemオブジェクトのインスタンスが返され、存在しない場合はnullが返されます。

サンプルコードは次のとおりです：


```dart
if(message.textElem.nextElem!=null){
   // 次のメッセージが存在します
}
```
