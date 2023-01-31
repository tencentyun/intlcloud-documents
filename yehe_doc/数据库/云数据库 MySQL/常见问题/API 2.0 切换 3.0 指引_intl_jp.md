TencentDB for MySQLは2018年01月01日にAPIインターフェースサービスを3.0に全面的にアップグレードしましたが、現在はAPI 2.0インターフェースに基づくアクセスの遅延が高く、使用が複雑であることを考慮して、TencentDB for MySQLのAPI 2.0インターフェースサービスの技術サポートは終了し、2023年03月31日にサービス終了となります。

TencentDB for MySQLのAPI 2.0に関連するインターフェースをビジネスでも使用している場合は、ビジネスに影響を与えないよう、できるだけ早くTencentDB for MySQL API　3.0にアップグレードすることをお勧めします。

下のAPI 2.0から3.0へのインターフェースリストを参照し、アップグレードする新しいインターフェースを見つけ、アップグレードを完了してください。

##　API 2.0から3.0へのインターフェースリスト
<table>
<thead><tr><th>API 2.0インターフェース</td><th>API 3.0インターフェース</td><th>API 3.0ドキュメント</td><th>インターフェースのパラメータ受け渡しの変化</td></tr></thead>
<tbody>
<tr>
<td>DescribeCdbInstances</td>
 <td>DescribeDBInstances</td>
 <td>インスタンスリスクのクエリーについて<a href="https://www.tencentcloud.com/zh/document/api/236/15872">こちら</a>。</td>
 <td>使用の複雑さを軽減するために、一部のパラメータが変更されています。<a href="https://www.tencentcloud.com/zh/document/api/236/15872">APIドキュメント</a>をご参照ください。</td>
 </tr>
 <tr>
<td>QueryCdbStatisticsInfo</td>
 <td>GetAppStat</td>
 <td>このインターフェースはサービス終了となり、呼び出しができません。インスタンス監視情報を取得するには、GetMonitorDataインターフェースを呼び出してください。<a href="https://intl.cloud.tencent.com/document/product/248/33881">詳細はこちら</a>。</td>
 <td>インターフェースのパラメータ受け渡しに変化がありません。</td>
 </tr>
 <tr>
<td>DescribeDBInstancesV3</td>
 <td>DescribeDBInstances</td>
 <td>インスタンスリスクのクエリーについて<a href="https://www.tencentcloud.com/zh/document/api/236/15872">こちら</a>。</td>
  <td>インターフェースのパラメータ受け渡しに変化がありません。</td>
 </tr>
 <tr>
<td>GetCdbExportLogUrl</td>
 <td>GetDownloadUrl</td>
 <td>このインターフェースは、既存のネットワークインターフェースを使用して置き換えることができます<br><li>type=slowlog_day スローログのクエリー DescribeSlowLogs<a href="https://intl.cloud.tencent.com/document/product/236/15845">詳細はこちら</a>。<br><li>type=errlog_day インスタンスエラーログのクエリー　DescribeErrorLogData　<a href="https://intl.cloud.tencent.com/document/product/236/35669">詳細はこちら</a>。<br><li>type=coldbackup　データバックアップリストのクエリー　DescribeBackups　<a href="https://intl.cloud.tencent.com/document/product/236/15842">詳細はこちら</a>。<br><li>type=binlog　ログバックアップリストのクエリー　DescribeBinlogs　<a href="https://intl.cloud.tencent.com/document/product/236/15843">詳細はこちら</a>。</td>
   <td>使用の複雑さを軽減するために、パラメータの一部が変更されています。APIの関連ドキュメントをご参照ください：<li><a href="https://intl.cloud.tencent.com/document/product/236/15845">スロークエリーログのクエリー</a>。<li><a href="https://intl.cloud.tencent.com/document/product/236/35669">インスタンスエラーログのクエリー</a>。<li><a href="https://intl.cloud.tencent.com/document/product/236/15842">データバックアップリストのクエリー</a>。<li><a href="https://intl.cloud.tencent.com/document/product/236/15843">ログバックアップリストのクエリー</a>。</td>
 </tr>
 <tr>
<td>RenewCdb</td>
 <td>RenewDBInstance</td>
 <td>クラウドデータベースインスタンスの期間更新　<a href="https://www.tencentcloud.com/zh/document/api/236/34477">詳細はこちら</a>。</td>
 <td>使用の複雑さを軽減するために、一部のパラメータが変更されています。<a href="https://www.tencentcloud.com/zh/document/api/236/34477">APIドキュメント</a>をご参照ください。</td>
 </tr>
</tbody></table>
