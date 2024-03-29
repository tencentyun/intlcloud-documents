## 1\. 背景

本モジュールは、お客様が Cloud Streaming Services 機能(以下「機能」)を使用する場合**に**適用されます。本モジュールは、[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)におけるデータ処理およびセキュリティに関する契約(Data Processing and Security Agreement）に組み込まれたことになります。本モジュールにおける用語のうち本書内に定義のないものは、DPSA内で定義された意味を有するものとします。DPSAと本モジュールとの間に矛盾がある場合には、その不一致の範囲で本モジュールが優先するものとします。

## 2\. 処理

当社は、本機能に関連して以下のデータを処理します。

| **個人情報**                                     | **用途**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **構成データ：** <li>ドメイン名の設定(認証の設定、帯域幅上限の設定、httpsの設定(SSL証明書を含む)、リージョンの設定、テンプレートの設定、オリジンサーバーの設定)。<br><li>記録テンプレート(テンプレート名、記録ファイル形式、記録単一ファイル期間、保存期間、タイムアウトの再開(hlsのみ)、VODサブアプリケーションへの記録)。<br><li>透かしテンプレート(テンプレート名、透かし画像、透かしの場所)。<br><li>トランスコードテンプレート（テンプレート名、ビットレート、ライブ画面の高さ、GOP、符号化方式）。<br><li>スクリーンショットテンプレート(テンプレート名、スクリーンショットの頻度、スクリーンショットストレージのcosの場所、スクリーンショットファイル名、スマートポルノ検出)。 | 弊社は、お客様固有の設定に基づいて、お客様とエンドユーザーに本機能をご提供する目的でのみ左記データを処理します。<br/>このデータは、当社の TencentDB for MySQL 機能に保存されますのでご注意ください。 |
| **ライブ録画ビデオ**(ライブストリームのビデオを録画することを選択した場合) | 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。<br/>このデータは、当社のビデオ・オン・デマンド（VOD）機能に保存されますので、ご注意ください。 |
| **ライブスクリーンショット(ライブスクリーンショット** の記録を選択した場合)、ポルノ検出後の結果のライブスクリーンショットを含む(ポルノ検出設定機能を有効にすることを選択した場合)  | 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。<br/>このデータは、当社のクラウドオブジェクトストレージ（COS）機能に保存されますので、ご注意ください。<br/>なお、お客様が本機能のポルノ検出設定機能を有効にした場合、COSに保存された当該データは、本機能を必要に応じて提供するため（ポルノ情報を審査・特定し、それに関する結果を返すことを含む）、当社のイメージモデレーションシステム（IMS）機能に送信されることにご注意ください。IMSは、ポルノ検出プロセスを完了し、それに関する結果をお客様に返すために必要な期間だけ、ライブスクリーンショットを保持します。 |


## 3\. サービス地域

DPSAに記載のとおり。

## 4\. 副処理者

DPSA で規定されている通り、Aceville Pte Ltd.を含みます。

## 5\. データ保持

当社は、本機能に関連して処理された個人データを以下のとおり保管します。

| **個人情報**                                | **保持ポリシー**                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| 構成データライブ録画ビデオライブスクリーンショット | お客様が選択したデータ保持期間と同じ期間、データを保持します。あるいは、アカウントを削除するか、機能の使用を終了すると、60日後に左記データが削除されます。 |

お客様は、DPSAに基づき、これらの個人データの削除を依頼することができます。

## 6\. 特記条項

お客様は、本機能を、個人データの処理に同意できる最低年齢に達しているエンドユーザー、または最低年齢に達していない個人の場合、親の同意が得られているエンドユーザーのみが使用することを保証する必要があります。その年齢は、エンドユーザーの管轄法域によって異なることがあります。

お客様は、本機能に関するエンドユーザの個人データの処理に関して、適用法に従い、かつ当社が適用法を遵守できるように、エンドユーザから必要な全ての同意を取得し、維持することを表明し、保証し、引き受けるものとします。  