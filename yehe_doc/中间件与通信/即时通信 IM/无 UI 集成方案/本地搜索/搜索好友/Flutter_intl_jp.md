## 機能説明
ユーザー検索は、プルされた友達リスト、プルされたユーザー情報（プロフィール）など、ローカルで保存されたユーザーのみを検索できます。

>?Flutter SDK 3.8.0ではサポートされています。

## ローカルユーザー情報の検索
インターフェース`searchFriends`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMFriendshipManager/searchFriends.html))を呼び出すことで、ローカルのユーザー情報を検索できます。
検索キーワード`keywordList`を設定し、検索の範囲、つまりユーザーの`userID`、`nickName`、`remark`フィールドを検索するかどうかを指定できます。

サンプルコードは次のとおりです：



```dart
//キーワードで友達を検索する
    //友達を検索する検索条件
    V2TimFriendSearchParam searchParam = V2TimFriendSearchParam(
      isSearchNickName: true,//ニックネームを検索するかどうか
      isSearchRemark: true,//備考を検索するかどうか
      isSearchUserID: true,//IDを検索するかどうか
      keywordList: [],//キーワードリスト。最大5つです。
    );
    V2TimValueCallback<List<V2TimFriendInfoResult>> searchFriendsRes =
        await TencentImSDKPlugin.v2TIMManager
            .getFriendshipManager()
            .searchFriends(searchParam: searchParam); //友達を検索する検索条件
    if (searchFriendsRes.code == 0) {
      //検索に成功しました
      searchFriendsRes.data?.forEach((element) {
        element.relation; //友達タイプ 0：友達ではない 1：相手が自分の友達リストにいる 2：自分が相手の友達リストにいる 3: お互いに友達である
        element.resultCode; //このレコードの検索結果のエラーコード
        element.resultInfo; //この検索結果の説明
        //friendInfoは友達の個人情報です。友達でない場合、userIDフィールドを除き、他のフィールドは空です。
        element.friendInfo
            ?.friendCustomInfo; //友達カスタムフィールド。まず、コンソール（機能設定 -> 友達カスタムフィールド）で友達カスタムフィールドを構成し、インターフェースを呼び出して設定する必要があります。
        element.friendInfo?.friendGroups; //友達が所属する分類リスト
        element.friendInfo?.friendRemark; //友達に対する注釈
        element.friendInfo?.userID; //ユーザーID
        element.friendInfo?.userProfile
            ?.allowType; //ユーザーの友達認証方法 0：全員からの友達追加を許可する １：全員からの友達追加を許可しない 2：自分を友達として追加するときに自分による確認が必要
        element.friendInfo?.userProfile?.birthday; //ユーザーの誕生日
        element.friendInfo?.userProfile?.customInfo; //ユーザーのカスタムステータス
        element.friendInfo?.userProfile?.faceUrl; //ユーザーのプロフィール写真url
        element.friendInfo?.userProfile?.gender; //ユーザーの性別 1：男 2：女
        element.friendInfo?.userProfile?.level; //ユーザーのレベル
        element.friendInfo?.userProfile?.nickName; //ユーザーのニックネーム
        element.friendInfo?.userProfile?.role; //ユーザーのロール
        element.friendInfo?.userProfile?.selfSignature; //ユーザーの自己紹介
        element.friendInfo?.userProfile?.userID; //ユーザーID
      });
    }
```
