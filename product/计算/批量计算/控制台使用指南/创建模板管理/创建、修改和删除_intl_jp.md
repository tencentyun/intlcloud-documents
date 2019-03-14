## タスクテンプレートの作成

タスクテンプレートの説明については、[名詞の説明]()の「タスクテンプレート」を参照してください。[Batchコンソール]()でタスクテンプレートを作成できます。具体的な手順は次のとおりです。
1. [Batchコンソール]()にログインします。まだBatchサービスを有効化していない場合は、Batchコンソールのホームページに関連する指示を参照してください。

2. 左側のナビゲーションバーの「タスクテンプレート」オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。
![](https://mc.qcloudimg.com/static/img/b6d89f6a4b4e0c8cc0469606948b8e41/image.jpg)

3. 基本情報を構成します。
   - リソース構成：「CVM詳細構成」オプションをクリックして、さらに選択することができます。関連する構成説明については、[CVM製品ドキュメント](https://intl.cloud.tencent.com/document/product/213)を参照してください。
   - リソース数：タスクを同時に実行するためのリソース数を決定します。関連する説明については、[名詞の説明](https://intl.cloud.tencent.com/document/product/599/10396)の「タスクインスタンス」を参照してください。
   - イメージ：関連する説明については、[名詞の説明](https://intl.cloud.tencent.com/document/product/599/10396)の「イメージ」を参照してください。
   ![](https://mc.qcloudimg.com/static/img/2e4c9a7879539ae70b907f669e4a8b78/image.jpg)

4. プログラム構成情報を設定します。
   - 実行方式：「Package」を選択した場合は、「パッケージアドレス」を入力する必要があります。「パッケージアドレス」は[COS](https://intl.cloud.tencent.com/document/product/436)に保存されています。
   - パッケージアドレス/Stdoutログ/Stderrログ：固定フォーマットが必要です。[COS、CFSパス記入]()を参照してください。
![](https://mc.qcloudimg.com/static/img/ed418b2351814d567c0beceb3183ec9d/image.jpg)

5. ストレージマッピングを構成します。
   - 入力パスマッピング：LINUXシステムでは、[COS](https://intl.cloud.tencent.com/document/product/436)および[CFS](https://intl.cloud.tencent.com/document/product/582)をサポートします。Windowsシステムでは、[CFS](https://intl.cloud.tencent.com/document/product/582)をサポートしています。COSとCFSのフォーマット要求については、[COS、CFSパス記入]()を参照してください。同時に、異なる操作システムの場合は、ローカルパスのフォーマットの違いに注意してください。
   - 出力パスマッピング：[COS](https://intl.cloud.tencent.com/document/product/436)をサポートします。COSのフォーマットについては[COS、CFSパス記入]()を参照してください。
   ![](https://mc.qcloudimg.com/static/img/b86945c2ee04dcb89d1ce9aa2a62955c/image.jpg)

6. タスクテンプレートのJSONファイルを確認したら、【保存】ボタンをクリックしてタスクテンプレートの作成を完了します。
![](https://mc.qcloudimg.com/static/img/779bfc1f07af787612d2fb1db5ce70d1/image.jpg)

## タスクテンプレートの削除
タスクテンプレートを使用する必要がなくなった場合は、タスクテンプレートリストから削除することができます。
![](https://mc.qcloudimg.com/static/img/9d207da685ef89b75a93818851f5050f/image.jpg)

## タスクテンプレートの変更
既存のタスクテンプレートを編集する必要がある場合は、タスクテンプレートIDをクリックしてタスクテンプレート構成ページに入り、アイテムごとに編集できます。
![](https://mc.qcloudimg.com/static/img/bab3f74591f80db4022716f897d57893/image.jpg)

