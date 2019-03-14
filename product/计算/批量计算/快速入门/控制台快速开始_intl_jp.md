## クイックスタート
本文では、Batchコンソールを使用してジョブを提出する方法について説明します。具体的な操作手順は次のとおりです。
### 準備
[COS](https://intl.cloud.tencent.com/document/product/436)バケットを準備します。まだバケットを作成していない場合は、[バケットの作成](https://intl.cloud.tencent.com/document/product/436/6232)を参照して作成を完了してください。

### [コンソール]()ログイン
まだBatchサービスを有効化していない場合は、Batchコンソールのホームページに関連する指示を参照してください。

### タスクテンプレートの作成

1. 左側のナビゲーションバーの「タスクテンプレート」オプションをクリックして、「広州」などの目標地域を選択します。【新規作成】ボタンをクリックします。

2. 基本情報を構成します。
  * 名前：helloなど
  * 説明：hello demoなど
  *　リソース構成：デフォルト値
  * リソース数：1台など
  * タイムアウト時間：デフォルト
  * 再試行回数：デフォルト
  * イメージ：img-m4q71qnf
![](https://mc.qcloudimg.com/static/img/d12041618aeba32ecd52f61d84656e40/image.jpg)

3. プログラム情報を構成します。
  * 実行方式：Local
  * Stdoutログ：フォーマットは[COS、CFSパス記入](https://cloud.tencent.com/document/product/599/13996)を参照してください。
  * Stderrログ：Stdoutログと同じ
  * コマンドライン：echo 'hello, world'
![](https://mc.qcloudimg.com/static/img/374f5532c7ee7af1211e91b2ff20ddd3/image.jpg)

4.　ストレージマッピングを構成し、完了したら【次へ】ボタンをクリックします。
   ![](https://mc.qcloudimg.com/static/img/4fa9b5f5516a4ca3e0c04dd6e85481c7/image.jpg)

5.　タスクのJSONファイルをプレビューして正しいことを確認し、【保存】ボタンをクリックします。
  ![](https://mc.qcloudimg.com/static/img/7a462bf1530b0d867473fc95e316943e/image.jpg)

6.　タスクテンプレートを確認します。
  ![](https://mc.qcloudimg.com/static/img/2138233d9271bc270abe0a2ba7deebdc/image.jpg)

### ジョブ提出
1. 左側のナビゲーションバーの「ジョブ」オプションをクリックして、「広州」などの目標地域を選択します。【新規作成】ボタンをクリックします。

2. ジョブの基本情報を構成します。
  * ジョブ名：helloなど
  * 優先度：デフォルト
  * 説明：hello jobなど
  ![](https://mc.qcloudimg.com/static/img/adfad5bef466330a4f5583a84531f4af/image.jpg)

3. 「タスクフロー」の左側にある「hello」タスクを選択し、マウスを動かしてタスクを右側のキャンバスに配置します。
  ![](https://mc.qcloudimg.com/static/img/f853b543e328755b0f15b6f62e5b2b8e/image.jpg)

4. 「タスクフロー」の右側にある「タスク詳細」を開き、構成が正しいことを確認したら、［完了］ボタンをクリックします。
![](https://mc.qcloudimg.com/static/img/7e8faba3818f7ff2ada687ed7602be2e/image.jpg)

5. 結果を照合します。ジョブリストページでジョブの実行ステータスを確認できます。
  ![](https://mc.qcloudimg.com/static/img/6513237516f727b80f3a095ed18f5b77/image.jpg)
 - ジョブIDをクリックすると、「タスク実行ステータス」の下で各タスクインスタンスの実行ステータスを確認することができます
 - ［ログの照合］ボタンをクリックすると、タスクインスタンスの標準出力と標準エラーを確認することができます。

  ![](https://mc.qcloudimg.com/static/img/3e743ad83c975d57b7ad9f56d78b8933/image.jpg)

## 次に何ができますか？

これは最も簡単な例で、シングルタスクジョブであり、リモートストレージマッピング機能を使用するのではなく、ユーザーに最も基本的な機能を示すだけです。コンソールの使用ガイドに従って、Batchのより高いレベルの機能をテストし続けることができます。
- **豊富なCVM構成**：Batchは、豊富なCVM構成項目を提供して、ビジネスシナリオに基づいてCVM構成をカスタマイズできます。
- **リモートコードパッケージの実行**：Batchは**カスタムイメージ + リモートコードパッケージ + コマンドライン**の方式を提供し、技術的にあらゆる方面でユーザーのビジネスニーズに対応します。
- **リモートストレージマッピング**：Batchはストレージアクセスを最適化し、リモートストレージサービスへのアクセスをローカルファイルシステムの操作に単純化します。

