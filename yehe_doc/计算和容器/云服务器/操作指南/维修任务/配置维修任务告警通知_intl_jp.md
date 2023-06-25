## 概要

CVM インスタンスのメンテナンスタスクにアラームを設定できます。障害発生時に、電子メール、ショートメッセージ、電話などのチャネルを介して即座に措置を講じるよう通知します。このドキュメントでは、[EventBridge](https://intl.cloud.tencent.com/document/product/1108/42267) を使用して、EventBridge コンソールで CVM インスタンスのアラーム通知を設定する方法について説明します。

## 操作手順
1. [EventBridgeコンソール](https://console.cloud.tencent.com/eb)にログインし、 [EventBridgeのアクティブ化](https://intl.cloud.tencent.com/document/product/1108/42272) の指示に従ってサービスをアクティブ化します。
2.左側のサイドバーで **[ Event Rule](https://console.cloud.tencent.com/eb/rule)** を選択し、「Event Rule」ページの上部でターゲットリージョンとイベントバスを選択して、**Create Event Rule**をクリックします。
3.「Create Event Rule」ページで、次の操作を実行します。
    1.  下図に示すように、「Basic Information」で、**ルール名**を入力します。
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/zHwA899_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102346.png)
    2. 下図に示すように、「Event Pattern」で、次の情報を参照して「イベントマッチング」パラメータを設定し、その他のパラメータを必要に応じて設定します。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/bQp2060_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102608.png)
       - **Tencent Cloud service**：ドロップダウンリストから**CVM**を選択します。
       - **Event Type**：必要に応じて、ドロップダウンリストからオプションを選択します。
   3. **Next**をクリックします。
   4. 「Delivery target」で、必要に応じて「Trigger method 」ドロップダウン リストからオプションを選択します。
      - 「トリガーモード」は**Cloud Log Service（CLS）**を選択する場合、 [CLSログターゲット](https://intl.cloud.tencent.com/document/product/1108/46992) を参照して設定を行うことができます。
      - 「トリガーモード」は**Notification message**を選択する場合、 [メッセージプッシュターゲット](https://intl.cloud.tencent.com/document/product/1108/46779) を参照して設定を行うことができます。
4. **Complete**をクリックし、設定を完了します。
