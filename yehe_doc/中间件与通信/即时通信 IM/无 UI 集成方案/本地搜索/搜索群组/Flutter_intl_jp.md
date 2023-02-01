## 機能説明
グループ検索は、追加されたグループリスト、プルされたグループ情報（プロフィール）など、ローカルで保存されたグループのみを検索できます。

> ? Flutter SDK 3.8.0ではサポートされています。

## ローカルグループの検索
インターフェース`searchGroups`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/searchGroups.html))を呼び出すことで、ローカルグループを検索できます。
検索キーワード`keywordList`を設定し、検索の範囲、つまりグループの`userID`、`groupName`フィールドを検索するかどうかを指定できます。

サンプルコードは次のとおりです：



```dart
//キーワードでグループを検索する
    // グループ情報を検索する検索条件
    V2TimGroupSearchParam param = V2TimGroupSearchParam(
        isSearchGroupID: true,//グループIDを検索するかどうか。既定値はtrueです。
        isSearchGroupName: true, // グループ名を検索するかどうか。既定値はtrueです。
        keywordList: []);// 検索キーワードリスト。最大5つまでです。
    // グループ情報を検索する
    V2TimValueCallback<List<V2TimGroupInfo>> searchGroupsRes =
        await TencentImSDKPlugin.v2TIMManager
            .getGroupManager()
            .searchGroups(searchParam: param);//グループ情報を検索する検索設定
    if (searchGroupsRes.code == 0) {
      //検索に成功しました
      searchGroupsRes.data?.forEach((element) {
        element.customInfo; // グループカスタムフィールド
        element.faceUrl; // グループのプロフィール写真Url
        element.groupAddOpt; // グループの追加オプションの設定
        element.groupID; // グループID
        element.groupName; // グループ名
        element.groupType; // グループタイプ
        element.introduction; // グループの説明
        element.isAllMuted; // グループで全員の発言が禁止されているかどうか
        element.isSupportTopic; // グループでトピック機能がサポートされているかどうか
        element.joinTime; // 現在のユーザーがこのグループに参加した時間
        element.lastInfoTime; // グループ情報の最終変更時間
        element.lastMessageTime; // グループメッセージの最終送信時間
        element.memberCount; // グループメンバーの人数
        element.notification; // グループのお知らせ
        element.onlineCount; // グループのオンライン人数
        element.owner; // グループオーナー
        element.recvOpt; // 現在のユーザーがこのグループでメッセージを受信するオプション
        element.role; // グループにおけるこのユーザーのロール
      });
    }
```





