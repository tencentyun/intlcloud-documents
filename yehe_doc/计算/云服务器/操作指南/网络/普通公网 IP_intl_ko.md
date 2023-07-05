## 작업 시나리오
본문은 일반 공용 IP 주소를 사용하는 방법을 설명합니다. 일반 공용 IP는 CVM 구매 시에만 할당이 가능하며, CVM과의 바인딩을 해제 할 수 없습니다. 구매 시 할당되지 않으면 획득할 수 없습니다.
<dx-alert infotype="explain" title="">
- 기존 계정 유형의 경우 CVM에서 EIP 바인딩 해제 시 각 계정은 일반 공용 IP를 하루 10회 무료 재할당 가능합니다.
- 현재 일반 공용 IP 주소 유형은 일반 BGP IP만 지원합니다.
</dx-alert>





## 작업 가이드


다음과 같은 일반 공용 IP 기능을 사용할 수 있습니다.

<table>
  <tr>
	<th width="17%">기능 유형</th>
	<th>작업 시나리오</th>
	<th width="20%">관련 문서</th>	
  </tr>
  <tr>
	<td>공용 IP 주소 검색</td>
	<td>실수로 공용 IP 주소(EIP 및 일반 공용 IP 포함)를 릴리스하거나 반환한 경우 
	공용 IP 콘솔에서 되돌릴 수 있습니다. 되돌린 후 공용 IP는 EIP입니다.</td>
	<td>
	  -
	</td>
  </tr>
  <tr>
	<td>일반 공용 IP를 EIP로 전환</td>
	<td>CVM의 일반 공용 IP를 EIP로 전환합니다. 전환 후 EIP는 
	CVM와 언제든지 바인딩 해제 및 바인딩이 가능하여 공용 IP의 효율적인 관리를 보다 쉽게 ​​구현할 수 있습니다.</td>
	<td>
	  -</a>
	</td>
  </tr>
  <tr>
	<td>공용 IP 변경</td>
	<td>CVM의 일반 공용 IP를 교체하고, 교체 후 기존 공용 IP를 릴리스합니다.</td>
	<td>
	  <ul style="margin:0px">
	 <a href="https://intl.cloud.tencent.com/document/product/213/16642">인스턴스 공용 IP 변경</a>
		</li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>네트워크 대역폭 변경</td>
  <td>필요에 따라 대역폭을 조정하거나 과금 방식을 조정하면 실시간으로 적용됩니다.</td>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/213/15517">네트워크 설정 변경</a>
	</td>
  </tr>
</table>

