このドキュメントでは、データベース/テーブルの作成、インスタンスセッション管理、データベースのリアルタイム監視、InnoDBロック待機管理などの古いバージョンのDMCコンソールの機能について説明します。
>?
>- SQLウィンドウやテーブルデータのビジュアル編集などの機能を使用する場合は、画面上にあるナビゲーションバーの【新しいバージョンに移動】をクリックして、新しいバージョンのDMCコンソールにアクセスできます。
>- 現在、TencentDB for MySQL v8.0は、InnoDBロック待機管理およびphpMyAdmin機能をサポートしていません。

## データベース/テーブルの作成
1. [DMCコンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Create】>【Create Database 】>【Add Database】または【Create】>【Create Table】を選択します。
![](https://main.qcloudimg.com/raw/655d55fd3304455269a547f90c96c91e.png)
2. 表示されるダイアログボックスで、新しいデータベース/テーブルを設定し、【Submit】をクリックします。
>?文字セット、照合順序の詳細については、[MySQLの公式ドキュメント](https://dev.mysql.com/doc/)をご参照ください。
>
 - データベースの作成
![](https://main.qcloudimg.com/raw/258605b4ac20f2136672bab0381e0f3f.png)
 - テーブルの作成
![](https://main.qcloudimg.com/raw/d2aec4106f019ff9d088be7c27737330.png)

## インスタンスセッション管理
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【instance session】を選択して、インスタンスセッション管理ページに入ります。ユーザーは、現在のデータベース内のすべてのインスタンスのセッションの詳細を表示し、セッションの概要、ユーザー、アクセスソース、およびデータベースの4つの異なるディメンションから情報を表示できます。
DMCを使用すると、セッションを強制終了して、セッション管理を容易にすることができます。
![](https://main.qcloudimg.com/raw/dd87caaefb78386484ebb58bfdbdc6e4.png)

## データベースのリアルタイム監視
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Instance Monitoring】を選択して、インスタンスの監視ページに入ります。データベースのリアルタイム監視機能は4秒ごとにデータを更新し、次の監視データを提供します。

MySQL ステータス情報|  InnoDB行操作 |   スレッド   |ネットワーク
---|---|---|---
[qps]は検索システムやデータベースなどが1秒間に外部からの問い合わせを処理する件数を示します| [read]はInnoDBストレージエンジンテーブルから読み込まれた行数を示します | [running]はアクティブな接続数、つまりSQLを実行している接続の数を示します |[in(KB)] はインスタンスのインバウンドネットワークトラフィックを示します
[tps] は1秒あたりに処理されたトランザクション数を示します | [insert] はInnoDBストレージエンジンテーブルに書き込まれたレコードの数を示します| [connected] はインスタンスに接続されているアイドル状態の接続、つまりSQLを実行していない接続の数を示します| [out(KB)] はインスタンスのアウトバウンドネットワークトラフィックを示します
[ins] は1秒あたりに実行されたinsert ステートメントの数を示します | [update] はInnoDBストレージエンジンテーブルで更新された行数を示します |-  |- |
[upd] は1秒あたりに実行されたupdateステートメントの数を示します | [delete] はInnoDBストレージエンジンテーブルから削除された行数を示します|- |- |
[del] は1秒あたりに実行されたdelete ステートメントの数を示します |- |- |- |
[sel] は1秒あたりに実行されたselectステートメントの数を示します | -|- | - |
[hit%] はキャッシュヒット率を示します。主にinnodb_buffer_poolのヒット率を指します | - | - |- |

## InnoDBロック待機管理
>?TencentDB for MySQL v8.0は InnoDB ロック待機管理機能をサポートしていません。
>
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【InnoDB lock wait】を選択して、InnoDBロック待機の管理ページに入ります。ユーザーは、ロックの保持とロックの待機の詳細を表示したり、セッションを削除したりできます。次の図に示すように：
![](https://main.qcloudimg.com/raw/ea4ebed0ba1a6e8b804af1554c09d3e6.png)
![](https://main.qcloudimg.com/raw/746daa00522aa773c96c1248570a4537.png)

## 組み込みツールphpMyAdmin
>?TencentDB for MySQL v8.0はphpMyAdmin機能をサポートしていません。
>
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【Go to PMA】を選択して、組み込みのphpMyAdminに移動してデータベースを管理します。phpMyAdminは、次のようなほとんどのMySQL機能をサポートしています。
- データベース、テーブル、ビュー、フィールド、およびインデックスを表示および削除します。
- データベース、テーブル、フィールド、およびインデックスを作成、複製、削除、名前変更、および変更します。
 - データベースとテーブルの詳細な操作を作成します。
 - データベースとテーブルの詳細な操作を削除します。
- サーバー、データベース、テーブル、および関連するサーバー構成を維持します。
- SQLステートメントを実行および編集します。
- ストアドプロシージャとトリガーを管理します。

## DBbrainインテリジェント最適化
[DMC コンソール](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)にログインし、上部のナビゲーションバーで【DBbrain Intelligent Optimization】をクリックして、DBbrainコンソールに移動します。 

