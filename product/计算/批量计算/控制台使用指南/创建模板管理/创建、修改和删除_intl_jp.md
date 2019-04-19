## タスクテンプレートの作成

タスクテンプレートの説明については、[名詞の説明]()の「タスクテンプレート」を参照してください。[Batchコンソール]()でタスクテンプレートを作成できます。具体的な手順は次のとおりです。
1. [Batchコンソール]()にログインします。まだBatchサービスを有効化していない場合は、Batchコンソールのホームページに関連する指示を参照してください。

2. 左側のナビゲーションバーの「タスクテンプレート」オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。
![](https://main.qcloudimg.com/raw/9040a7e885e21aa3fe99e7060e76c15e.png)

3. 基本情報を構成します。
   - リソース構成：「CVM詳細構成」オプションをクリックして、さらに選択することができます。関連する構成説明については、[CVM製品ドキュメント](https://intl.cloud.tencent.com/document/product/213)を参照してください。
   - リソース数：タスクを同時に実行するためのリソース数を決定します。関連する説明については、[名詞の説明](https://intl.cloud.tencent.com/document/product/599/10396)の「タスクインスタンス」を参照してください。
   - イメージ：関連する説明については、[名詞の説明](https://intl.cloud.tencent.com/document/product/599/10396)の「イメージ」を参照してください。
   ![](https://main.qcloudimg.com/raw/0448f705c865b179587eff6e60d5459b.png)

4. プログラム構成情報を設定します。
   - 実行方式：「Package」を選択した場合は、「パッケージアドレス」を入力する必要があります。「パッケージアドレス」は[COS](https://intl.cloud.tencent.com/document/product/436)に保存されています。
   - パッケージアドレス/Stdoutログ/Stderrログ：固定フォーマットが必要です。[COS、CFSパス記入]()を参照してください。
![](https://main.qcloudimg.com/raw/626c2e80f1ea78d315ef473a17c843e2.png)

5. ストレージマッピングを構成します。
   - 入力パスマッピング：LINUXシステムでは、[COS](https://intl.cloud.tencent.com/document/product/436)および[CFS](https://intl.cloud.tencent.com/document/product/582)をサポートします。Windowsシステムでは、[CFS](https://intl.cloud.tencent.com/document/product/582)をサポートしています。COSとCFSのフォーマット要求については、[COS、CFSパス記入]()を参照してください。同時に、異なる操作システムの場合は、ローカルパスのフォーマットの違いに注意してください。
   - 出力パスマッピング：[COS](https://intl.cloud.tencent.com/document/product/436)をサポートします。COSのフォーマットについては[COS、CFSパス記入]()を参照してください。
   ![](https://main.qcloudimg.com/raw/8b994c5d4ffa0d2155a0e06a9a91f377.png)

6. タスクテンプレートのJSONファイルを確認したら、【保存】ボタンをクリックしてタスクテンプレートの作成を完了します。
![](https://main.qcloudimg.com/raw/824b15b3dcff490bf8486098d243fe02.png)

## タスクテンプレートの削除
タスクテンプレートを使用する必要がなくなった場合は、タスクテンプレートリストから削除することができます。
![](https://main.qcloudimg.com/raw/0918678402a90b8bc19c685bb8be6bb8.png)

## タスクテンプレートの変更
既存のタスクテンプレートを編集する必要がある場合は、タスクテンプレートIDをクリックしてタスクテンプレート構成ページに入り、アイテムごとに編集できます。
![](https://main.qcloudimg.com/raw/c325e5c25ee1ab8305be0f1d22ecfa53.png)

