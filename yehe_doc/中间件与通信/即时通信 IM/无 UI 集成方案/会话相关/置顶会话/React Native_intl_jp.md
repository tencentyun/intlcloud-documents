## 機能説明

セッションの先頭固定表示は、セッションを簡単に特定できるように、友達とのセッションまたはグループセッションをセッションリストの一番上に表示する機能です。先頭固定表示の状態がサーバーに保存されているため、端末デバイスを切り替えた場合、先頭固定表示の状態は新しいデバイスに同期されます。

>!先頭固定表示可能なセッションは50であり、これ以上設定できません。

## セッションの先頭固定表示

`pinConversation`([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/pinConversation.html))インターフェースを呼び出して、セッションを先頭固定表示するかを設定できます。

セッションは、`V2TimConversation`オブジェクトの`orderKey`フィールドでソートされます。`orderKey`フィールドは整数型です。新しいメッセージを送受信する時、下書きまたはセッションの先頭固定表示を設定する時、セッションが有効化され、`orderKey`フィールドの値が大きくなります。

先頭固定表示を設定したセッションは常に先頭固定表示を設定していないセッションの上に表示されることに注意してください。複数のセッションを先頭固定表示に設定した場合、これらのセッション同士の相対順番は固定されます。例えば、5つのセッション1、2、3、4、5が順番に並んでおり、セッション2と3を先頭固定表示に設定すれば、セッションの並び順が2、3、1、4、5に変わります。セッション2と3が一番上に表示され、セッション2がセッション3の上に表示されます。

`getConversationList`を呼び出してセッションリストを取得する時、このインターフェースは先頭固定表示されているセッションを先に返してから、 先頭固定表示されていないセッションを返します。`V2TIMConversation`オブジェクトの`isPinned`フィールドで、セッションが先頭固定表示されているかを確認できます。

サンプルコードは以下の通りです：

```javascript
// isPinnedパラメーターがtrueの場合、セッションが先頭固定表示されている。そうではない場合、先頭固定表示されていない。
const isPinned = true;
conversationManager.pinConversation("conversationID", isPinned);
```

## 先頭固定表示変更の通知

事前に`addConversationListener`([詳細はこちら](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/addConversationListener.html))を呼び出してセッションリスナーを追加した場合、`onConversationChanged`から`V2TimConversation`オブジェクトの`isPinned`フィールドの値を取得できます。このフィールドでセッションの先頭固定表示に変更があったかを判断できます。
サンプルコードは以下の通りです：

```javascript
conversationManager.addConversationListener({
  onConversationChanged: (conversationList) => {
    // 変更後の最新のセッション
  },
});
```
