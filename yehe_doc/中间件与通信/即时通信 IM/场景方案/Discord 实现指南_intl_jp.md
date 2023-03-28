## Discordの紹介

Discordはコミュニティのために設計された無料のインターネットインスタント通信ソフトとデジタル配信プラットフォームで、主にゲーマー、教育関係者、友人、ビジネス関係者を対象としており、ユーザー同士がソフトのチャットチャンネルでメッセージ、画像、ムービー、音声でコミュニケーションを取ります。

## Discordの概念

### サーバー

Discordには、一般的な通信ソフトのグループとは別のグループチャットとして、サーバー（コミュニティのようなもの）と呼ばれるものがあり、サーバーの所有者はサーバーの中に自分だけのコミュニティを作ることができます。

### チャネル

サーバーにチャンネルと呼ばれるチャットパイプを構築し、音声と文字に分けられます。音声チャンネルはゲームのライブ配信やチャットなどに利用されます。チャンネルでアイデンティティグループに様々な権限を設定することで、Discordコミュニティシステムをさらに多様化します。

### サブチャンネル

ユーザーは特定のトピックについてサブチャンネル内で議論します。

## 準備作業

### Tencent Cloud IMアプリの作成

このチュートリアルはTencent Cloud IMをベースにしているため、[Tencent Cloud IM Console](https://console.cloud.tencent.com/im)でアプリケーションを作成する必要があります。次の図を参照してください： 

アプリケーションを作成したら、[Tencent Cloud IM Consoleアプリケーション基本情報ページ](https://console.cloud.tencent.com/im/detail)で、アプリケーションの基本情報を確認します。

### 関連する設定と機能について

Tencent Cloud IMを使用してDiscord関連機能を実装するには、Tencent Cloud IMに関連する基本的な概念と、このチュートリアルの後述する専門用語を事前に理解しておく必要があります。

- SDKAppID：Tencent Cloud IMは各アプリケーションにSDKAppIDを割り当て、コンソールでアプリケーションを作成した後にアプリ詳細ページで確認できます。開発者は、Tencent Cloud IMクライアントのSDKを初期化し、ユーザーログイン用チケットを計算する際に使用できます。詳細については、UISDKなしの[初期化](https://intl.cloud.tencent.com/document/product/1047/47968)および[ログイン](https://intl.cloud.tencent.com/document/product/1047/47971)のドキュメントをご参照ください。
- キー：現在のアプリケーションキーはTencent Cloud IMコンソールのアプリケーション詳細ページに表示されます。SDKへのユーザーログイン用チケットの計算に使用されます。
- ユーザーアカウント：Tencent Cloud IMへログインするユーザーはTencent Cloud IMのアカウントシステムに含まれなければなりません。ユーザーがクライアントSDKを使用して正常に[ログイン]（https://intl.cloud.tencent.com/document/product/1047/47971）すると、Tencent Cloud IMバックグラウンドで自動的にIMユーザーが作成されます。また、Tencent Cloud IMが提供するサーバー側APIを使ってユーザーを[IMのユーザーシステムにインポート]（https://intl.cloud.tencent.com/document/product/1047/34953）することができます。
- グループ：これまでのIMでは、さまざまな場面で必要に応じて、[5種類のグループ](https://intl.cloud.tencent.com/document/product/1047/33529)を提供しています。ユーザーはグループ内で発言すると、グループのメンバーはメッセージを受け取ることができます。
- コールバックの設定：開発者は、IMが提供するクライアントSDKとサーバー側APIを積極的に統合するだけでなく、IMは特定のビジネスロジックの開始時に必要な情報を開発者サーバー側に自動的に戻します。開発者がTencent Cloud IMコンソールの[コールバック設定](https://console.cloud.tencent.com/im/callback-setting)モジュールで適切な設定を完了するだけで済みます。Tencent Cloud IMは豊富なコールバック設定を提供し、信頼性の高いコールバックを保証します。開発者はコールバックを通じて多くのカスタム要件を実現できます。
- カスタムフィールド：デフォルトでは、Tencent Cloud IMが開発者に提供するフィールドはほとんどのニーズに対応しています。フィールドを拡張するユーザーに対し、Tencent Cloud IMは、次のようなカスタムフィールドを各モジュールに提供しています。
    - [ユーザーカスタムフィールド](https://console.cloud.tencent.com/im/user-data)
    - [友達カスタムフィールド](https://console.cloud.tencent.com/im/friends-diy-vars)
    - [グループカスタムフィールド](https://console.cloud.tencent.com/im/qun-setting)
    - [グループメンバーのカスタムフィールド](https://console.cloud.tencent.com/im/qun-setting)
  >?ユーザーはカスタムフィールドを使用するには、コンソールで設定し、SDKのAPIを用いて読み書きしてください。

### クライアント側とサーバー側の統合SDK

Discord関連の機能を実装する際には、IMSDKを統合する必要があります。Tencent Cloud　IMは豊富で使いやすいSDKおよびサーバー側APIを提供しており、同じSDKAppIDでログインしたアプリケーションではすべての端末でメッセージの相互通信ができます。開発者は、ビジネスニーズのシナリオとテクノロジースタックに基づいて、適切なSDKを選択できます。

## Discord機能の分析 

上図に示すように、Discordの機能は主にサーバー、チャンネルおよびサブチャンネルに分けられており、サーバーとサーバーの間には王者栄耀サーバーや和平精英サーバーなど、コンテンツ上の違いがあります。サーバー内には文字チャンネル、音声チャンネル、ワールドチャンネルなど、さまざまなチャンネルを作れます。ユーザーのコミュニケーションは実際に各チャンネルで行われています。ユーザーはコミュニケーションしているコンテンツに対し他のアイデアを持っている場合、そのコンテンツについてサブチャンネルを作成してコミュニケーションを続けます。Discordのコアプレイはここで説明したとおりです。このチュートリアルでは、Tencent Cloud IMを使用して関連機能を実装する方法を1つずつ分析します。

>?**デモコードについては、このチュートリアルでAndroid側（Java SDK）の例を示しています。他のSDKインターフェースの呼び出しについては、[UIなしの統合方法](https://intl.cloud.tencent.com/document/product/1047/34306)をご参照ください。**

### サーバー

#### サーバーの作成 

分析の結果、Discordのサーバーリストには次のような特徴があります：

1. サーバーの人数が非常に多い場合があります。
2. ユーザーは実際にサーバーでコミュニケーションをとることはなく、サーバー内のチャンネルやサブチャンネルでのみチャットを行います。
3. サーバー内のチャット履歴にはローミングが必要です。
4. 自由に入ることができます。
5. サーバーにチャンネルを作成できます。

IMは5種類のグループを提供しているが、Discordのサーバーの特徴を見ると、[コミュニティ（Community）]（https://intl.cloud.tencent.com/document/product/1047/33529）だけがサーバーの特徴に合致しており、Tencent Cloud IMコミュニティは作成後に自由に出入りでき、最大10万人の同時オンラインと履歴メッセージの保存が可能で、ユーザーがグループIDを検索してグループ参加を申請すると、管理者の承認なしにグループに入れます。

サーバー（グループ）は、Tencent Cloud IMが提供するcreateGroupインターフェースで作成されます。作成したグループのタイプはCommunityであり、サーバーにチャンネルを作成するには[setSupportTopic](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#af97a85fc91302dbbdf0f6c0a0a022ccd)をtrueに設定する必要があります。デモコードは次のとおりです：

```java
V2TIMGroupInfo  groupinfo = new V2TIMGroupInfo();
groupinfo.setGroupName("テストサーバー");
groupinfo.setSupportTopic(true);
/// 初期グループメンバー
List<V2TIMCreateGroupMemberInfo> memberList = new LinkedList<V2TIMCreateGroupMemberInfo>();
// サーバーのアバターなどのその他の設定
V2TIMManager.getGroupManager().createGroup(groupinfo, memberList, new V2TIMValueCallback<String>() {
            @Override
            public void onError(int i, String s) {
                //　作成失敗
            }

            @Override
            public void onSuccess(String s) {
            	// 正常に作成されるとサーバーIDを返します
            }
});
```

インターフェースを正常に呼び出した後、onSuccessのコールバックでサーバーIDが返され、サーバーでのチャンネル作成機能で使用されます。

>!開発者は、IMが提供するサーバー側APIを使って、[サーバー側でサーバーを作成](https://intl.cloud.tencent.com/document/product/1047/34895)できます。主なパラメータは次のとおりです：
>
>```json
{
    "Type": "Community",     // グループタイプ（必須）
    "Name"："TestCommunityGroup",　//　コミュニティ名(必須)
    "SupportTopic"：1　　　　　　　　　　　　//　トピックオプションへの対応。対応の場合は1、非対応の場合は0。
}
```

###### サーバーリスト

Discordの左端にはサーバーリスト機能があり、ユーザーが参加しているサーバーのリストを示しています。コミュニティのシーンに合わせて、Tencent Cloud IMは検索用APIを提供しています。

```java
V2TIMManager.getGroupManager().getJoinedCommunityList(new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
            @Override
            public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
                // サーバーリストの取得に成功する場合は、返されたList<V2TIMGroupInfo>はサーバーリストの基本情報を示します。
            }

            @Override
            public void onError(int i, String s) {
              //　サーバーリストの取得に失敗する場合は、
            }
});
```

返された[V2TIMGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html)リストはサーバーの基本情報を示します。ただし、基本情報には、サーバーの未読数やカスタマイズ状態などに関する情報はありません。したがって、Discordのような効果を実現するには、IMが提供する別のAPIを使用する必要があります。サーバーリストの未読数は、後述のセクションで説明します。

#### サーバー分類

サーバーを作成すると、それぞれのサーバーがデフォルトの分類を作成し、作成後に新しい分類を作成することもできます。サーバーはTencent Cloud IMで基本的にコミュニティであるため、コミュニティのカスタムフィールドを設定することで実現できます。グループのカスタムフィールドを使用するには、次の2つのステップがあります：

1. コンソールでカスタムフィールドkeyを有効にします。
2. クライアントSDK/サーバー側APIで読み書きを実行します。 

クラスタカスタムフィールドの[サービス側API](https://intl.cloud.tencent.com/document/product/1047/34962)および[クライアント側SDK](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf)を設定します。

>!コミュニティはUltimate機能であり、コミュニティのカスタムフィールドを設定するには、まずUltimateを購入する必要があります。

#### サーバーメッセージ未読数&カスタムステータスの表示

![image-20221205031412051](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-12-04-191412.png)

![image-20221205031429070](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-12-04-191429.png)

前のセクションでは、参加済みサーバーリスト取得APIでは、未読数やサーバーの状態などの情報が返されないことを説明しました。注意すべき点として、このデータを取得するだけでなく、このデータの変化を監視してクライアントUIを更新する必要があります。サーバーはIMコミュニティを使用して実装され、IM内のコミュニティでセッションを生成しないため、すべてのパブリックチャンネルのセッションとプライベートチャンネルのセッションの合計を集計する必要があります。パブリックチャンネルの未読数は[V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html)の[getUnreadCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#ac2e3266d20b348145d75079020ac50c7)によって取得され、プライベートチャンネルはworkグループによって実現されるので、プライベートチャンネルの未読数は[getConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a619aaff2bb5664e094d2341819b95096)によって取得されます。

```java
// パブリックチャンネル
List<String> conversationIDList = new LinkedList();
conversationIDList.add("GROUP_$GROUPID");
V2TIMManager.getConversationManager().getConversationList(conversationIDList, new V2TIMValueCallback<List<V2TIMConversation>>() {
            @Override
            public void onError(int i, String s) {
                // サーバーに対応するセッション情報の取得に失敗しました
            }

            @Override
            public void onSuccess(V2TIMConversationList List<V2TIMConversation>) {
               // サーバーに対応するセッション情報の取得に成功しました
            }
});
// プライベートチャンネル
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
                @Override
                public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
                    
                }

                @Override
                public void onError(int i, String s) {
                }
});
```

サーバーのカスタム状態機能は、サーバーセッションのカスタムデータを設定することで実現できます。APIは[setConversationCustomData](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ac11ca7227145e3f359f6a3473ed600a5)です。

```java
List<String> conversationIDList = new LinkedList();
String customData = "通話中"
V2TIMManager.getConversationManager().setConversationCustomData(conversationIDList, customData, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
            @Override
            public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
                // グループセッションのカスタムデータの設定に成功しました
            }

            @Override
            public void onError(int i, String s) {
                // グループセッションのカスタムデータの設定に失敗しました
            }
});
```

サーバーセッションの関連データが変更された場合、クライアントはUIの更新を表示しようとする場合、サーバーセッションの変更をリスニングするために、IMはイベントリスニング関数[addConversationListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4)を提供し、以下の情報が変更された場合にこのコールバック関数がトリガされます。

1. サーバーメッセージの追加・削除・変更
2. サーバーメッセージ未読数の変更
3. サーバーのカスタマイズ情報の変更
4. サーバートップ表示
5. サーバーのメッセージ受信設定の変更
6. サーバータグの変更
7. サーバーグループの変更
8. ...

```java
V2TIMConversationListener conversationLister = new V2TIMConversationListener() {
            @Override
            public void onSyncServerStart() {
            }

            @Override
            public void onSyncServerFinish() {
            }

            @Override
            public void onSyncServerFailed() {
            }

            @Override
            public void onNewConversation(List<V2TIMConversation> conversationList) {
            }

            @Override
            public void onConversationChanged(List<V2TIMConversation> conversationList) {
            }
            @Override
            public void onTotalUnreadMessageCountChanged(long totalUnreadCount) {
            }

            @Override
            public void onConversationGroupCreated(String groupName, List<V2TIMConversation> conversationList) {
            }

            @Override
            public void onConversationGroupDeleted(String groupName) {
            }

            @Override
            public void onConversationGroupNameChanged(String oldName, String newName) {
            }

            @Override
            public void onConversationsAddedToGroup(String groupName, List<V2TIMConversation> conversationList) {、
            }

            @Override
            public void onConversationsDeletedFromGroup(String groupName, List<V2TIMConversation> conversationList) {
            }
}
V2TIMManager.getConversationManager().addConversationListener(conversationLister);
```

以上から、getJoinedCommunityList、getConversationListインターフェースおよびaddConversationListenerコールバックにより、サーバーリストを表示するDiscord機能を実現できます。

### チャネル

サーバー内では複数のチャンネルを作成できます。図に示すように、このサーバーの下に4つのチャンネルが作成され、4つのチャンネルが2つのカテゴリに配置されています。 

チャンネルの場合、ユーザーは別のユーザを招待することや、チャンネルの基本的な設定を行うことができます。ユーザーのチャットの多くはチャンネル内で行われるため、チャンネルの能力がDiscordでは最も重要となります。Tencent Cloud IMでは、つまりトピックの能力に相当します。IMコミュニティのコミュニティ内でトピックを新規作成する機能をサポートします。

#### デフォルトチャンネル

Discordはサーバーを作成する際に、デフォルトで4つのチャンネルを作成しますが、Tencent Cloud IMを使用しても、次のようなプロセスで同様な機能を実現できます。

1. [グループ作成後コールバック](https://console.cloud.tencent.com/im/callback-setting)を使用して、サーバーが正常に作成されたことをビジネスサーバー側に通知します。
2. 他のグループに関連する業務に影響を及ぼさないように、ビジネス側が作成したコミュニティを確認します。
3. サーバープロパティに基づいて、[サーバー側でトピックを作成](https://intl.cloud.tencent.com/document/product/1047/49471)します。

サーバー側でトピックを作成するとき主なパラメータは次のとおりです。

```json
{
    "GroupId"："@TGS#_@TGS#cQVLVHIM62CJ"//トピックが属するグループID(必須)
    "TopicId"："@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",//ユーザー定義のトピックID(オプション入力)
    "TopicName"："TestTopic",//トピックの名前(必須)
    "From_Account"："1400187352",//トピックを作成したメンバー
    "CustomString"："This is a custom string",//カスタム文字列
    "FaceUrl"："http://this.is.face.url",//トピックのアバターURL(オプション)
    "Notification"："This is topic Notification",//トピックの掲示（オプション入力）
    "Introduction"："This is topic Introduction"//トピックの概要（オプション入力）
}
```

#### チャネル作成

Discordクライアントでは、ユーザーが次のようなチャンネル分類でチャンネルを作成できます。 

以上のように、チャンネルを作成することはIMのコミュニティでトピックを作成することに相当します。また、作成時には、トピックを分類し、トピックの基本情報を設定することができます。 

関連する機能は、[createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0)を使用して実装されます。

```java
String groupID="サーバーID"
V2TIMTopicInfo info = new V2TIMTopicInfo();
info.setCustomString("{'categray'：'game','type'：'text'}")//チャンネル分類とタイプを設定
// ここでV2TIMTopicInfoの具体的な情報を設定できます
V2TIMManager.getGroupManager().createTopicInCommunity(groupID, info, new V2TIMValueCallback<String>() {
            @Override
            public void onSuccess(String s) {
                // チャンネル作成成功
            }

            @Override
            public void onError(int i, String s) {
                //　チャンネル作成失敗
            }
});
```

チャンネル作成時には、[V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html)のメンバーメソッドを呼び出すことでチャンネルの情報、チャンネル分類およびチャンネルタイプを設定できます。[setCustomString](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#aad0cc8249c21c5ccae385fdfb8ba32ea)で設定されます。 

チャンネルを作成する際には、通常のチャンネルとは異なるプライベートチャンネルであるか否かを設定できます。

1. ユーザーはサーバーに参加した後、プライベートチャンネルに参加しません。
2. プライベートチャンネルへの参加は、サーバー管理者の招待が必要です。

そのため、workグループを使ってプライベートチャンネルの機能を実現しますが、サーバーがどのプライベートチャンネルをバインドしているのかという情報をビジネス側が保存する必要があります。

#### チャンネルタイプ

Discordはチャンネル作成時に、音声チャンネルと文字チャンネルのいずれかを選択できます。文字チャンネルは通常の文字、顔文字、画像のチャットであり、音声チャンネルは音声ビデオチャットです。注意すべきこととして、同じユーザーが同じ時間に1つの音声チャンネル内に入ることです。ユーザーが新しい音声チャンネルに参加するには、現在参加している音声チャンネルを終了する必要があります。 

次のように4つの注意点があります：

1. チャンネルの作成時にチャンネルタイプを設定します。チャンネルタイプの設定方法については、「チャンネルの作成」で説明しました。
2. ユーザーが音声チャンネルに参加する際には、すでに他の音声チャンネルに入っているかどうかを判断しなければなりません。
3. 音声チャンネルはグローバルです。
4. Tencent Cloud IMは、ユーザーが音声チャンネルにいるかどうか、どの音声チャンネルにいるかのAPIを一時的に提供していないため、この部分のデータは事業側で管理されます。

第4の点について、開発者は、Tencent Cloud IMが提供するグループ参加後のコールバックおよびグループ退出後のコールバックを使用して、ユーザーが音声チャンネルにいるかどうかの状態を判断し、その状態をビジネス側ストレージ内に保存するなどのメンテナンスを行います。注意すべきこととして、Tencent Cloud IMのコールバックには遅延が存在する可能性があり、つまり、ユーザーが音声チャンネルを退出した後も、短時間は他の音声チャンネルに参加できない可能性があります。このため、ユーザーが音声チャンネルを参加・退出する状態をリアルタイムで業務サーバー側に報告するように、クライアントに報告する方法でも対応します。

#### ユーザーをチャンネルに招待

ユーザーがチャンネルに入る方法は次の3つがあります：

1. ユーザをサーバーに招待するとき、サーバーに入ったユーザーはすべての公開されたチャンネルに入ります。
2. ユーザーは検索したサーバーに入ります。
3. サーバー管理者からの招待を受けてプライベートチャンネルに入ります。

コミュニティの特性から、ユーザーがワールドチャンネルに入るには、サーバーに参加すればよいことが分かります。

1. グループIDを検索して参加できます。
2. 招待者が入場できます。
3. 特に承認を得る必要なく、申請すれば入れます。



####　チャンネル設定

チャンネルのミュート設定や通知設定は、API[setAllMute](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#a13fbe06ce357215cfd7053954552030b)および[setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e)を使用します。

```java
// チャネル基本情報の設定
V2TIMManager.getGroupManager().setTopicInfo(topicInfo, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        //　設定成功
    }

    @Override
    public void onError(int i, String s) {
        // 設定失敗
    }
});
```

```java
// チャンネルがメッセージを受け取る方法を設定します
String groupID = "topicid"
int opt = 0; 
V2TIMManager.getMessageManager().setGroupReceiveMessageOpt(groupID, opt, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### チャネルメッセージリスト

チャンネルの履歴メッセージレコードは、[getHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a97fe2d6a7bab8f45b758f84df48c0b12)を使用して取得できます。

```java
final V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGroupID("チャネルID");
option.setCount(20);
// その他の設定
V2TIMManager.getMessageManager().getHistoryMessageList(option, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // チャンネル履歴メッセージの取得に成功
    }

    @Override
    public void onError(int code, String desc) {
        // チャンネル履歴メッセージの取得に失敗
    }
});
```

#### チャンネルメッセージ未読数

チャンネル内メッセージ未読数とサーバーメッセージ未読数は異なり、サーバー未読数はセッション情報の中に含まれ、チャンネルの未読数はチャンネルの基本情報の中に含まれます。Tencent Cloud IMのグループコールバック[onTopicInfoChanged]（https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a29285e4e127337e299bd2b695a1afdeb）によって未読数をリアルタイムで取得します。

```java
String groupID = "サーバーID";
List< String > topicIDList= new LinkedList(); // チャネルメッセージリスト
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
    @Override
    public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
        // チャンネルID、チャンネル名、未読数などのチャンネル情報の取得
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### チャンネルメンバーリスト

サーバーに参加しているユーザーはデフォルトですべてのパブリックチャンネルに参加するため、サーバーのグループメンバリストを確認すればよい。機能チャンネルからメンバーリストの取得：

```java
String groupID = "サーバーID";
int filter=0;//グループメンバー、管理者、一般メンバー...
long nextSeq=0;//ページングパラメータ
V2TIMManager.getGroupManager().getGroupMemberList(groupID, filter, nextSeq , new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
    @Override
    public void onError(int i, String s) {
        CommonUtil.returnError(result,i,s);
    }

    @Override
    public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
        
    }
});
```

プライベートチャンネルのグループメンバーリスト取得も[getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be)を呼び出し、プライベートチャンネルのグループIDを渡せばよいです。

### サブチャンネル

サブチャンネルは、チャンネル内のメッセージについてさらに議論を行うグループであり、ユーザーは1つのチャンネル内で議論しているポイントをまとめて閲覧することができ、チャンネル内メッセージリストでは、サブチャンネルの概要を確認することもできます。サブチャネルはTencent Cloud IMでもグループの概念であり、1つのサブチャンネルが1つのグループとなります。

####　サブチャンネルの作成

サブチャンネルの作成は、チャンネル内の1つのメッセージにバインドすることも、Tencent Cloud IMが提供するCreateGroupインターフェースを介して個別に作成することもできますが、以下の点に注意する必要があります。

1.　サーバー内のすべてのメンバーは、デフォルトで新しく作成されたサブチャンネルに配置されます。
2.　サブチャンネルが作成されると、サーバーに参加しているメンバもサブチャンネルに参加します。
3.　その後にサブチャンネルに参加したユーザーはサブチャンネル作成後のチャット履歴を閲覧できます。

以上のように、サブチャンネルを作成した後、グループを作成すると、サーバーのグループメンバーをサブチャンネルに加え、ユーザーがサーバーに参加する場合には、グループに参加した後のコールバックにおいて、サーバーのすべてのサブチャンネルにユーザーを加えます。この2つのステップは、ビジネスサーバー側で実行することをお勧めします。使用するAPIは次のとおりです：

1.　[サーバー内のメンバー](https://intl.cloud.tencent.com/document/product/1047/34948)を問い合せます。
2.　[グループの作成とメンバーの設定](https://intl.cloud.tencent.com/document/product/1047/34895)。
3.　[ユーザーをグループに招待する](https://intl.cloud.tencent.com/document/product/1047/34921)。

サーバー側のコールバックは[グループ参加後のコールバック](https://intl.cloud.tencent.com/document/product/1047/34372)。

####　サブチャンネルの数

チャンネルリストでは、チャンネルの下にあるサブチャンネルのリストを取得できますので、サブチャンネルとサーバーの多対1の関係をバインドする必要があります。サブチャンネルに履歴メッセージが存在し、サブチャンネルとメッセージの1対1の関係もバインドする場合、Tencent Cloud IMは上記の関係をバインドする能力を現時点で提供していないため、ビジネス側が別途で対応しなければなりません。サービスが提供するHTTPインターフェースを介して、サブチャンネルの数とサブチャンネルリストを取得します。オンラインメッセージを送信して、サブチャンネルリストをリアルタイムでリフレッシュします。

####　サブチャンネルの概要

メッセージのサブチャンネルを作成すると、そのサブチャンネルのメッセージ概要がメッセージリストに表示されます。

1.　サブチャンネルにあるメッセージの数。
2.　このサブチャンネル内のlastMessageに関する情報。
3.　情報はリアルタイムでメッセージリストに表示される必要があります。

サブチャンネルのメッセージ概要能力を実現するには、グループ内メッセージ送信後のコールバック、およびメッセージ編集の能力を組み合わせる必要があります。ユーザーがサブチャンネルでメッセージを送信した後、IMサービスはメッセージ送信後のコールバックをトリガし、関連情報をビジネス側に同期させ、ビジネス側でメッセージカウントを行い、lastMessage関連情報を処理し、メッセージ編集APIを介してメッセージに保存します。

### メッセージ関連

####　メッセージフィードバック

メッセージフィードバックは、次の図に示すように、ユーザーがメッセージを拡張するために使用されます。 

すべてのメッセージのタイプは編集およびフィードバックが可能であり、コミュニティをサポートする必要があるため、データをcloudCustomDataフィールドに保存することをお勧めします。詳細なデータストレージフォーマットは次のとおりです：

```json
{
  "reaction": {
    "simle":["user1","user2"]
  }
}
```

```java
V2TIMManager.getMessageManager().modifyMessage(modifiedMessage, new V2TIMCompleteCallback<V2TIMMessage>() {
    @Override
    public void onComplete(int i, String s, V2TIMMessage v2TIMMessage) {
        //　メッセージの変更完了
    }
});
```

####　メッセージ編集

メッセージ編集は、メッセージフィードバックの原理と同様に、設定されたカスタムデータだけが異なります。同様に、すべてのメッセージにメッセージ編集を適用するために、cloudCustomDataフィールドを次の形式で編集することをお勧めします。

```json
{
  "isEdited": true
}
```

```java
V2TIMManager.getMessageManager().modifyMessage(modifiedMessage, new V2TIMCompleteCallback<V2TIMMessage>() {
    @Override
    public void onComplete(int i, String s, V2TIMMessage v2TIMMessage) {
        //　メッセージ編集完了
    }
});
```

####　メッセージのタグ付け  

メッセージのタグ付けとは、ユーザーがグループチャットでメッセージにタグ付けを行い、他のユーザーがタグ付けられたメッセージを確認できるようにすることです。コミュニティはグループ属性をサポートしていないので、ここではカスタムメッセージを使用してメッセージタグ付け機能を実装します。

グループのカスタムメッセージを使用するには、[Tencent Cloud IM Console](https://console.cloud.tencent.com/im/qun-setting)を設定する必要があります。

次のように設定します：

```java
V2TIMGroupInfo info = new V2TIMGroupInfo();
info.setCustomInfo("pin data");
V2TIMManager.getGroupManager().setGroupInfo(info, new V2TIMCallback() {
    @Override
    public void onError(int i, String s) {
        // 設定失敗
    }

    @Override
    public void onSuccess() {
        //　設定成功
    }
});
```

設定されると、グループメンバーは[onMemberInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a4ac777faad07e32408ae7ef5e2e3fc86)イベントを受信し、オンラインにいないユーザーは、タグ付けられたメッセージの内容をグループ情報から取得できます。

```java
List< String > groupIDList = new LinkedList();
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfoResults) {
        
    }
});
```

現時点では、カスタムフィールドはサーバー上にのみ設定でき、チャンネル上には設定できないことに注意してください。

####　入力中のステータス

友達が入力している間、他のユーザー側は入力中の状態を見ることができます。前述のように、Tencent Cloud IMが提供するオンラインメッセージを使用してこのメッセージを表示します。

1.　オンラインユーザーのみが受け取ることができます。
2.　メッセージローミングは保存されません。

また、パフォーマンスを最適化するために、次のような最適化を行うこともできます。

-　20s以内にメッセージを送信したユーザー双方が入力中状態メッセージの送信をトリガします。
-　同じテキストメッセージについて、複数回のオンラインメッセージ送信がトリガーされません。

###　プライベートメッセージ

プライベートメッセージとは、Discordユーザーとユーザーとの間で、友達関係があるかどうかに関係なくメッセージを送信することができます。

-　友達関係がない場合、メッセージを送信するにはユーザーIDを知るほか、Tencent CloudのIMコンソールで[メッセージ送信検出](https://console.cloud.tencent.com/im/login-message)リレーションシップチェーンのオプションをオフにする必要があります。オフにしないと、メッセージの送信に失敗します。
-　ユーザーは、最初に[addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208)インターフェースを使用して友達を追加し、[getFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624)を使用して自分の友達リストを取得することもできます。

関連コードは次のとおりです：

```java
// 友達を追加
V2TIMManager.getFriendshipManager().addFriend(info, new V2TIMValueCallback<V2TIMFriendOperationResult>() {
            @Override
            public void onError(int i, String s) {
                // 友達追加失敗
            }

            @Override
            public void onSuccess(V2TIMFriendOperationResult v2TIMFriendOperationResult) {
               // 友達追加成功
            }
});
```

```java
// 友達リストを取得する
V2TIMManager.getFriendshipManager().getFriendList(new V2TIMValueCallback<List<V2TIMFriendInfo>>() {
            @Override
            public void onError(int i, String s) {
               // 友達リスト取得失敗
            }

            @Override
            public void onSuccess(List<V2TIMFriendInfo> v2TIMFriendInfos) {
               // 友達リストを正常に取得する
            }
});
```

### 個人センター

#### オンラインステータス 
Discordユーザーパネルのプレゼンス状態機能は、Tencent Cloud IMが提供するプレゼンス状態APIによって実現されます。

-　[setSelfStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7520045679f1493c890f2b3b5eee7b84)を使用して、ユーザー独自のオンライン/オフライン状態を設定します。ユーザー独自のオンライン/オフライン状態はIMによって設定され、開発者は変更できません。
-　[getUserStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2428c7f87859dd85bed1730ad8d3b92a)を使用して友達のプレゼンス状態を取得します。
-　[onUserStatusChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94251d1971d7b6692b3278ed0d42b73e)を使用して、友達のプレゼンス状態の変更を受信します。

関連コードは次のとおりです：

```java
//　個人のプレゼンス状態の設定
V2TIMUserStatus customStatus = new V2TIMUserStatus();
V2TIMManager.getInstance().setSelfStatus(customStatus, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

```java
//　友達のプレゼンス状態を取得
List<String> userIDList = new LinkerList();
V2TIMManager.getInstance().getUserStatus(userIDList, new V2TIMValueCallback<List<V2TIMUserStatus>>() {
    @Override
    public void onSuccess(List<V2TIMUserStatus> v2TIMUserStatuses) {
       
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### 個人情報関連

個人情報関連の機能は、Tencent Cloud IMが提供する情報リレーションシップチェーン関連のAPIを介して実装できます。

-　個人プロファイル[getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e)を取得します。
-　個人プロファイル[setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a)を設定します。

```java
// 個人情報を設定する
final V2TIMUserFullInfo userFullInfo = new V2TIMUserFullInfo();
V2TIMManager.getInstance().setSelfInfo(userFullInfo, new V2TIMCallback() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess() {
        
    }
});
```

```java
// ユーザープロファイルの取得
List<String> userIDList = new LinkedList();
V2TIMManager.getInstance().getUsersInfo(userIDList, new V2TIMValueCallback<List<V2TIMUserFullInfo>>() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess(List<V2TIMUserFullInfo> v2TIMUserFullInfos) {
        
    }
});
```

### その他

####　検索機能

Discordの検索機能は次のとおりです： 

Tencent Cloud IMは、次のような豊富な検索機能を提供します。

- メッセージの検索[searchLocalMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9364c8a0c6a0899b17c0a479b8ca848a)。
-　グループの検査[searchGroups](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023)。
-　グループメンバーの検索[searchGroupMembers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a)。
-　友達の検索[searchFriends](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3e657c9ec5d68a4c423a64d71f5f9c6e)。

API利用の詳細については、公式ドキュメント[検索について](https://intl.cloud.tencent.com/document/product/1047/48134)をご参照ください。

####　オフラインプッシュ機能

ユーザーがオフラインになった場合、Tencent Cloud IMのオンラインメッセージはユーザーに届かません。これは端末機器メーカーが提供するオフラインプッシュ機能が必要で、Tencent Cloud IMはオフラインプッシュを導入するのにも非常に便利です。詳細については[オフラインプッシュ](https://intl.cloud.tencent.com/document/product/1047/39156)をご参照ください。

####　センシティブワード検証

情報を送信したり、プロファイルを設定したりする際には、内容をフィルタリングする必要があります。Tencent Cloud　IMもこうした解決策を提供し、ユーザーが正しくIMを利用できるよう支援しています。
