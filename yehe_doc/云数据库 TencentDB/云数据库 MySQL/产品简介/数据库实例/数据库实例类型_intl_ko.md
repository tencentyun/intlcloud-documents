데이터베이스 인스턴스는 Tencent Cloud에서 단독적으로 실행되는 데이터베이스 환경으로서, 하나의 데이터베이스 인스턴스에는 사용자가 생성한 여러 개의 데이터베이스가 포함되어 있으며, 독립형 데이터베이스 인스턴스와 동일한 툴과 응용 프로그램을 사용하여 액세스할 수 있습니다.

TencentDB for MySQL에는 다음과 같은 두 가지 데이터베이스 인스턴스가 있습니다.

<table>
<thead><tr>
<th>인스턴스 유형 </th><th width=”20%”>정의 </th><th width="15%”>아키텍처</th><th>인스턴스 리스트 표시 여부 </th><th>기능</th></tr></thead>
<tbody><tr>
<td>마스터 인스턴스</td><td>읽기 및 쓰기 가능 인스턴스</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">단일 노드</a> <li> <a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">이중 노드</a><li> <a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">삼중 노드</a></td>
<td>는</td><td>마스터 인스턴스에 읽기 전용 인스턴스를 마운트 할 수 있어 읽기/쓰기 분리 기능을 사용할 수 있습니다.</td></tr>
<tr>
<td>읽기 전용 인스턴스</td><td>읽기 기능만 제공하는 인스턴스</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">단일 노드 </a></td><td>는</td>
<td>읽기 전용 인스턴스는 단독으로 존재할 수 없으며, 반드시 하나의 마스터 인스턴스에 종속되어야 합니다. 또한, 유일한 데이터 출처는 마스터 인스턴스로부터 동기화된 데이터이며, 마스터 인스턴스와 같은 리전이어야만 합니다.</td>


### 관련 정보
- 읽기 전용 인스턴스의 생성 작업 및 주의사항은 [읽기 전용 인스턴스 생성](https://intl.cloud.tencent.com/document/product/236/7270)을 참고 바랍니다.
- 읽기 전용 인스턴스 RO 그룹의 생성 및 설정은 [읽기 전용 인스턴스 관리](https://intl.cloud.tencent.com/document/product/236/11361)를 참고 바랍니다.

  
