
## 지원 제품
데이터베이스 감사 기능 지원 사항:
- TencentDB for MySQL 5.6, 5.7, 8.0 2노드와 3노드를 지원합니다. TencentDB for MySQL 5.5 버전 및 TencentDB for MySQL 단일 노드는 현재 지원하지 않습니다.
- TDSQL-C for MySQL.
- TencentDB for MongoDB 4.0.

## 감사 가격
[데이터베이스 감사](https://console.cloud.tencent.com/dls/mysql) 감사 로그 저장 용량에 따라 과금합니다. 과금 단위는 1시간으로 1시간 이하는 모두 1시간으로 과금합니다.

<table>
<thead><tr><th rowspan="2" width=30%>리전</th><th colspan = "2" >가격(USD/GB/시간)</th></tr><th>고빈도 액세스 스토리지</th><th>표준IA 스토리지</th></tr></thead>
<tbody>
<tr>
<td>중국(금융 리전 포함)</td>
<td>	0.00147059</td><td>0.00018382</td></tr>
<tr>
<td>기타 국가 및 지역</td>
<td>	0.00220588</td><td>0.00220588</td></tr>        
</tbody></table>

>?현재는 TencentDB for MySQL만 고빈도 및 표준IA 스토리지가 지원되며, 다른 클라우드 데이터베이스 제품은 고빈도 스토리지만 지원됩니다.

## 구매 방식
- [TencentDB for MySQL 감사 활성화](https://intl.cloud.tencent.com/document/product/1102/41311)
- [TencentDB for MySQL 감사 활성화](https://intl.cloud.tencent.com/document/product/1102/41312)
- [TencentDB for MongoDB에서 감사 활성화](https://intl.cloud.tencent.com/document/product/1102/47769)

## 릴리스 안내
- CDB (사용량 과금）감사 기능 활성화 후, 사용자가 해당 CDB를 릴리스하면, 해당 CDB에 적용되던 감사 기능도 정지되며, 관련 로그는 자동 삭제되고, 복구할 수 없습니다.
- CDB (월간권) 감사 기능 활성화 후, 사용자가 해당 CDB를 릴리스하거나 CDB가 기간 만료로 릴리스될 경우, 해당 CDB에 적용되던 기능도 정지되며, 로그는 자동 삭제되고, 복구할 수 없습니다. 

## 연체 결제 정책
1. **계정 잔액이 0보다 적을 때부터 적용됩니다**
   - 2시간 동안, SQL 감사 서비스를 사용할 수 있으며 계속 과금됩니다.  
   - 2시간 이후부터 SQL 감사 기능이 **자동 정지**되며 과금도 정지됩니다.

2. ** 기능 자동 정지 이후**
   - 자동 정지 후 24시간 동안, 잔액을 0 이상으로 충전하면 SQL 감사 기능은 복구되고 과금이 진행됩니다. 계정 잔액이 0 이하이면 SQL 감사 기능을 복구할 수 없습니다.   
   - 자동 정지 후 24시간이 지난 후에도 계정 잔액이 0보다 적으면 로그는 삭제되고 복구할 수 없습니다. 
