CAM 사용자는 Tencent Cloud에서 생성한 개체입니다. 하나의 CAM 사용자는 하나의 Tencent Cloud 계정과 연결됩니다. 등록된 Tencent Cloud 계정 ID는 **기본 계정**이며 [사용자 관리](https://console.cloud.tencent.com/cam)를 통해 다른 권한을 가진 **서브 계정**을 생성하고 협력 받을 수 있습니다. 서브 계정 유형은 [서브 사용자](https://intl.cloud.tencent.com/document/product/598/13674), [협력자](https://intl.cloud.tencent.com/document/product/598/13666) 및 [메시지 수신자](https://intl.cloud.tencent.com/document/product/598/13667)로 구분됩니다.

<table>
	<tr>
		<th rowspan="2">계정 유형</th>
		<th rowspan="2">기본 계정</th>
		<th colspan="3">서브 계정</th>
	</tr>
	<tr>
		<th>서브 사용자</th>
		<th>협력자</th>
		<th>메시지 수신자</th>
	</tr>
	<tr>
		<td>정의</td>
		<td>
					<ul>
						<li>Tencent Cloud의 모든 리소스를 소유하고 임의 리소스에 접근할 수 있습니다.</li>
						<li>기본 계정을 사용하여 리소스를 조작하는 것은 권장되지 않습니다.　서브　계정을　생성하고　최소 가중치 원칙에 따라　전략을　부여하여　제한된 권한을 가진　서브　계정으로　클라우드 리소스를　조작하는 것이 좋습니다.</li>
					</ul>
		</td>
		<td>서브 사용자는 기본　계정에 의해　생성되고 소유권은　해당　기본　계정에　있습니다.</td>
		<td>기본 계정 ID를 가지며 기본 계정의 협력자로 추가되면 해당 기본 계정의 서브　계정 중의 하나이며 기본 계정 ID로 다시 전환할 수 있습니다.</td>
		<td>메시지 수신 기능만 있습니다.</td>
	</tr>
	<tr>
		<td>콘솔을 통해 접근</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>프로그래밍으로　접근</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>전략　권한　부여</td>
		<td>기본적으로 모든 전략을 가지고 있습니다</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>메시지 알림</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
	</tr>
</table>
