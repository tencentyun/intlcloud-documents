この文書では、接続プール機能の有効化・無効化について説明します。

## 前提条件
［データベースプロキシのアクティブ化］(https://www.tencentcloud.com/document/product/236/42052)が完了していること。

## 接続プール機能の有効化
1. [MySQL コンソール](https://console.cloud.tencent.com/cdb)にログインし、上側でリージョンを選択して、対象インスタンスIDをクリックすると、インスタンス管理画面が表示されます。
2. インスタンス管理画面で、**データベースプロキシ** > **アクセスポリシー**を選択し、ターゲットアクセスポリシーを見つけて**設定**をクリックします。
>?**データベースプロキシ** > **概要*** > **接続アドレス**の下でターゲットアクセスアドレスを見つけ、**操作**列の**設定を調整**をクリックすることもできます。
>
3. 設定の調整画面で、接続プールの状態の横にあるボタンをオンにすると、セッションレベルの接続プール機能がデフォルトで有効になります。その後、**確定**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/ae2436546dfc7c8f0f8b6c6d6f154482.png)

## 接続プールの無効化
1. [MySQL コンソール](https://console.cloud.tencent.com/cdb)にログインし、上側でリージョンを選択して、対象インスタンスIDをクリックすると、インスタンス管理画面が表示されます。
2. インスタンス管理画面で、**データベースプロキシ** > **アクセスポリシー**を選択し、ターゲットアクセスポリシーを見つけて**設定**をクリックします。
>?**データベースプロキシ** > **概要*** > **接続アドレス**の下でターゲットアクセスアドレスを見つけ、**操作**列の**設定を調整**をクリックすることもできます。
>
3. 設定の調整画面で、接続プールの状態のボタンをオフにして、**確定**をクリックします。
