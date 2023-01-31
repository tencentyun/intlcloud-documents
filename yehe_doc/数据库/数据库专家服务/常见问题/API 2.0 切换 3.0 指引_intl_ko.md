TencentDB for MySQL은 2018년 01월 01일에 API 서비스를 v3.0으로 완전히 업그레이드했습니다. API 2.0은 액세스 대기 시간이 더 길고 사용하기 더 복잡하기 때문에 API 2.0에 대한 기술 지원이 중단되었으며 2023년 03월 31일에 비활성화됩니다.

비즈니스에 영향을 미치지 않도록 가능한 한 빨리 TencentDB for MySQL API 3.0으로 업그레이드하는 것이 좋습니다.

아래의 API 2.0 및 3.0 비교표를 참고하여 업그레이드에 필요한 새 API를 찾고 그에 따라 업그레이드를 완료할 수 있습니다.

## v2.0에서 v3.0으로 전환된 API 목록
<table>
<thead><tr><th>API 2.0</td><th>API 3.0</td><th>API 3.0 문서</td><th>입력 매개변수 변경</td></tr></thead>
<tbody>
<tr>
<td>DescribeCdbInstances</td>
 <td>DescribeDBInstances</td>
 <td>인스턴스 목록을 쿼리합니다. 자세한 내용은 <a href="https://www.tencentcloud.com/zh/document/api/236/15872">DescribeDBInstances</a>를 참고하십시오.</td>
 <td>API를 더 쉽게 사용할 수 있도록 <a href="https://www.tencentcloud.com/zh/document/api/236/15872">API 문서</a>에 설명된 대로 일부 매개변수가 변경되었습니다.</td>
 </tr>
 <tr>
<td>QueryCdbStatisticsInfo</td>
 <td>GetAppStat</td>
 <td>이 API는 사용되지 않습니다. 인스턴스 모니터링 정보를 얻으려면 GetMonitorData를 호출하십시오. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/248/33881"> GetMonitorData</a>를 참고하십시오.</td>
 <td>변경 사항 없음.</td>
 </tr>
 <tr>
<td>DescribeDBInstancesV3</td>
 <td>DescribeDBInstances</td>
 <td>인스턴스 목록을 쿼리합니다. 자세한 내용은 <a href="https://www.tencentcloud.com/zh/document/api/236/15872">DescribeDBInstances</a>를 참고하십시오.</td>
  <td>변경 사항 없음.</td>
 </tr>
 <tr>
<td>GetCdbExportLogUrl</td>
 <td>GetDownloadUrl</td>
 <td><br><li>type = slowlog_day: 슬로우 로그를 쿼리합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/15845">DescribeSlowLogs</a>를 참고하십시오. <br><li>type = errlog_day: 인스턴스의 오류 로그를 쿼리합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/35669">DescribeErrorLogData</a>를 참고하십시오. <br><li>type = coldbackup: 데이터 백업 목록을 쿼리합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/15842">DescribeBackups</a>를 참고하십시오. <br><li>type = binlog: 로그 백업 목록을 쿼리합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/15843">DescribeBinlogs</a>를 참고하십시오. </td>
   <td>API를 더 쉽게 사용할 수 있도록 일부 매개변수가 다음과 같이 변경되었습니다. <li><a href="https://intl.cloud.tencent.com/document/product/236/15845">DescribeSlowLogs</a>. <li><a href="https://intl.cloud.tencent.com/document/product/236/35669">DescribeErrorLogData</a>. <li><a href="https://intl.cloud.tencent.com/document/product/236/15842">DescribeBackups</a>. <li><a href="https://intl.cloud.tencent.com/document/product/236/15843">DescribeBinlogs</a>.</td>
 </tr>
 <tr>
<td>RenewCdb</td>
 <td>RenewDBInstance</td>
 <td>TencentDB 인스턴스를 갱신합니다. 자세한 내용은 <a href="https://www.tencentcloud.com/zh/document/api/236/34477">ModifyNameOrDescByDpId</a>를 참고하십시오.</td>
 <td>API를 더 쉽게 사용할 수 있도록 <a href="https://www.tencentcloud.com/zh/document/api/236/34477">ModifyNameOrDescByDpId</a>에 설명된 대로 일부 매개변수가 변경되었습니다.</td>
 </tr>
</tbody></table>
