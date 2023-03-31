## 機能説明
メッセージ拡張はメッセージにkey/valueタグを追加できます。メッセージ拡張をベースにし、投票、しりとり、アンケート調査などの機能を実装できます。
- 投票の運用し―ンでは、まず、`createCustomMessage` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html))インターフェースを呼び出し、投票に用いるカスタムメッセージを作成します。そのうち、`data`に投票のタイトルとオプションを保存します。 次に、メッセージ拡張keyに投票したユーザのIDを保存し、メッセージ拡張valueに投票したユーザのオプションを保存します。各ユーザが投票したオプションがあれば、オプションごとの投票したユーザがユーザ全員に占める比率を動的に計算できます。
- しりとりの運用し―ンでは、まず、`createCustomMessage`インターフェースを呼び出し、しりとりに用いるカスタムメッセージを作成します。そのうち、`data`にしりとりのタイトルを保存します。 次に、メッセージ拡張keyにしりとりをしたユーザのIDを保存し、メッセージ拡張valueにしりとりの情報を保存します。
- アンケート調査の運用し―ンでは、まず、`createCustomMessage`インターフェースを呼び出し、アンケート調査に用いるカスタムメッセージを作成します。そのうち、`data`にアンケートのタイトルとオプションを保存します。 次に、メッセージ拡張keyに調査対象となるユーザのIDを保存し、メッセージ拡張valueにアンケートの調査情報を保存します。

> ?
- この機能はUltimate版のユーザのみに提供し、[Ultimate版](https://buy.cloud.tencent.com/avc?from=17220)を購入後に使用できます。
- この機能はSDK 4.1.8以降でサポートされます。
- この機能を使用するには、[IMコンソール](https://console.cloud.tencent.com/im) > 機能設定 > ログインとメッセージ > メッセージ拡張で有効にする必要があります。
- コミュニテ(Community)とライブストリーミンググループ(AVChatRoom)のメッセージはこの機能をサポートしません。

### メッセージ拡張の設定
`setMessageExtensions` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/setMessageExtensions.html))インターフェースを呼び出してメッセージ拡張を設定できます。拡張keyがすでに存在している場合、拡張valueを変更します。拡張keyが存在しない場合、拡張を追加します。

メッセージ拡張インターフェースの入力パラメータの詳細は以下の通りです：
<table>
<thead>
<tr>
<th>属性</th>
<th>意味</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>message</td>
<td>メッセージオブジェクト</td>
<td>メッセージは次の3つの条件を満たす必要があります：<ul style="margin-bottom: 0px;"><li>メッセージを送信する前に、<code>supportMessageExtension</code> (<a href="https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/sendMessage.html">Flutter</a>)にYESを設定していること。</li><li>メッセージの状態は送信成功であること。</li><li>メッセージはコミュニティ(Community)とライブストリーミンググループ(AVChatRoom)のメッセージではないこと。</li></ul></td>
</tr>
<tr>
<td>extensions</td>
<td>拡張リスト</td>
<td>拡張keyがすでに存在している場合、拡張valueを変更します。拡張keyが存在しない場合、拡張を追加します。</td>
</tr>
</tbody></table>

> ?
> 1. 拡張keyは最大100バイトをサポートします。拡張valueは最大1KBをサポートします。1回で最大20拡張を設定できます。1通のメッセージに対して、最大300拡張を設定できます。
1. 複数のユーザが同時に同じ拡張keyを設定または削除する時、1番目のユーザだけが正常に削除できます。他のユーザは返されたメッセージからエラーコード23001と最新の拡張情報を受信します。エラーコードと最新の拡張情報を受信した後、必要に応じて再設定してください。
2. ユーザ同士が異なる拡張keyを設定することを強くお勧めします。そうすれば、ほとんどの運用シーンでは衝突が発生しません。例えば、投票、しりとり、アンケート調査の運用シーンでは、自分のuserIDを拡張keyとして設定するなど。

サンプルコードは次のとおりです：

```dart
    // メッセージ拡張を設定する
    V2TimValueCallback<List<V2TimMessageExtensionResult>>
        setMessageExtensionsRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .setMessageExtensions(msgID: '', // 拡張するメッセージのid
                extensions: []); // メッセージ拡張フィールド
    if (setMessageExtensionsRes.code == 0) {
      // 正常にメッセージ拡張を設定した
    }
```

### メッセージ拡張の取得

`getMessageExtensions` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageExtensions.html))インターフェイスを呼び出してメッセージ拡張リストを取得します。

> ? ネットワークに接続していない場合、SDKはそのままローカルにキャッシングされたメッセージ拡張リストを返します。

サンプルコードは次のとおりです：

```dart
    // メッセージ拡張を取得する
    V2TimValueCallback<List<V2TimMessageExtension>> getMessageExtensionsRes =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .getMessageExtensions(
              msgID: '', // 拡張情報を取得するメッセージのid
            );
    if (getMessageExtensionsRes.code == 0) {
      // 正常にメッセージ拡張を取得した
      getMessageExtensionsRes.data?.forEach((element) {
        element.extensionKey; // 変更された拡張フィールドkey
        element.extensionValue; // 変更された拡張フィールドvalues
      });
    }
```

### メッセージ拡張の削除

`deleteMessageExtensions` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/deleteMessageExtensions.html))インターフェースを呼び出し、指定したメッセージ拡張を削除します。`keys`フィールドに`null`が設定されている場合、すべてのメッセージ拡張が削除されます。

サンプルコードは次のとおりです：

```dart
    // メッセージ拡張の削除
    V2TimValueCallback<List<V2TimMessageExtensionResult>>
        deleteMessageExtensionsRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .deleteMessageExtensions(msgID: '', // 拡張を削除するメッセージのid
                keys: []); // 拡張フィールドを削除するkeyのリスト
    if (deleteMessageExtensionsRes.code == 0) {
      // 正常にメッセージ拡張を削除した
      deleteMessageExtensionsRes.data?.forEach((element) {
        element.extension; //メッセージ拡張情報
        element.resultCode; //実行結果コード
        element.resultInfo; //詳細情報
      });
    }
```

### メッセージ拡張の更新

事前に`addAdvancedMsgListener`を呼び出して高度なメッセージイベントリスナーを追加した場合、メッセージ拡張が追加または更新されると、`onRecvMessageExtensionsChanged` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvMessageExtensionsChanged.html))コールバックを受信します。メッセージ拡張が削除されると、`onRecvMessageExtensionsDeleted` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvMessageExtensionsDeleted.html))コールバックを受信します。

サンプルコードは次のとおりです：

```dart
    //メッセージリスナーを作成する
    V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
      onRecvMessageExtensionsChanged:
          (String msgID, List<V2TimMessageExtension> extensions) {
        // msgID　変更されたメッセージのid
        // extensions　変更された拡張フィールドのリスト
        for (V2TimMessageExtension element in extensions) {
          element.extensionKey; // 変更された拡張フィールドkey
          element.extensionValue; // 変更された拡張フィールドvalues
        }
      },
      onRecvMessageExtensionsDeleted: (msgID, extensionKeys) {
        // msgID　拡張メッセージが削除されたメッセージのid
        // extensionKeys 拡張メッセージが削除されたkeyのリスト
      },
    );
    // 高度なメッセージのイベントリスナーを追加する
    TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .addAdvancedMsgListener(listener: listener);
```
