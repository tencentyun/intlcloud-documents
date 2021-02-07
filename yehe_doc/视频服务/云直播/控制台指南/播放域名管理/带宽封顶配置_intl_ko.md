Tencent Cloud는 재생 도메인의 대역폭 상한 설정 기능을 제공합니다. 해당 기능은 기본적으로 비활성화되어 있으며, 도메인 가속 리전의 다운스트림 대역폭 상한값을 설정하면 통계 주기 내에 대역폭 피크치가 임계값에 도달하는 경우 라이브 방송 요청에 대해 403을 반환합니다. 도메인 실제 사용 상황에 따라 대역폭 상한 기능을 활성화하거나 비활성화할 수 있습니다.


## 전제 조건
- [LVB 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
- [재생 도메인](https://cloud.tencent.com/document/product/267/20381)이 추가되어 있어야 합니다.


<h2 id="limit">사용 제한</h2>

| 재생 도메인 가속 리전 유형 | 제한 리전 기본 유형 | 비고 |
|---------|---------|---------|
| 중국대륙 | 중국대륙 | 제한 리전 수정 불가 |
| 중국홍콩, 마카오, 중국대만 지역 및 해외 리전 | 중국홍콩, 마카오, 중국대만 리전 및 해외 리전 | 제한 리전 수정 불가 |
| 글로벌 가속 | 글로벌 가속 | 제한 리전 수정 지원:<ul style="margin-bottom:0px;"><li>중국대륙 제한과 중국홍콩, 마카오, 중국대만 리전 및 해외 리전 제한 각각 설정</li><li>글로벌 가속 리전 제한 동시 설정</li></ul> |


## 대역폭 상한 설정 생성
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **재생 도메인** 또는 오른쪽에 있는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Advanced Configuration] 탭을 선택하여 [Bandwidth Cap Configuration] 부분을 확인합니다.
3. 해당 부분 오른쪽에 있는 [Edit]를 클릭하여 대역폭 상한 설정 페이지로 이동합니다.
4. [Bandwidth Cap] 슬라이드 버튼![](https://main.qcloudimg.com/raw/96d86bb811611dbc89c4757fb64af536.png)을 활성화합니다.
5. [+ 제한 추가] 버튼을 클릭하여 다음과 같이 설정합니다.
	1. 	제한 리전은 해당 재생 도메인 가속 지역 유형에 따라 자체적으로 판단하며, 관련 설정 규칙은 [사용 제한](#limit)을 참조하십시오.
	2. 대역폭 임계값을 입력합니다.
	3. 임계값 단위 Mbps, Gbps 또는 Tbps를 선택합니다.
6. [Save]를 클릭합니다.

![](https://main.qcloudimg.com/raw/c2d7d5c342e3e7dc81575a6baa906fc3.png)
>! 
>- 각 단위간 환산법은 1000단위입니다. 예: 1Tbps=1000Gbps, 1Gbps=1000Mbps
>- 리전 설정을 전환하면 대역폭 상한 설정이 유효하지 않게 되므로 대역폭 상한을 다시 설정해야 합니다.


## 대역폭 상한 설정 비활성화
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **재생 도메인** 또는 오른쪽에 있는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Advanced Configuration] 탭을 선택하여 [Bandwidth Cap Configuration] 부분을 확인합니다.
3. 해당 부분 오른쪽에 있는 [Edit]를 클릭하여 대역폭 상한 설정 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/4dad76e233af788367fd5753a97a01bf.png)
4. [Bandwidth Cap] 슬라이드 버튼![](https://main.qcloudimg.com/raw/a02cf62f7cf3e9c072047690a6818ac2.png)을 비활성화합니다.
5. [Save]를 클릭합니다.
