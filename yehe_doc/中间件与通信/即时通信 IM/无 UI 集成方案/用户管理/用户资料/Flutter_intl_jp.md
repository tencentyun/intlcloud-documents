## 機能説明
ユーザーは、個人のニックネーム、プロフィール写真、署名などのプロフィール情報を設定・取得できるほか、知らない人のデータ情報を取得することもできます。関連する方法はコアクラスの` TencentImSDKPlugin.v2TIMManager.getFriendshipManager()`にあります。


## リレーションシップチェーンイベントのリスナー
`addFriendListener` ([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/addFriendListener.html))を呼び出すことで、リレーションシップチェーンイベントのリスナーを追加できます。

リレーションシップチェーンイベントの受信を中止する場合は、`removeFriendListener`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/removeFriendListener.html))を呼び出すことで、リレーションシップチェーンイベントのリスナーを削除できます。

> ! リレーションシップチェーンイベントのリスナーを事前に設定しておくだけで、以下の各種イベント通知を正常に受信できます。

サンプルコードは次のとおりです：


```dart
    //リレーションシップチェーンリスナーを設定する
    V2TimFriendshipListener listener = V2TimFriendshipListener(
      onBlackListAdd: (List<V2TimFriendInfo> infoList) async {
        //ブラックリストにおけるユーザーの追加に関するコールバック
        //infoList　追加されたユーザー情報の一覧
      },
      onBlackListDeleted: (List<String> userList) async {
        //ブラックリストの削除に関するコールバック
        //topicIDList    削除されたユーザーIDの一覧
      },
      onFriendApplicationListAdded:
          (List<V2TimFriendApplication> applicationList) async {
        //友達リクエスト数の増加に関するコールバック
        //applicationList 追加された友達リクエスト情報の一覧
      },
      onFriendApplicationListDeleted: (List<String> userIDList) async {
        //友達リクエスト数の減少に関するコールバック
        //減少した友達リクエストの送信ユーザーIDの一覧
      },
      onFriendApplicationListRead: () async {
        //友達リクエストの既読数に関するコールバック
      },
      onFriendInfoChanged: (List<V2TimFriendInfo> infoList) async {
        //友達情報の変更に関するコールバック
        //infoList 友達情報が変更された友達リスト
      },
      onFriendListAdded: (List<V2TimFriendInfo> users) async {
        //友達リストにおけるメンバーの追加に関するコールバック
        //users追加された友達情報の一覧
      },
      onFriendListDeleted: (List<String> userList) async {
        //友達リストにおけるメンバーの減少に関するコールバック
        //userList 減少した友達IDの一覧
      },
    );
    TencentImSDKPlugin.v2TIMManager
        .getFriendshipManager()
        .addFriendListener(listener: listener);//リレーションシップチェーンリスナーを追加する
//リレーションシップチェーンリスナーを削除する
 friendshipManager.removeFriendListener(listener: frindshipListener);
```



## ユーザー情報の管理
### 個人情報の表示と変更
`getUsersInfo`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getUsersInfo.html))インターフェースを呼び出すことで、個人情報を表示できます。そのうち、パラメータ`userIDList`に自分のUserIDを入力する必要があります。

`setSelfInfo`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/setSelfInfo.html))インターフェースを呼び出すことで、個人情報を変更できます。
情報が正常に変更されると、`onSelfInfoUpdated`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/V2TimUserFullInfoCallback.html))コールバックが受信されます。

サンプルコードは次のとおりです：


```dart
// 個人情報を取得する
V2TimValueCallback<String> self = await TencentImSDKPlugin.v2TIMManager.getLoginUser();
TencentImSDKPlugin.v2TIMManager.getUsersInfo(userIDList: [self.data]);

// 個人情報を設定する
 TencentImSDKPlugin.v2TIMManager.setSelfInfo(userFullInfo: V2TimUserFullInfo(nickName: "",role: 0,faceUrl: ""));

```


### 友達でないユーザー情報の表示
`getUsersInfo`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMManager/getUsersInfo.html))インターフェースを呼び出すことで、友達でないユーザー情報を表示できます。そのうち、パラメータ`userIDList`には、友達でないユーザーのUserIDを入力するだけでよいです。

> ? 友達でないユーザー情報を変更できません。

### 友達情報の表示と変更
`getFriendsInfo`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/getFriendsInfo.html))インターフェースを呼び出すことで、指定の友達情報を表示し、コールバック情報から`V2TIMFriendInfoResult`の`relation`フィールドを通じてユーザーと自分の関係を取得できます。

| relation                                          | 自分との関係                                           |
| ------------------------------------------------- | ------------------------------------------------------ |
| `V2TIM_FRIEND_RELATION_TYPE_NONE`                 | 友達でないことを示します。                             |
| `V2TIM_FRIEND_RELATION_TYPE_BOTH_WAY`             | お互いに友達であることを示します。                     |
| `V2TIM_FRIEND_RELATION_TYPE_IN_MY_FRIEND_LIST`    | 相手が自分の友達リストに登録されていることを示します。 |
| `V2TIM_FRIEND_RELATION_TYPE_IN_OTHER_FRIEND_LIST` | 自分が相手の友達リストに登録されていることを示します。 |



```dart
// 友達情報を取得する
V2TimValueCallback<List<V2TimFriendInfoResult>> friendsInfo = await friendshipManager.getFriendsInfo(userIDList: []);
```


`setFriendInfo`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/setFriendInfo.html))インターフェースを呼び出すことで、友達に対する注釈などの情報を変更できます。



```dart
// 友達情報を設定する
TencentImSDKPlugin.v2TIMManager.setSelfInfo(userFullInfo: V2TimUserFullInfo(nickName: "",role: 0,faceUrl: ""));
```


## よくある質問
### 拡張版で取得したユーザー情報が最新でないのはなぜですか？
拡張版SDKでのユーザー情報の更新は、友達と知らない人の2つの状況に分けられます。
 - 友達情報：友達情報が更新されると、バックグラウンドがシステム通知をSDKに自主的に送信するため、友達情報をリアルタイムで更新できます。
 - 知らない人の情報：知らない人の情報が更新されると、友達関係がないため、バックグラウンドはSDKにシステム通知を送信できず、情報をリアルタイムで更新できません。ユーザー情報が取得されるたびにバックグラウンドへのネットワークリクエストを送信することを避けるために、SDKはキャッシュロジックを追加し、同じユーザーのバックグラウンドから自主的にデータをプルする時間間隔は10分となっています。
