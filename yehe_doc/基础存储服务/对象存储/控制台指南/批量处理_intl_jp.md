## 概要

Cloud Object Storage（COS）はバッチ処理機能により、バケット内のオブジェクトに対して大規模なバッチ操作を実行することができます。現在、以下の操作に対して、バッチ処理を行うことができます。

- オブジェクトのコピー
- アーカイブオブジェクトの復元

処理したいオブジェクトをオブジェクトリストファイルに整理することができます。このリストファイルは、リスト機能によって作成されたリストレポートから取得できます（あらかじめ[リスト機能の有効化](https://intl.cloud.tencent.com/document/product/436/30624)を行う必要があります）。また、指定された形式でご自分で作成することも可能です。COSバッチ処理機能により、このオブジェクトリストファイルを元にバッチ処理を行うことができます。COSバッチ処理タスクの詳細情報については、[バッチ処理の概要](https://intl.cloud.tencent.com/document/product/436/32958)をご参照ください。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バッチ処理**をクリックし、バッチ処理管理ページに進みます。
3. **タスクの作成**をクリックすると、バッチ処理タスクの作成が開始されます。

   ![](https://qcloudimg.tencent-cloud.cn/raw/96365cc5d704e9ee76de549e29ed6514.png)
設定項目の説明は次のとおりです。
 - **タスクリージョン**：タスクが作成されるリージョンを選択します。タスクリージョンは、リストで処理されるオブジェクトのバケットリージョンと同じである必要があります。同じでない場合、タスクは失敗します。

>? 現在、バッチ処理機能は中国大陸のパブリッククラウドリージョン、シリコンバレーリージョンでサポートしています。
>
 - **リスト形式**：使用するリストオブジェクトのタイプを選択します。以下の2つの形式があります。
<table>
   <tr>
      <th>リスト形式</th>
      <th>フィールド</th>
      <th>設定説明</th>
   </tr>
   <tr>
      <td nowrap="nowrap">COSリストレポート</td>
      <td>-</td>
      <td>COSが生成したリストレポートと、ユーザーがカスタマイズしたCSVファイルのどちらかを選択できます</td>
   </tr>
   <tr>
      <td rowspan="3">CSV</td>
      <td>Bucket</td>
      <td>バケット名</td>
   </tr>
   <tr>
      <td>Key</td>
      <td>バケット内のオブジェクト名です。オブジェクト名にURLエンコード形式が用いられている場合は、正常な形式にデコードしてからでなければ使用できません</td>
   </tr>
   <tr>
      <td>VersionId</td>
      <td>オブジェクトのバージョンIDです。バケット上でバージョン管理を有効にすると、COSはバケットに追加されたオブジェクトにバージョン番号を割り当てます。最新ではないバージョンのオブジェクトを使用したい場合、リストオブジェクトのバージョンIDを含めて選択することができます</td>
   </tr>
</table>
 - **リストバケット**：リストが配置されているバケットを選択します。
 - **リストファイルパス**：リストファイルまたはCSVファイルが配置されているパスを選択します。形式はそれぞれjsonとcsvです。例えば、バケット`examplebucket-1250000000`のルートディレクトリにリストファイルを保存している場合、リストパスは`manifest.json`となります。 
4. **次のステップ**をクリックし、タスクのタイプを選択します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/a5ea91301f9a227db26a8723147afc2f.png)
設定項目の説明は次のとおりです。
  - **一括データコピー**：
    - ターゲットバケット：リスト内のオブジェクトをコピーした後に保存したいバケットです。
    - プレフィックス操作：コピーしたオブジェクトに対し、プレフィックスの追加、置き換えまたは削除を選択できます。
    - ストレージタイプ：コピーされたオブジェクトに対しストレージタイプを設定します。標準ストレージ、低頻度ストレージ、アーカイブストレージ、ディープアーカイブストレージから選択できます。
    - サーバー側の暗号化：コピーされたオブジェクトに対し暗号化するかどうかを選択します。暗号化なしとSSE-COS暗号化から選択できます。
    - アクセス権限：コピーしたオブジェクトに対しアクセス権限を設定します。すべての権限のコピー、すべての権限の置き換え、新しい権限の追加から選択できます。
    - オブジェクトメタデータ：コピーされたオブジェクトに対しメタデータを設定します。すべてのメタデータのコピー、すべてのメタデータの置き換え、新しいメタデータの追加から選択できます。
    - オブジェクトタグ：コピーされたオブジェクトに対しオブジェクトタグを設定します。すべてのタグのコピー、すべてのタグの置き換え、新しいタグの追加から選択できます。
  - **CASのバッチ復元**：
    - リカバリモード：標準モードとバッチモードから選択できます。リカバリモードについては、[アーカイブオブジェクトの復元](https://intl.cloud.tencent.com/document/product/436/30961)をご参照ください。
    - レプリカの有効期間：レプリカが自動的に期限切れになり、削除されるまでの日数を設定します。設定範囲は、最短で1日、最長で365日です。
5. **次のステップ**をクリックし、以下の関連設定を入力します。

   ![](https://qcloudimg.tencent-cloud.cn/raw/51b4635e62af9c862d78a99c31ea5e93.png)
 - **タスク説明（オプション）**：このタスクの説明です。未入力でもかまいません。
 - **タスクの優先度**：より優先度の高いタスクが先に実行されます。0以外の正の整数を入力でき、数字が大きいほど優先度が高いことを意味します。
 - **タスクレポート**：タスクレポートを発行するかどうかを選択できます。
 - **CAMロール**：CAMロールを作成するか、既存のCAMロールを選択して、COSに操作権限を付与することができます。
 
>! バッチ処理では、CAMロールを作成する方法でCOSバッチ処理の権限を付与する必要があります。CAMロールの詳細については、[CAMロールの概要](https://intl.cloud.tencent.com/document/product/598/19420)をご参照ください。
>
6. **次のステップ**をクリックし、入力したバッチ処理タスクの設定をチェックし、必要に応じてチェックを入れます。**この項目にチェックを入れると、タスクは作成直後に起動します。上記の設定情報が正しいことを確認してください**。
変更したい場合は、対応する**変更**または**前へ戻る**をクリックしてください。
  ![](https://qcloudimg.tencent-cloud.cn/raw/52a427cd3a47d865281311a60be6b582.png)
7. 誤りがないことを確認したら、**作成**/**作成して起動**をクリックすれば完了です。
バッチタスクの作成が完了すると、作成済みのタスクはタスクリストに表示されるようになります。タスクをキャンセルしたい場合は、右側の**タスクのキャンセル**をクリックします。

  ![](https://qcloudimg.tencent-cloud.cn/raw/766a6283403513af3d84c0d9d63ca48a.png)

