TencentDB for MySQL 인스턴스, 줄여서 ‘인스턴스’는 Tencent Cloud에서 독립적으로 실행되는 데이터베이스 환경으로, 사용자가 TencentDB for MySQL 서비스를 구매하는 기본 단위입니다. 사용자는 콘솔을 통해 TencentDB for MySQL 인스턴스를 생성, 수정 및 삭제할 수 있습니다.
각 인스턴스는 서로 독립적이며 리소스가 격리되어 있습니다. CPU, 메모리, IO 등 상호 선점 문제가 존재하지 않습니다. 각 인스턴스는 데이터베이스 유형, 버전 등과 같은 고유한 특성을 가지며, 시스템은 해당 인스턴스의 동작을 제어하는 ​​매개변수를 가지고 있습니다.

TencentDB for MySQL에는 다음과 같은 세 가지 데이터베이스 인스턴스가 있습니다.

<table>
<thead><tr>
<th>인스턴스 유형</th><th width=”20%”>정의</th><th width="15%”>아키텍처</th><th>인스턴스 리스트 표시 여부</th><th>기능</th></tr></thead>
<tbody><tr>
<td>프라이머리 인스턴스</td><td>읽기 및 쓰기 가능 인스턴스</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">단일 노드</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">2노드</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">3노드</a></td>
<td>Yes</td><td>프라이머리 인스턴스에 읽기 전용 인스턴스 또는 재해 복구 인스턴스를 마운트하여 읽기/쓰기 분리 및 원격 재해 복구 기능을 구현할 수 있습니다.</td></tr>
<tr>
<td>읽기 전용 인스턴스</td><td>읽기 기능만 제공하는 인스턴스</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">단일 노드</a></td><td>Yes</td>
<td>읽기 전용 인스턴스는 단독으로 존재할 수 없으며, 반드시 하나의 프라이머리 인스턴스에 종속되어야 합니다. 또한, 유일한 데이터 출처는 프라이머리 인스턴스로부터 동기화된 데이터이며, 프라이머리 인스턴스와 같은 리전이어야만 합니다.</td></tr>
<tr>
<td>재해 복구 인스턴스</td><td>교차 가용존 및 리전 간 재해 복구 기능을 제공하는 인스턴스</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">2노드</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">3노드</a><td>Yes</td>
<td>재해 복구 인스턴스는 동기화 시에 읽기만 가능하며, 프라이머리 인스턴스와의 동기화 관계를 자체적으로 종료하고 프라이머리 인스턴스로 승격하여 읽기 및 쓰기 액세스 기능을 제공할 수 있습니다. 따라서, 재해 복구 인스턴스의 리전을 프라이머리 인스턴스와 다르게 하시길 권장합니다.</td></tr>
</tbody></table>

### 관련 정보
- 읽기 전용 인스턴스의 생성 작업 및 주의사항은 [읽기 전용 인스턴스 생성](https://intl.cloud.tencent.com/document/product/236/7270)을 참고 바랍니다.
- 읽기 전용 인스턴스 RO 그룹의 생성 및 설정은 [읽기 전용 인스턴스 관리](https://intl.cloud.tencent.com/document/product/236/11361)를 참고 바랍니다.
- 재해 복구 인스턴스의 생성 작업 및 주의사항은 [재해 복구 인스턴스 관리](https://intl.cloud.tencent.com/document/product/236/7272)를 참고 바랍니다.
