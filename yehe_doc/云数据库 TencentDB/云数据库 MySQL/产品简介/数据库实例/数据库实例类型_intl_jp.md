データベースインスタンスはTencent Cloudで単独で動作するデータベース環境です。データベースインスタンスにはユーザーによって作成された複数のデータベースを含めることができ、スタンドアロン・データベースのインスタンスと同じのツール及びアプリケーションによりアクセスできます。

Tencent MySQLには次の3種類のデータベースインスタンスがあります。

<table>
<thead>
<tr>
<th>インスタンスタイプ</th>
<th width="20%">定義</th>
<th width="15%">アーキテクチャ</th>
<th>インスタンスリストが見えるか</th>
<th>機能</th>
</tr>
</thead>
<tbody><tr>
<td>マスターインスタンス</td>
<td>読み書き可能なインスタンス</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">基本版</a> <li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">高可用版</a><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">金融版</a></td>
<td>はい</td>
<td>マスターインスタンスは読取専用インスタンス及び災害復旧インスタンスをマウントし、リード・ライト分離と遠隔地の災害復旧機能を実現することができます</td>
</tr>
<tr>
<td>読取専用インスタンス</td>
<td>読取機能のみを提供するインスタンス</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">単ノード高IOバージョン</a></td>
<td>はい</td>
<td>読取専用インスタンスは個別に存在できず、ある特定のマスターインスタンスに所属しなければなりません。唯一のデータソースはマスターインスタンスからの同期データであり、マスターインスタンスと同一地域でなければなりません</td>
</tr>
<tr>
<td>災害復旧インスタンス</td>
<td>Availability Zone間及び地域間の災害対応能力を提供するインスタンス</td>
<td><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">高可用版</a><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">金融版</a></td>
<td>はい</td>
<td>災害復旧インスタンスは同期時に読取のみであり、災害復旧インスタンスはマスターインスタンスから同期関係を自発的に切り離し、プロアクティブにマスターインスタンスに昇格することで、読取と書込のアクセスが可能になり、またマスターインスタンスとは別の場所に配置されなければなりません</td>
</tr>
</tbody></table>

### 関連情報
- 読取専用インスタンスの新規作成及び注意事項については、[読取専用インスタンスの新規作成](https://intl.cloud.tencent.com/document/product/236/7270)をご参照ください。
- 読取専用インスタンスROグループの新規作成と構成については、[読取専用インスタンスの管理](https://intl.cloud.tencent.com/document/product/236/11361)をご参照ください。
- 災害復旧インスタンスの新規作成及び注意事項については、[災害復旧インスタンスの管理](https://intl.cloud.tencent.com/document/product/236/7272)をご参照ください。
