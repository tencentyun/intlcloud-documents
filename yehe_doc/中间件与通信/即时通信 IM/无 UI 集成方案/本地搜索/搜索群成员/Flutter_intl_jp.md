## 機能説明
グループメンバー検索は、ローカルに保存されたことのあるグループメンバーだけを検索できます。例えば、取得したことのあるグループメンバーリスト、取得したことのあるグループメンバープロフィールなど。

> ? flutter sdk 3.8.0ではサポートされる。ライブストリーミンググループ(AVChatRoom)はローカルにグループメンバーを保存しないため、グループメンバー検索機能を使用できません。

## ローカルグループ検索
`searchGroupMembers` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/searchGroupMembers.html))インターフェースを呼び出してローカルグループメンバーを検索できます。
検索キーワード`keywordList`を設定し、検索範囲を指定できます。つまり、`memberUserID`、`memberNickName`、`memberRemark`、`memberNameCard`フィールドを検索するかを指定できます。

`searchGroupMembers`に渡したパラメータ`V2TIMGroupMemberSearchParam` ([詳細はこちら](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Group/V2TimGroupMemberSearchParam.html))における`groupIDList`が空（`null`/`nil`）かによって、以下の処理が実行されます：
- groupIDListが空の場合、すべてのグループのグループメンバーを検索します。返された検索結果はgroupIDで分類されます。
- groupIDListが空でない場合、指定したグループのグループメンバーを検索します。

サンプルコードは以下の通りです：



```dart
    //検索パラメータを設定する
    V2TimGroupMemberSearchParam param = V2TimGroupMemberSearchParam(
        groupIDList: [],// グループIDリストを指定する。nullの場合、すべてのグループのグループメンバーを検索する
        isSearchMemberNameCard: True,// グループメンバーの名刺を検索するかを設定する。デフォルトではtrueとする
        isSearchMemberRemark: true,// グループメンバーの備考を検索するかを設定する。デフォルトではtrueとする
        isSearchMemberNickName: true,// グループメンバーのニックネームを検索するかを設定する。デフォルトではtrueとする
        isSearchMemberUserID: true,// グループメンバーのuserIDを検索するかを設定する。デフォルトではtrueとする
        keywordList: []);// キーワードリストを検索する。最大5つまで検索可能
    //グループメンバーを検索する
    V2TimValueCallback<V2GroupMemberInfoSearchResult> searchGroupMembersRes =
        await TencentImSDKPlugin.v2TIMManager
            .getGroupManager()
            .searchGroupMembers(param: param); // グループメンバーの検索パラメータを検索する
    if (searchGroupMembersRes.code == 0) {
      // 検索成功
      searchGroupMembersRes.data?.groupMemberSearchResultItems;// グループメンバーの検索結果
    }
```





