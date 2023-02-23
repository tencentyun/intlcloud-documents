## 機能説明
グループメンバー管理は、グループメンバーに対して実施するリスト取得、発言禁止、強制退会、権限付与、グループマスターの権限譲渡などの操作を指します。関連のメソッドは中核クラス `TencentImSDKPlugin.v2TIMManager.getGroupManager()`に存在します。

[](id:getGroupMemberList)

## グループメンバーリストの取得

`getGroupMemberList` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html))インターフェースを呼び出して指定したグループのグループメンバーを取得できます。このリストには各グループメンバーのプロフィール情報、例えば、ユーザID（`userID`）、グループ名刺（`nameCard`）、プロファイルフォト（`faceUrl`）、ニックネーム（`nickName`）、グループ参加時間（`joinTime`）などの情報が含まれています。

１つのグループには非常に多くのグループメンバー（5000+など）が存在する可能性があるため、グループメンバーリストを取得するインターフェースでは、フィルター（`filter`）とページごとの取得（`nextSeq`）これらの2つの高度な特徴がサポートされています。

### フィルター（filter）
`getGroupMemberList` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html))インターフェースを呼び出す時、`filter`で特定のロールの情報リストを取得するかを設定できます。

| フィルター                                                     | フィルタータイプ                   |
| ---------------------------------------------------------- | -------------------------- |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ALL    | すべてのグループメンバーの情報リストを取得する   |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_OWNER  | グループマスターの情報リストだけを取得する       |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN  | グループ管理者の情報リストだけを取得する   |
| GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_COMMON | 一般グループメンバーの情報リストだけを取得する |

サンプルコードは以下の通りです：



```java
// filterパラメータでグループマスターの情報だけを取得することを設定する
groupManager.getGroupMemberList(count: 10,filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN,nextSeq: '0',offset: 0,groupID: "",);
```


### ページごとの取得（nextSeq）
ほとんどの場合、UIにすべてのグループメンバーの情報を表示する必要がなく、グループメンバーリストの最初のページだけを表示すればよいです。ユーザが「次のページへ」をクリックするかリストページを上にスワップして更新する時のみ、より多くのグループメンバーを取得する必要があります。このようなシーンでは、ページごとの取得を使用してください。

ページごとの取得の使用手順は以下の通りです：
1. 初めて`getGroupMemberList`を呼び出す時、パラメータ`nextSeq`に0（セッションリストを最初から取得することを意味する）を指定し、1回で最大50グループメンバーを取得するように設定します。
2. 初めてグループメンバーリストを正常に取得した場合、`getGroupMemberList`のコールバック`V2TIMGroupMemberInfoResult`の実行結果に`nextSeq`（次回ページごとに取得するフィールド）が含まれます：
   * `nextSeq`が0の場合、すべてのグループメンバーが取得されました。
   * `nextSeq`が0より大きい場合、グループメンバーを依然として取得できます。この場合、ただちに「次のページ」のメンバーリストを取得する必要があるとは限りません。よく使用された通信ソフトウェアでは、ページごとの取得は通常ユーザのスワップ操作によって行われます。ユーザが上にスワップすると、1ページのメンバーリストが取得されます。
3. ユーザが引き続きグループメンバーリストを上にスワップする時、取得可能なグループメンバーが存在すれば、`getGroupMemberList`インターフェースを呼び出し、新しい`nextSeq`パラメータを渡します（`nextSeq`の値は前回の取得処理で返された`V2TIMGroupMemberInfoResult`オブジェクトから取得する）。
4. `nextSeq`が0になるまで「ステップ3」を繰り返し、取得を終了します。

サンプルコードは以下の通りです：



```java
// filterパラメータでグループマスターのプロフィールだけを取得することを設定する
groupManager.getGroupMemberList(count: 10,filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN,nextSeq: '0',offset: 0,groupID: "",);
```


[](id:mute)
## 発言禁止

### 指定したグループメンバーに対する発言禁止
グループのマスターまたは管理者は`muteGroupMember` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html))を呼び出し、指定したグループメンバーに対して発言禁止と発言禁止時間を設定できます。発言禁止時間は秒単位で指定します。発言禁止の情報はグループメンバーの`muteUtil`フィールドに保存されます。

グループメンバーに対して発言禁止を設定した後、グループメンバー全員（発言禁止されたグループメンバーを含む）が`onMemberInfoChanged` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnMemberInfoChangedCallback.html))コールバックを受信します。

### グループ全体の発言禁止
グループのマスターまたは管理者は`setGroupInfo` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html))インターフェースを呼び出し、グループ全体に対して発言禁止を設定できます。具体的には、`allMuted`フィールドに`true`を設定します。グループ全体の発言禁止には時間上の制限がありません。グループプロフィール`setAllMuted(false)`で発言禁止を解除できます。

> ? グループ全体に対して発言禁止を設定すると、`onGroupInfoChanged` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnGroupInfoChangedCallback.html))コールバックが実行されます。この機能はデフォルトでは無効になっており、コンソールで手動で有効にすることができます。
>  方法：[IMコンソールのグループ設定モジュール](https://console.cloud.tencent.com/im/qun-setting)に入って、グループシステム通知設定を選択し、各タイプのグループに対して**編集**をクリックし、「グループ全体発言禁止変更通知」を変更します。

サンプルコードは以下の通りです。
```dart
// グループメンバーuserBを10分間発言禁止する
groupManager.muteGroupMember(groupID: '',userID: 'userB',seconds: 10);

// 全員発言禁止
groupManager.setGroupInfo(info: V2TimGroupInfo(isAllMuted: true,groupID: '',groupType: 'Public'));

TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) {
    //グループメンバーの情報を変更する
  },
  onGroupInfoChanged: (groupID,info){
    // グループ情報を変更する
  }
  ));
```

>? グループマスターだけが管理者を発言禁止できます



[](id:kickGroupMember)
## 強制退会
グループのマスターまたは管理者は`kickGroupMember` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/kickGroupMember.html))インターフェースを呼び出し、指定した一般グループメンバーをグループから強制退会させることができます。

一般グループメンバーが強制退会されると、グループメンバー全員（強制退会されたメンバーを含む）が`onMemberKicked` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnMemberKickedCallback.html))コールバックを受信します。

ライブストリーミンググループ（AVChatRoom）にはグループ参加制限がないため、強制退会をサポートするインターフェースがありません。`muteGroupMember` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html)を呼び出して指定したメンバーを発言禁止することで、メンバーを管理できます。発言禁止の実施方法については、[発言禁止](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/muteGroupMember.html)をご参照ください。

>? グループマスターだけが管理者をグループから強制退会できます。

サンプルコードは以下の通りです：



```dart
groupManager.kickGroupMember(groupID: '',memberList: []);
```


## 管理者の設定
グループマスターは`setGroupMemberRole` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/setGroupMemberRole.html))を呼び出し、知らない人とのソーシャルグループ(Public)と臨時ミーティンググループ(Meeting)のグループメンバーに管理者の権限を付与できます。

一般グループメンバーは権限が付与されると、管理者と同じ権限を持ち、以下の操作を実施できるようになります：
* グループの基本情報を変更する
* 一般グループメンバーをグループから強制退会する
* 一般グループメンバーを発言禁止する（一定時間発言できないこと）
* グループ参加申請を処理する

詳しくは、[グループメンバーのロールの紹介](https://intl.cloud.tencent.com/document/product/1047/33529)をご参照ください。

一般グループメンバーは管理者の権限が付与されると、グループメンバー全員（権限が付与されたメンバーを含む）が`onGrantAdministrator` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnGrantAdministratorCallback.html))コールバックを受信します。

一般グループメンバーは管理者の権限が回収されると、グループメンバー全員（権限が回収されたメンバーを含む）が`onRevokeAdministrator` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRevokeAdministratorCallback.html))コールバックを受信します。

サンプルコードは次のとおりです：


```dart
groupManager.setGroupMemberRole(groupID: '',userID: '',role: GroupMemberRoleTypeEnum.V2TIM_GROUP_MEMBER_ROLE_ADMIN);

// 監視するロールを変更する
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) {

  },
  onGroupInfoChanged: (groupID,info){

  },
  onGrantAdministrator: (String groupID, V2TimGroupMemberInfo info, List<V2TimGroupMemberInfo> infolist){},
  onRevokeAdministrator: (String groupID, V2TimGroupMemberInfo info, List<V2TimGroupMemberInfo> infolist){},
  ));
```


[](id:transfer)

## グループマスターの権限の譲渡
グループマスターは[transferGroupOwner](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/transferGroupOwner.html)を呼び出して、グループマスターの権限を他のグループメンバーに譲渡できます。

グループマスターの権限が譲渡されると、グループメンバー全員が[onGroupInfoChanged](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnGroupInfoChangedCallback.html)コールバックを受信します。そのうち、`V2TIMGroupChangeInfo`のtypeは `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER`で、valueの値は新しいグループマスターのUserIDです。

サンプルコードは以下の通りです：



```dart
groupManager.transferGroupOwner(groupID: "", userID: "userID");
```


## オンライングループメンバー数を取得する
`getGroupOnlineMemberCount` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupOnlineMemberCount.html))を呼び出してオンライングループメンバー数を取得できます。

> ?
- 1. 現在、ライブストリーミンググループ（AVChatRoom）だけでは、オンライングループメンバー数の取得がサポートされます。
> 2. SDK呼出しの頻度は最大60秒に1回です。

サンプルコードは以下の通りです：


```dart
groupManager.getGroupOnlineMemberCount(groupID: '');
```

