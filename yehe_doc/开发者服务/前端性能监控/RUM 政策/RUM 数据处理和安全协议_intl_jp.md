## 1\. 背景
本モジュールは、お客様がReal User Monitoring（以下「機能」）をご利用になる場合に適用されます。本モジュールは、[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)に掲載されているData Processing and Security Agreement（データ処理およびセキュリティに関する契約）（以下「DPSA」）に組み込まれます。本モジュールにおける用語のうち本書内に定義のないものは、DPSA内で定義された意味を有するものとします。DPSAと本モジュールとの間に矛盾がある場合には、その不一致の範囲で本モジュールを優先するものとします。

## 2\. 処理
当社は、本機能に関連して以下のデータを処理します。

<table>
   <tr>
      <th>個人情報</th>
      <th>用途</th>
   </tr>
   <tr>
      <td><b>オリジナルログデータ：</b>JSエラーログ、 Promiseエラー、JS読み込み例外、インターフェースリクエストログ、デバイス型番、オペレーターの種類、ネットワークの種類、オペレーティングシステム、地域、デバイスのブランド、カスタムイベントデータ（お客様定義のレポートイベントから取得したデータ） </td>
      <td>この情報は、お客様に本機能を提供する目的で使用します。
<br/>このデータは当社のクラウドログサービス（CLS）機能とTencentDB for Redis (Redis)機能、TencentDB for MySQL機能に統合され、その中で保存・バックアップされます。</td>
</td>
   <tr>
      <td><b>インジケータデータ：</b>オリジナルログデータを系統的に整理し集計したデータ（ページのパフォーマンス、API監視、静的リソース監視、異常発生数）</td>
     <td>この情報は、お客様に本機能を提供する目的で使用します。
<br/>このデータは当社のCLS機能とRedis機能、TencentDB for MySQL機能に統合され、その中で保存・バックアップされます。当社のクラウド監視（CM）機能を有効化・購入された場合、本機能のご提供（インジケータデータが異常である場合に通知）にあたりCMでもこのデータが収集されます。</td>
</td>
   <tr>
     <td><b>プロジェクトデータ：</b>プロジェクト名、プロジェクトの説明、プロジェクトの種類、ウェブサイトアドレス、プロジェクト格付け、PV/UVデータ。</td>
     <td>この情報は、お客様に本機能を提供する目的で使用します。
<br/>このデータは当社のCLS機能とRedis機能、TencentDB for MySQL機能に統合され、その中で保存・バックアップされます。 </td>
</tr>
   <tr> 
</table> 



## 3\. サービス地域

DPSAに記載のとおり。

## 4\. 副処理者
DPSA で規定されている通り、Aceville Pte Ltd.を含みます。

## 5\. データ保持
当社は、本機能に関連して処理された個人データを以下のとおり保管します。

<table>
   <tr>
      <th>個人情報</th>
      <th>保持ポリシー</th>
​        </tr>
   <tr>
      <td>オリジナルログデータ</td>
      <td>左記データは、手動で削除するまで保持されます。それ以外の場合、30日間保存されます。</tr>
   </tr>
   <tr>
      <td>インジケータデータ</td>
      <td>左記データは、手動で削除するまで保持されます。それ以外の場合、15日間保存されます。</tr>
      </tr>
   <tr> 
      <td>プロジェクトデータ</td>
      <td>左記データは、手動で削除するまで保持されます。それ以外の場合、 1年間保持されます（保存期間が90日間のプロジェクト格付けとPV/UVデータを除く） </td>
</table>


お客様は、DPSAに基づき、当該個人データの削除を依頼することができます。

## 6\. 特記条件
お客様は、エンドユーザーのうち自己の個人データの処理に対して同意をすることのできる最低年齢に達している個人のみが本機能を使用するという状況を、確実なものとする必要があります。その年齢は、エンドユーザーの管轄法域によって異なることがあります。