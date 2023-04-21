このドキュメントは、ユーザーが最大限に安全かつ確実にCVMを利用することに役立ちます。

## セキュリティとネットワーク

- **アクセス制限：**ファイアウォール（[セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452)）を使用して、信頼できるアドレスがインスタンスへのアクセスを許可することによってアクセスを制限します。セキュリティグループで最も厳しい規則を設定します。例えばポートアクセス、IP アドレスアクセスを制限するなど。
- **セキュリティグレベル：**異なるセキュリティグループ規則を作成して異なるセキュリティグレベルのインスタンスグループに適用し、重要な業務を実行しているインスタンスが外部に簡単にアクセスできないように確保します。
- **ネットワークロジック隔離：** [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/213/5227)を利用してロジック領域の分割を行います。
- **アカウント権限管理：**同じクラウドリソースグループに対して複数の異なるアカウント制御が必要な場合、ユーザーは[ポリシーメカニズム](https://intl.cloud.tencent.com/document/product/598/10601) を使用し、クラウドリソースへのアクセスを制御できます。
- **安全ログイン：**できるだけ[SSH キー](https://intl.cloud.tencent.com/document/product/213/6092) でユーザーの Linux タイプのインスタンスにログインします。[パスワードログイン](https://intl.cloud.tencent.com/document/product/213/6093) を使用してのインスタンスは定期にパスワードを変更する必要があります。

## ストレージ

- **ハードウェアストレージ：**高い信頼性を求めるデータに対して、Tencent CloudのCloud Block Storageを利用してデータの永続性を保証し、できるだけ [ローカルディスク](https://intl.cloud.tencent.com/document/product/213/5798)を選択しないでください。詳細については、 [Cloud Block Storage製品ドキュメント](https://intl.cloud.tencent.com/document/product/362)をご参照ください。
- **データベース：**頻繁にアクセスし、容量が不安定なデータベースに対して、Tencent Cloudクラウドデータベースを利用できます。

## バックアップとリカバー

- **同一リージョンのインスタンスバックアップ：**　**カスタマイズイメージ**および**Cloud Block Storageスナップショット**方式を利用してインスタンスと業務データをバックアップします。詳細については、[Cloud Block Storageスナップショット](https://intl.cloud.tencent.com/document/product/362/5754) と [カスタマイズイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)をご参照ください。
- **クロスリージョンのインスタンスバックアップ：** [イメージレプリケーション](https://intl.cloud.tencent.com/document/product/213/4943) を利用してクロスリージョンレプリケーションとインスタンスバックアップを行います。
- **インスタンス故障のブロック：** [Elastic IP](https://intl.cloud.tencent.com/document/product/213/5733)によってドメイン名マッピングを行い、CVMが利用できない時に迅速にサービス IP を別のCVMインスタンスにリダイレクトすることを保証することにより、インスタンス故障をブロックします。

## モニタリングとアラーム
- **モニタリングと応答イベント：**定期的にモニタリングデータを確認して、かつ適切なアラームを設置します。詳細については、[TCOP製品ドキュメント](https://intl.cloud.tencent.com/document/product/248)をご参照ください。
- **突発リクエストの処理：** [Auto Scaling](https://intl.cloud.tencent.com/document/product/377)を利用し、 ピークサービス中のCVMの安定性を保証でき、更に不健康のインスタンスを自動的に置き換えることもできます。
