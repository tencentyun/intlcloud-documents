## 概要

Cloud Object Storage（COS）のメディア処理の既存ビジネスまたは機能がニーズを満たすことができない場合は、Serverless Cloud Function（SCF）を使用し、関数処理機能をカスタマイズすることで、コアとなるコードロジックを作成し、ビジネスニーズを柔軟に実現しながら、研究開発コストを低減させることができます。詳細は [SCFドキュメント](https://intl.cloud.tencent.com/document/product/583/9199)をご参照ください。

>?
> - 現在、関数のカスタマイズ処理機能は、ワークフローでの開始のみをサポートしています。
> - SCFでカスタマイズ処理を使用すると、対応する機能の料金が発生し、SCFサービスにより課金されます。課金説明の詳細は、 [SCF課金ドキュメント](https://intl.cloud.tencent.com/document/product/583/17299)をご参照ください。
> 

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリストに進みます。
3. 処理したいバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで、**データワークフロー>ワークフロー**をクリックし、ワークフロー管理ページに進みます。
5. **ワークフローの作成**をクリックし、ワークフロー作成ページで、「関数のカスタマイズ」ノードを追加します。

設定項目の説明は次のとおりです。
 - ノード入力パラメータ例：ワークフローにおいて、関数のカスタマイズで指定した入力パラメータを使用します。ユーザーの手動による追加は不要で、関数のカスタマイズにおけるノードに基づいて入力パラメータを取得します。
 - 関数Namespace：作成される関数は、デフォルトでCOSネームスペースの下に配置されます。
 - 関数の分類：よく用いられる機能を選択し、COSオブジェクトの通常の操作をすぐに実施するか、カスタマイズを選択し、自身でその他の機能の関連パラメータを設定します。
 - 機能タイプ：よく用いられる機能を選択する場合、プリセット機能の選択を行い、カスタマイズ関数を使用したCOSドキュメント操作の管理を参照します。
 - 関数の選択：現在のワークフローでは、非同期実行と起動状態のステータス追跡の関数のみをサポートしています。
 関数の新規追加が必要な場合は、「新規関数」をクリックし、SCFコンソールへジャンプして作成してください。次の設定項目の説明に従って設定すれば完了です。

    - 作成方法：テンプレート作成またはカスタマイズ作成を選択し、必要な機能を開発します。
    - あいまい検索：workflowを選択します。
6. 設定に間違いがないことを確認し、**確定**をクリックします。



