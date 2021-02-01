このドキュメントでは、データベース/テーブルの作成、データベース管理、インスタンスの監視、インスタンスセッション、テーブルデータのビジュアル編集などの新しいバージョンのDMCコンソールの機能について説明します。
>? データベースのリアルタイム監視やInnoDBロック待機管理などの機能を使用する場合は、DMCナビゲーションバーの右上隅にある【 Back to old version】をクリックして、古いバージョンのDMCコンソールにアクセスできます。

## データベース/テーブルの作成
1. [DMCコンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Create】>【Create Database 】>【Create Database 】または【Create】>【Create Table】を選択します。
![](https://main.qcloudimg.com/raw/2e7d5ffdeb7b527d4dde3246b24dd04b.png)
2.表示されるダイアログボックスで、新しいデータベース/テーブルを設定し、【Submit】をクリックします。
>?文字セット、照合順序の詳細については、[MySQLの公式ドキュメント](https://dev.mysql.com/doc/)をご参照ください。
>
 - データベースの作成
![](https://main.qcloudimg.com/raw/43a11a0dcd4da77bc45a6d686cc86617.png)
 - テーブルの作成
![](https://main.qcloudimg.com/raw/2cb0348e7929c14dce28928e32a830c0.png)

## データベース管理
[DMCコンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Database Management 】を選択し、データベース管理ページに入ります。ユーザーはデータベースを作成、編集、削除できます。
![](https://main.qcloudimg.com/raw/48e93b028657d9b10f69c1a41eda1f19.png)

## インスタンスセッション
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【instance session】を選択して、インスタンスセッションページに入ります。ユーザーは、現在のデータベース内のすべてのインスタンスのセッションの詳細を表示し、セッションの概要、ユーザー、アクセスソース、およびデータベースの4つの異なるディメンションから情報を表示できます。
DMCを使用すると、セッションを強制終了して、セッション管理を容易にすることができます。
![](https://main.qcloudimg.com/raw/26f08e7b47be3ba94842372d40f36961.png)

## SQLウィンドウ
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【SQL Window】をクリックするか、左側のナビゲーションバーの[操作]メニューで【SQL Operation 】をクリックして、SQLウィンドウページに入ります。 SQLウィンドウは、次の機能をサポートしています。
- SQLコマンドの実行および結果の表示
- SQLステートメント形式の最適化
- SQLコマンドの実行プランの表示
- 一般的に使用されるSQLステートメントの保存
- SQLテンプレートの使用
- SQLステートメントの実行結果のエクスポート
![](https://main.qcloudimg.com/raw/39144de0b6effe7ad50a164a3d1d3273.png)

## データ管理
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Data Management】>【Data Importing】または【Data Exporting 】を選択すると、データベースにデータをインポートしたり、データベースからデータをエクスポートしたりできます。
![](https://main.qcloudimg.com/raw/f499d283976127a5a678ed160d5a6d22.png)

## テーブルデータのビジュアル編集
新しいバージョンの DMC for MySQLは、データの挿入、削除、および更新をサポートしています。ユーザーは、左側のナビゲーションバーの[table]をクリックして、テーブルデータを一括で追加、削除、および変更できます。変更が完了したら、[Quick Operation] ペインで【OK】をクリックして、変更されたSQLステートメントをプレビューします。確認後に一括変更が実行されます。
![](https://main.qcloudimg.com/raw/4488c0191fbbd19b221af38a0daffc76.png)
