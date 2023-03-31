## 機能説明
IM SDKは友達の管理をサポートしています。これにより、ユーザーは自主的的に友達の追加と削除を行うことができるほか、友達にのみメッセージを送信できるように設定することもできます。

### 友達リストの取得
IM SDKがフレンドシップチェーンのロジックをサポートしています。`getFriendList`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendList.html))を呼び出すことで、友達リストを取得できます。

サンプルコードは次のとおりです：


```dart
// 友達リストを取得する
V2TimValueCallback<List<V2TimFriendInfo>> friendsList = await friendshipManager.getFriendList();
```



### 友達の追加
`addFriend`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addFriend.html))インターフェースを呼び出すことで、友達を追加できます。

サンプルコードは次のとおりです：


```dart
// お互いに友達として追加する
V2TimValueCallback<V2TimFriendOperationResult> addFriend = await friendshipManager.addFriend(userID: "userID",remark:"友達追加時の注釈",addWording:"備考",addType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH);
```


相手のユーザー情報における、友達追加の設定状況（承認が必要かどうか）に応じて、処理方法が2つ分けられます。

#### 状況1：友達を追加するときに相手による承認は不要です
1. ユーザーAとBは`setFriendListener`を呼び出してリレーションシップチェーンのリスナーを設定します。
2. ユーザーBは`setSelfInfo`関数の`allowType`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/User/V2TimUserFullInfo.html#allowtype))フィールドで、友達追加時に承認が不要である（`V2TIM_FRIEND_ALLOW_ANY`）ように設定します。
3. ユーザーAが`addFriend`を呼び出してBを友達として追加することを申請すると、追加が完了です。追加完了後、申請パラメータ`V2TIMFriendAddApplication`の`addType`の設定によって、次の2つの状況があります：
   * 相互的な友達(`V2TIM_FRIEND_TYPE_BOTH`)として設定されている場合、ユーザーAとBの両方は`onFriendListAdded`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnFriendListAddedCallback.html))コールバックを受信します。
   * 一方的な友達（`V2TIM_FRIEND_TYPE_SINGLE`）に設定されている場合、ユーザーAのみが`onFriendListAdded`コールバックを受信します。


#### 状況2：友達を追加するときに相手による承認が必要です
1. ユーザーAとBは`setFriendListener`を呼び出してリレーションシップチェーンの監視を設定します。
2. ユーザーBは`setSelfInfo`関数の`allowType`フィールドで、友達追加時に承認が必要である（`V2TIM_FRIEND_NEED_CONFIRM`）ように設定します。 
3. ユーザーAが`addFriend`を呼び出してBを友達として追加することを申請した後、インターフェースで正常にコールバックしたパラメータでは、`resultCode`が30539を返した場合は、ユーザーBの承認を待つ必要があることを示します。同時に、AとBの両方が`onFriendApplicationListAdded`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnFriendApplicationListAddedCallback.html))のコールバックを受信します。
4. ユーザーBが`onFriendApplicationListAdded`のコールバックを受信します。パラメータ`V2TIMFriendApplication`の`type`が`V2TIM_FRIEND_APPLICATION_COME_IN`の場合、受け入れるか拒否するかを選択できます。
    - Bは`acceptFriendApplication`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/acceptFriendApplication.html))を呼び出して、友達リクエストを受け入れます。パラメータの受け入れタイプが「一方的な友達追加のみを許可」（`V2TIM_FRIEND_ACCEPT_AGREE`）である場合：
      - Aが`onFriendListAdded`コールバックを受信する場合は、一方的な友達追加に成功したことを示します。
      - Bが`onFriendApplicationListDeleted`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnFriendApplicationListDeletedCallback.html))コールバックを受信します。このとき、BはAの友達になりますが、AはまだBの友達ではありません。
    - Bが`acceptFriendApplication`を呼び出して友達リクエストを受け入れます。パラメータの受け入れタイプが「相互的な友達追加を許可」（`V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD`）である場合、AとBの両方が`onFriendListAdded`コールバックを受信すると、お互いの友達登録に成功しました。
    - Bが`refuseFriendApplication`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/refuseFriendApplication.html))を呼び出して友達リクエストを拒否した場合、両方のユーザーが`onFriendApplicationListDeleted`コールバックを受信します。


### 友達の削除
`deleteFromFriendList`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/deleteFromFriendList.html))インターフェースを呼び出すことで、友達関係を削除できます。

サンプルコードは次のとおりです：


```dart
// 相互的な友達を削除する
V2TimValueCallback<List<V2TimFriendOperationResult>> deleteres = await friendshipManager.deleteFromFriendList(deleteType: FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList:['user1']);
```



### 友達関係の確認
`checkFriend`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/checkFriend.html))インターフェースを呼び出すことで、友達関係を確認できます。

サンプルコードは次のとおりです。


```dart
// 友達と相互的（一方的）なの友達関係を持っているかどうかを検出します。
V2TimValueCallback<List<V2TimFriendCheckResult>> checkres = await friendshipManager.checkFriend(checkType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList: [] );
```


### 友達へのメッセージ送信のみを許可するように設定
IM SDKが個人チャットメッセージを送信するときに、デフォルトで友達関係を確認しません。カスタマーサービスのシナリオでは、ユーザーがコミュニケーションする前に、先にカスタマーサービスの担当者を友達として追加しなければならないことは、非常に不便です。そのため、このデフォルト設定は、オンラインカスタマーサービスなどのシナリオでよく使用されます。
先に友達を追加し、後でメッセージを送信するというインタラクション体験を実現するには、[IMコンソール](https://console.cloud.tencent.com/im) >【機能設定】>【ログインとメッセージ】>【友達関係の確認】で「個人チャットメッセージを送信してリレーションシップチェーンを確認」を有効にします。有効にすると、ユーザーは友達にのみメッセージを送信でき、ユーザーが友達以外のユーザーにメッセージを送信すると、SDKは20009エラーコードを報告します。
