## 機能説明
IM SDKは友達の管理をサポートしています。これにより、ユーザーは自主的的に友達の追加と削除を行うことができるほか、友達にのみメッセージを送信できるように設定することもできます。

### 友達リストの取得
IM SDKがフレンドシップチェーンのロジックをサポートしています。`FriendshipGetFriendProfileList`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipGetFriendProfileList.html))を呼び出すことで、友達リストを取得できます。

サンプルコードは次のとおりです：


```c#
// 友達リストを取得する
TIMResult res = TencentIMSDK.FriendshipGetFriendProfileList((int code, string desc, List<FriendProfile> profile_list, string user_data)=>{
 // 非同期処理のロジック
});
```



### 友達の追加
`FriendshipAddFriend`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipAddFriend.html))インターフェースを呼び出すことで、友達を追加できます。

サンプルコードは次のとおりです：


```c#
// お互いに友達として追加する
FriendshipAddFriendParam param = new FriendshipAddFriendParam
{
  friendship_add_friend_param_identifier = "friend_userid",
  friendship_add_friend_param_friend_type = TIMFriendType.FriendTypeBoth,
  friendship_add_friend_param_remark = "nickname",
  friendship_add_friend_param_add_wording = "greeting"
};
TIMResult res = TencentIMSDK.FriendshipAddFriend(param, (int code, string desc, FriendResult result, string user_data)=>{
 // 非同期処理のロジック
});
```


相手のユーザー情報における、友達追加の設定状況（承認が必要かどうか）に応じて、処理方法が2つ分けられます：

#### 状況1：友達を追加するときに相手による承認が不要です
1. ユーザーAとBは`SetOnAddFriendCallback`を呼び出してリレーションシップチェーンのリスナーを設定します。
2. ユーザーBは`ProfileModifySelfUserProfile`関数の`user_profile_item_add_permission`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/UserApi/ProfileModifySelfUserProfile.html))フィールドで、友達追加時に承認が不要である（`kTIMProfileAddPermission_AllowAny`）ように設定します。
3. ユーザーAが`FriendshipAddFriend`を呼び出してBを友達として追加することを申請すると、追加は完了します。追加完了後、申請パラメータ`FriendshipAddFriendParam`の`friendship_add_friend_param_friend_type`の設定によって、次の2つの状況があります：
   * 相互的な友達(`TIMFriendType.FriendTypeBoth`)として設定されている場合、ユーザーAとBの両方は`OnAddFriendCallback`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/callback/OnAddFriendCallback.html))コールバックを受信します。
   * 一方的な友達（`TIMFriendType.FriendTypeSignle`）に設定されている場合、ユーザーAのみが`OnAddFriendCallback`コールバックを受信します。


#### 状況2：友達を追加するときに相手による承認が必要です
1. ユーザーAとBは`SetOnAddFriendCallback`を呼び出してリレーションシップチェーンの監視を設定します。
2. ユーザーBは`ProfileModifySelfUserProfile`関数の`user_profile_item_add_permission`フィールドで、友達追加時に承認が必要である（`kTIMProfileAddPermission_NeedConfirm`）ように設定します。
3. ユーザーAが`FriendshipAddFriend`を呼び出してBを友達として追加することを申請した後、インターフェースで正常にコールバックしたパラメータでは、`code`が30539を返した場合は、ユーザーBの承認を待つ必要があることを示します。
4. ユーザーBが`SetFriendAddRequestCallback`のコールバックを受信します。受け入れるか拒否するかを選択できます：
    - Bは`FriendshipHandleFriendAddRequest`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipHandleFriendAddRequest.html))を呼び出して、友達リクエストを受け入れます。パラメータの受け入れタイプが「一方的な友達追加のみを許可」（`TIMFriendResponseAction.ResponseActionAgree`）である場合：
      - Aが`OnAddFriendCallback`コールバックを受信する場合は、一方的な友達追加に成功したことを示します。
      - Bが`FriendApplicationListDeletedCallback`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListDeletedCallback.html))コールバックを受信します。このとき、BはAの友達になりますが、AはまだBの友達ではありません。
    - Bが`FriendshipHandleFriendAddRequest`を呼び出して友達リクエストを受け入れます。パラメータの受け入れタイプが「相互的な友達追加を許可」（`TIMFriendResponseAction.ResponseActionAgreeAndAdd`）である場合、AとBの両方が`OnAddFriendCallback`コールバックを受信すると、お互いの友達登録に成功しました。
    - Bが`FriendshipHandleFriendAddRequest`を呼び出してパラメータ`TIMFriendResponseAction.ResponseActionReject`を渡し、友達リクエストを拒否した場合、両方のユーザーが`FriendApplicationListDeletedCallback`コールバックを受信します。


### 友達の削除
`FriendshipDeleteFriend`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipDeleteFriend.html))インターフェースを呼び出すことで、友達関係を削除できます。

サンプルコードは次のとおりです：


```c#
// 相互的な友達を削除する
FriendshipDeleteFriendParam param = new FriendshipDeleteFriendParam
{
  friendship_delete_friend_param_friend_type = TIMFriendType.FriendTypeBoth,
  friendship_delete_friend_param_identifier_array = new List<string>
  {
    "user_id"
  }
};
TIMResult res = TencentIMSDK.FriendshipDeleteFriend(param, (int code, string desc, FriendResult result, string user_data)=>{
 // 非同期処理のロジック
});
```



### 友達関係の確認
`FriendshipCheckFriendType`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipCheckFriendType.html))インターフェースを呼び出すことで、友達関係を確認できます。

サンプルコードは次のとおりです：


```c#
// 友達と相互的（一方的）なの友達関係を持っているかどうかを検出します。
FriendshipCheckFriendTypeParam param = new FriendshipCheckFriendTypeParam
{
  friendship_check_friendtype_param_check_type = TIMFriendType.FriendTypeBoth,
  friendship_check_friendtype_param_identifier_array = new List<string>{
    "user_id"
  }
};
TIMResult res = TencentIMSDK.FriendshipCheckFriendType(param, (int code, string desc, List<FriendshipCheckFriendTypeResult> result_list, string user_data)=>{
 // 非同期処理のロジック
});
```


### 友達へのメッセージ送信のみを許可するように設定
IM SDKが個人チャットメッセージを送信するときに、デフォルトで友達関係を確認しません。カスタマーサービスのシナリオでは、ユーザーがコミュニケーションする前に、先にカスタマーサービスの担当者を友達として追加しなければならないことは、非常に不便です。そのため、このデフォルト設定は、オンラインカスタマーサービスなどのシナリオでよく使用されます。
先に友達を追加し、後でメッセージを送信するというインタラクション体験を実現するには、[IMコンソール](https://console.cloud.tencent.com/im) >【機能設定】>【ログインとメッセージ】>【友達関係の確認】で「個人チャットメッセージを送信してリレーションシップチェーンを確認」を有効にします。有効にすると、ユーザーは友達にのみメッセージを送信でき、ユーザーが友達以外のユーザーにメッセージを送信すると、SDKは20009エラーコードを報告します。
