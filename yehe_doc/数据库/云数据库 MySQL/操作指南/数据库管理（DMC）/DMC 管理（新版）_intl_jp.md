このドキュメントでは、データベース/テーブルの作成、データベース管理、インスタンスの監視、インスタンスセッション、テーブルデータのビジュアル編集などの新しいバージョンのDMCコンソールの機能について説明します。
>? データベースのリアルタイム監視やInnoDBロック待機管理などの機能を使用する場合は、DMCナビゲーションバーの右上隅にある【 Back to old version】をクリックして、古いバージョンのDMCコンソールにアクセスできます。

## データベース/テーブルの作成
1. [DMCコンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Create】>【Create Database 】>【Create Database 】または【Create】>【Create Table】を選択します。
![](https://main.qcloudimg.com/raw/4b1c803307c0c64d96ff6b8fdf43d3dd.png)
2.表示されるダイアログボックスで、新しいデータベース/テーブルを設定し、【Submit】をクリックします。
>?文字セット、照合順序の詳細については、[MySQLの公式ドキュメント](https://dev.mysql.com/doc/)をご参照ください。
>
 - データベースの作成
![](https://main.qcloudimg.com/raw/392a9c91adf523e57deb300f0be7e86d.png)
 - テーブルの作成
![](https://main.qcloudimg.com/raw/0d4806266e021e7864c0aa605781929c.png)

## データベース管理
[DMCコンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Database Management 】を選択し、データベース管理ページに入ります。ユーザーはデータベースを作成、編集、削除できます。
![](https://main.qcloudimg.com/raw/85b4d1def1c7eadaf415d9944ff3101c.png)

## インスタンスセッション
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【instance session】を選択して、インスタンスセッションページに入ります。ユーザーは、現在のデータベース内のすべてのインスタンスのセッションの詳細を表示し、セッションの概要、ユーザー、アクセスソース、およびデータベースの4つの異なるディメンションから情報を表示できます。
DMCを使用すると、セッションを強制終了して、セッション管理を容易にすることができます。
![](https://main.qcloudimg.com/raw/4218f038cb177548047f0042f4986351.png)

## SQLウィンドウ
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【SQL Window】をクリックするか、左側のナビゲーションバーの[操作]メニューで【SQL Operation 】をクリックして、SQLウィンドウページに入ります。 SQLウィンドウは、次の機能をサポートしています。
- SQLコマンドの実行および結果の表示
- SQLステートメント形式の最適化
- SQLコマンドの実行プランの表示
- 一般的に使用されるSQLステートメントの保存
- SQLテンプレートの使用
- SQLステートメントの実行結果のエクスポート
![](https://main.qcloudimg.com/raw/cf0c070dc6ae01c6d9c8795ce0934fb6.png)

## データ管理
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Data Management】>【Data Importing】または【Data Exporting 】を選択すると、データベースにデータをインポートしたり、データベースからデータをエクスポートしたりできます。
![](https://main.qcloudimg.com/raw/5c58a3bbfe40ac943bd08a726427b7fa.png)

## テーブルデータのビジュアル編集
新しいバージョンの DMC for MySQLは、データの挿入、削除、および更新をサポートしています。ユーザーは、左側のナビゲーションバーの[table]をクリックして、テーブルデータを一括で追加、削除、および変更できます。変更が完了したら、[Quick Operation] ペインで【OK】をクリックして、変更されたSQLステートメントをプレビューします。確認後に一括変更が実行されます。
