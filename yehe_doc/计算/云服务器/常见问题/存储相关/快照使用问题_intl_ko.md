### 모든 리전에서 스냅샷을 사용할 수 있습니까?
현재 스냅샷 기능은 모든 가용존에서 지원됩니다.

### 스냅샷을 생성하면 디스크 성능에 영향을 줍니까?
스냅샷을 생성하면 소량의 클라우드 디스크 I/O를 차지합니다. 비즈니스 유휴 상태일 때 스냅샷을 생성하는 것이 좋습니다.

### 스냅샷 생성은 얼마나 걸립니까?
스냅샷 생성에 걸리는 시간은 디스크 쓰기 횟수 및 기본 읽기/쓰기 작업과 같은 요인의 영향을 받습니다. 스냅샷을 생성해도 디스크 사용에는 영향을 미치지 않습니다.

### 스냅샷을 롤백하려면 CVM을 종료해야 합니까?
- CVM에 마운트된 CBS의 경우 스냅샷을 롤백하려면 CVM을 종료해야 합니다.
- 마운트되지 않은 CBS의 경우 스냅샷을 직접 롤백할 수 있습니다.

### CBS의 첫 번째 전체 스냅샷 크기는 어떻게 계산됩니까?
CBS에 생성된 첫 번째 스냅샷은 특정 시점에서 CBS의 모든 데이터를 복사하는 전체 스냅샷입니다. 스냅샷 크기는 CBS의 사용된 용량과 같습니다. 예를 들어 CBS의 총 용량이 200GB이고 122GB를 사용한 경우 첫 번째 전체 스냅샷의 크기는 122GB입니다.

### CVM 인스턴스 스냅샷을 로컬 장치로 다운로드하거나 내보낼 수 있습니까?
아니요. 스냅샷은 다운로드하거나 로컬 장치로 내보낼 수 없습니다. 스냅샷에서 사용자 지정 이미지를 만든 다음 이미지를 내보내야 합니다.

### 자동 스냅샷은 수동 스냅샷과 다르거나 충돌합니까?
아니요. 두 가지를 동시에 사용할 수 있습니다. 그러나 자동 스냅샷이 생성되는 동안에는 수동 스냅샷을 생성할 수 없습니다.
- 자동 디스크 스냅샷 생성이 완료될 때까지 사용자 지정 디스크 스냅샷을 생성할 수 없으며 그 반대의 경우도 마찬가지입니다.
- 대용량 디스크에서 생성된 하나의 스냅샷이 두 개의 자동 스냅샷 사이의 간격보다 오래 지속되면 다음 자동 스냅샷은 건너뜁니다. 예를 들어, 자동 스냅샷이 9:00, 10:00, 11:00에 생성되도록 구성하고 9:00에 생성된 자동 스냅샷이 70분 동안 지속되고 10:10에 종료되는 경우 다음 자동 스냅샷은 10:00이 아니라 11:00에 생성됩니다.

### 로컬 디스크에 대한 스냅샷을 생성할 수 있습니까?
아니요. 애플리케이션 레이어에서 데이터 이중화를 사용하거나 클러스터용 배포 세트를 생성하여 애플리케이션 가용성을 향상시키는 것이 좋습니다.

### CBS를 릴리스한 후 로컬 스냅샷이 삭제됩니까?
아니요. 콘솔 또는 API를 통해 스냅샷을 삭제해야 합니다. 자세한 내용은 [스냅샷 삭제](https://intl.cloud.tencent.com/document/product/362/5758)를 참고하십시오.

### 파일 시스템에 표시되는 사용된 디스크 용량이 스냅샷 크기와 다른 이유는 무엇입니까?
CBS 스냅샷은 블록 레벨 클론 또는 백업입니다. 일반적으로 스냅샷 용량은 다음과 같은 이유로 파일 시스템에 표시되는 데이터 용량보다 큽니다.
- 하위 데이터 블록은 파일 시스템의 메타데이터를 저장합니다.
- 일부 데이터가 삭제됩니다. 데이터를 삭제하면 기록된 데이터 블록이 수정되어 스냅샷에 백업됩니다.

### Tencent Cloud에서 스냅샷이 삭제되는 것을 방지하려면 어떻게 해야 합니까?
- Tencent Cloud 계정이 연체되지 않도록 하십시오. 계정이 연체되면 스냅샷은 ‘격리’ 상태에 들어가고 ‘격리’ 상태의 스냅샷은 30일 동안 보관됩니다. 잔액이 0보다 크거나 같을 때까지 이 기간 동안 충전하지 않으면 계정의 모든 스냅샷(이미지 스냅샷 제외)은 만료 후 삭제됩니다.
- 정기 스냅샷 정책의 보존 시간 속성을 장기 보존으로 수정합니다. CBS의 자동 스냅샷이 최댓값에 도달하면 가장 먼저 생성된 스냅샷이 자동으로 삭제됩니다. 자세한 단계는 [정기 스냅샷](https://intl.cloud.tencent.com/document/product/362/35238)을 참고하십시오. 스냅샷 할당량은 [사용 제한](https://intl.cloud.tencent.com/document/product/362/32406)을 참고하십시오.

### 백업 비용을 줄이기 위해 스냅샷을 삭제하려면 어떻게 해야 합니까?
- CBS 스냅샷의 경우 콘솔 또는 API를 통해 직접 삭제할 수 있습니다. 자세한 내용은 [스냅샷 삭제](https://intl.cloud.tencent.com/document/product/362/5758)를 참고하십시오.
- 사용자 정의 이미지와 연결된 스냅샷의 경우 먼저 사용자 정의 이미지를 삭제한 다음 [스냅샷 삭제](https://intl.cloud.tencent.com/document/product/362/5758)를 해야 합니다.

### 인스턴스가 만료되거나 CBS가 릴리스되면 자동 스냅샷이 삭제됩니까?
아니요. 자동 스냅샷은 예약된 스냅샷의 보존 기간 정책에 따라 보존되기 때문에 인스턴스가 만료되거나 CBS가 릴리스된 후에도 삭제되지 않습니다. 예약된 스냅샷의 정책을 수정하려면 [예약된 스냅샷](https://intl.cloud.tencent.com/document/product/362/35238)을 참고하십시오.

### 이미지 또는 CBS가 생성된 스냅샷을 삭제하려면 어떻게 해야 합니까?
- CBS가 생성된 스냅샷을 별도로 삭제할 수 있습니다. 스냅샷을 삭제하면 원본 스냅샷 데이터에 의존하는 비즈니스를 운영할 수 없습니다.
- 사용자 정의 이미지가 생성된 스냅샷은 먼저 이미지를 삭제한 다음 스냅샷을 삭제해야 합니다.
- 인스턴스가 생성된 스냅샷: 스냅샷을 별도로 삭제할 수 있습니다. 스냅샷을 삭제하면 원본 스냅샷 데이터에 의존하는 비즈니스를 운영할 수 없습니다.

### 예약된 스냅샷을 기반으로 사용자 정의 이미지 또는 CBS를 생성하면 스냅샷 정책이 실행되지 않습니까?
아니요.


### CBS에 자동 스냅샷 정책이 여러 개 있을 수 있습니까?
자동 스냅샷 정책은 여러 개 있을 수 없습니다.

### 잘못된 작업으로 인한 데이터 손실을 방지하려면 어떻게 해야 합니까?
위험성이 있는 작업을 수행하기 전에 스냅샷을 만들어 데이터를 백업할 수 있습니다. 예를 들어, 중요한 시스템 파일을 수정하기 전에 스냅샷을 생성하고, 클래식 네트워크에서 VPC로 인스턴스를 마이그레이션하고, 데이터를 백업하고, 실수로 릴리스된 인스턴스를 복원하고, 네트워크 공격을 방지하거나, 운영 체제를 변경하거나, 프로덕션 환경에 대한 데이터 지원을 제공합니다. 자세한 내용은 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)을 참고하십시오. 오류가 발생하면 [스냅샷 롤백](https://intl.cloud.tencent.com/document/product/362/5756)하여 위험을 줄일 수 있습니다.

### 광저우 리전에 인스턴스를 생성하고 해당 인스턴스의 데이터 디스크에 대한 스냅샷을 생성했습니다. 인스턴스가 만료되어 출시된 후 광저우 리전에서 다른 인스턴스를 구매했습니다. 새 인스턴스의 스냅샷을 롤백하여 원본 인스턴스를 복원할 수 있습니까?
아니요. 스냅샷은 스냅샷이 생성된 CBS로만 롤백할 수 있습니다. 이전 데이터 디스크의 스냅샷을 사용하여 CBS를 생성하고 CBS를 새 인스턴스에 마운트할 수 있습니다. 자세한 내용은 [스냅샷을 사용하여 CBS 생성](https://intl.cloud.tencent.com/document/product/362/5757) 및 [CBS 마운트](https://intl.cloud.tencent.com/document/product/362/32401)를 참고하십시오.

### 스냅샷과 이미지의 차이점은 무엇인가요?
인스턴스에 마운트된 데이터 디스크가 없고 모든 데이터가 시스템 디스크에 기록되어 있는 경우 이미지를 생성하여 시스템 디스크의 데이터를 보호할 수 없습니다. 연속 백업을 위해 이미지를 예약할 수 없습니다. 시스템 디스크 데이터가 손상되면 이미지가 처음 생성된 상태로만 데이터를 복구할 수 있습니다. 따라서 이미지는 데이터 보호에 적합하지 않습니다. 구체적인 차이점은 다음과 같습니다.
<table>
		<tr>
		<th width="10%">이름</th>
		<td width="45%">스냅샷</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">이미지</a></td>
		</tr>
		<tr>
		<th>성질</th>
			<td>특정 시점에 CBS에 데이터 백업</td>
	   	<td>CVM 소프트웨어 설정을 위한 템플릿(운영체제, 사전 설치된 프로그램 등)</td>
		</tr>
		<tr>
		<th>적용 시나리오</th>
		<td>
			<ul>
				<li>중요한 비즈니스 데이터를 정기적으로 백업</li>
				<li>주요 작업 전 데이터 백업</li>
				<li>생성 데이터의 다중 복사 애플리케이션</li>
			</ul>
		</td>
		<td>
			<ul>
				<li>단기간에 변하지 않는 백업 시스템</li>
				<li>애플리케이션 일괄 배포</li>
				<li>시스템 마이그레이션</li>
			</ul>
		</td>
		</tr>
</table>

### 계정 A에서 계정 B로 스냅샷 데이터를 마이그레이션하려면 어떻게 해야 합니까?
스냅샷은 마이그레이션할 수 없습니다. 대신 마이그레이션하려는 스냅샷에서 이미지를 생성하고 다른 계정과 이미지를 공유할 수 있습니다.

### 데이터 디스크 스냅샷에서 사용자 정의 이미지를 생성할 수 있습니까?
아니요. 시스템 디스크 스냅샷에서만 사용자 정의 이미지를 생성할 수 있습니다.



