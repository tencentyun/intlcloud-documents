CLB는 정상적으로 실행되는 리얼 서버 인스턴스로 요청을 라우팅합니다. 본문은 필요에 따라 또는 CLB를 처음 사용할 때 리얼 서버를 추가하거나 삭제하는 방법에 대해 설명합니다.

## 전제 조건
CLB 인스턴스를 생성하고 리스너를 구성했습니다. 자세한 내용은 [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975)를 참고하십시오.
## 작업 단계
### CLB에 리얼 서버 추가
>?
>- CLB 인스턴스가 Auto Scaling 그룹과 연결되어 있으면 해당 그룹의 CVM이 CLB의 리얼 서버에 자동으로 추가됩니다. CVM 인스턴스가 Auto Scaling 그룹에서 제거되면 CLB의 리얼 서버에서 자동으로 삭제됩니다.
>- API를 사용하여 리얼 서버를 추가하는 방법에 대한 자세한 내용은 [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/api/214/1265)를 참고하십시오.
>- CVM별 청구 계정이 있고 비 BGP ISP(China Mobile/China Unicom/China Telecom)를 선택한 경우, 트래픽별 청구 및 대역폭별 청구 패키지 CVM 인스턴스만 바인딩할 수 있습니다. 계정 및 ISP 유형에 대한 자세한 내용은 [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246) 및 [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)을 참고하십시오.
>
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
2. ‘인스턴스 관리’ 페이지에서 ‘CLB’ 인스턴스의 오른쪽에 있는 **리스너 구성**을 클릭합니다.
3. 리스너 구성 페이지에서 백엔드 CVM에 바인딩할 리스너를 선택합니다.
 - **HTTP/HTTPS 리스너**[](id:http)
	 1. HTTP/HTTPS 리스너 섹션에서 선택한 리스너 왼쪽의 +를 클릭합니다.
	 ![](https://main.qcloudimg.com/raw/5c123efc112957e25f51ab2f8a753063.png)
	 2. 펼쳐진 도메인 이름의 왼쪽에 있는 +를 클릭합니다.
	 ![](https://main.qcloudimg.com/raw/816b003603e735d3d4f21e8891d9e279.png)
	 3. 펼쳐진 URL 경로를 선택하고 **바인딩**을 클릭합니다.
![](https://main.qcloudimg.com/raw/05f2041acaced53d2ae8bc24a2f0662b.png)
 - **TCP/UDP/TCP SSL 리스너**
TCP/UDP/TCP SSL 리스너 섹션 왼쪽의 목록에서 백엔드 CVM과 바인딩할 리스너를 선택하여 **바인딩**을 클릭합니다.
![](https://main.qcloudimg.com/raw/7dc44fc32104e533b512ab6c0b616e21.png)
4. CLB 인스턴스를 리얼 서버와 바인딩합니다.[](id:CLB)
	- **방법1**: ‘리얼 서버와 바인딩’ 대화 상자에서 **CVM**을 클릭하고 CVM 인스턴스를 하나 이상 선택하고 포워딩 포트와 가중치를 입력하고 **확인**을 클릭합니다. 포트에 대한 자세한 내용은 [서버 상용 포트](https://intl.cloud.tencent.com/document/product/213/12451)를 참고하십시오.
>?
>- ‘리얼 서버와 바인딩’ 팝업 창에는 동일한 리전, 동일한 네트워크 환경에서 격리되거나 만료되지 않고 최대 대역폭이 0보다 큰 사용 가능한 CVM만 표시됩니다.
>- CLB 인스턴스가 여러 리얼 서버와 바인딩될 때 Hash 알고리즘을 사용하여 트래픽을 포워딩합니다.
>- 가중치가 클수록 요청이 더 많이 포워딩됩니다. 값 범위는 0 - 100(기본값: 10)입니다. 0으로 설정하면 리얼 서버는 새 요청 수신을 중지합니다. 세션 지속성을 활성화하면 리얼 서버의 요청이 고르게 분산되지 않을 수 있습니다. 자세한 내용은 [Load Balancing Algorithm Selection and Weight Configuration Examples](https://intl.cloud.tencent.com/document/product/214/5371)를 참고하십시오.
>
 ![](https://main.qcloudimg.com/raw/a7f71557ff1812f777c9e989b916049f.png)
	- **방법2**: 일괄 바인딩해야 하는 CVM 인스턴스의 사전 설정 포트 값이 동일한 경우 ‘리얼 서버와 바인딩’ 팝업 대화 상자에서 **CVM**을 클릭하고 포트 값을 입력하고 해당 CVM 인스턴스를 선택하고 가중치를 설정한 다음 **확인**을 클릭하여 일괄로 바인딩합니다. 포트에 대한 자세한 내용은 [서버 상용 포트](https://intl.cloud.tencent.com/document/product/213/12451)를 참고하십시오.
![](https://main.qcloudimg.com/raw/118bfbab842d72e990d9ffe08c6379ff.png)



### CLB의 리얼 서버 가중치 수정
리얼 서버 가중치는 포워딩할 CVM 요청 수를 결정합니다. 리얼 서버를 바인딩할 때 가중치를 미리 설정해야 합니다. 다음은 ‘HTTP/HTTPS 리스너’(TCP/UDP/TCP SSL 리스너에도 적용됨)를 사용할 때 리얼 서버 가중치를 변경하는 예를 보여줍니다.
>?
>- API로 리얼 서버 가중치를 수정하는 방법에 대한 자세한 내용은 [ModifyLoadBalancerBackends](https://intl.cloud.tencent.com/document/api/214/1264)를 참고하십시오.
>- 부하 분산 리얼 서버의 가중치에 대한 자세한 내용은 [CLB Round-Robin Methods](https://intl.cloud.tencent.com/document/product/214/6153)를 참고하십시오.
>
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
2. ‘인스턴스 관리’ 페이지에서 ‘CLB’ 인스턴스의 오른쪽에 있는 **리스너 구성**을 클릭합니다.
3. HTTP/HTTPS 리스너 섹션 왼쪽의 목록에서 펼치기 아이콘을 클릭하여 인스턴스 및 리스너 규칙을 표시하고 URL을 선택합니다.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
4. HTTP/HTTPS 리스너 섹션 오른쪽의 서버 목록에서 해당 서버 가중치를 수정합니다.
>?가중치가 클수록 요청이 더 많이 포워딩됩니다. 값 범위는 0 - 100(기본값: 10)입니다. 0으로 설정하면 리얼 서버는 새 요청 수신을 중지합니다. 세션 지속성을 활성화하면 리얼 서버의 요청이 고르게 분산되지 않을 수 있습니다. 자세한 내용은 [Load Balancing Algorithm Selection and Weight Configuration Examples](https://intl.cloud.tencent.com/document/product/214/5371)를 참고하십시오.
>
	- **방법1**: 단일 백엔드 CVM의 가중치 수정
		1. 수정하려는 CVM 인스턴스를 찾아 해당 가중치 위에 마우스를 놓고 <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;"> 편집 버튼을 클릭합니다.
		![](https://main.qcloudimg.com/raw/519a69a1fab550879e92cdfc159a8fa1.png)
		2. ‘가중치 수정’ 팝업 창에서 새 가중치를 입력하고 **제출**을 클릭합니다.
	- **방법2**: 여러 백엔드 CVM의 가중치를 수정합니다.
>?일괄 수정을 수행한 후 백엔드 CVM은 동일한 가중치를 사용합니다.
>
		1. 편집하려는 CVM 인스턴스 앞의 체크 박스를 클릭하고 **가중치 수정**을 클릭합니다.
		![](https://main.qcloudimg.com/raw/09fdd5cb7a49f80bdc088632d7249f1e.png)
		2. ‘가중치 수정’ 팝업 창에서 새 가중치를 입력하고 **제출**을 클릭합니다.



### CLB용 리얼 서버 포트 수정
CLB 콘솔에서 리얼 서버 포트를 수정할 수 있습니다. 다음은 ‘HTTP/HTTPS 리스너’(TCP/UDP/TCP SSL 리스너에도 적용됨)를 사용할 때 리얼 서버 포트를 변경하는 예시를 보여줍니다.
>?API로 리얼 서버 포트를 수정하는 방법에 대한 자세한 내용은 [ModifyTargetPort](https://intl.cloud.tencent.com/document/product/214/33812)를 참고하십시오.
>
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
2. ‘인스턴스 관리’ 페이지에서 ‘CLB’ 인스턴스의 오른쪽에 있는 **리스너 구성**을 클릭합니다.
3. HTTP/HTTPS 리스너 섹션 왼쪽의 목록에서 펼치기 아이콘을 클릭하여 인스턴스 및 리스너 규칙을 표시하고 URL을 선택합니다.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
4. HTTP/HTTPS 리스너 섹션의 오른쪽 목록에서 해당 서버 포트를 수정합니다. 포트 선택 방법에 대한 자세한 내용은 [서버 상용 포트](https://intl.cloud.tencent.com/document/product/213/12451)를 참고하십시오.
	- **방법1**: 단일 백엔드 CVM의 포트 수정
		1. 수정하려는 CVM 인스턴스를 찾아 해당 포트 위에 마우스를 놓고 <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;"> 편집 버튼을 클릭합니다.
		![](https://main.qcloudimg.com/raw/923c439bedc4af2e6129d8ada459a1c5.png)
		2. ‘포트 수정’ 팝업 창에서 새 포트 값을 입력하고 **제출**을 클릭합니다.
	- **방법2**: 여러 백엔드 CVM 포트 일괄 수정.
>?일괄 수정을 수행한 후 백엔드 CVM은 동일한 포트를 사용합니다.
>
	1. 편집하려는 CVM 인스턴스 앞의 체크 박스를 클릭하고 **포트 수정**을 클릭합니다.
	![](https://main.qcloudimg.com/raw/07d40e5fcf1111a9141be83e41f67797.png)
	2. ‘포트 수정’ 팝업 창에서 새 포트 값을 입력하고 **제출**을 클릭합니다.



### CLB에서 리얼 서버 바인딩 해제
CLB 콘솔에서 바인딩된 리얼 서버를 바인딩 해제할 수 있습니다. 다음은 ‘HTTP/HTTPS 리스너’(TCP/UDP/TCP SSL 리스너에도 적용됨)를 사용할 때 리얼 서버의 바인딩을 해제하는 방법의 예시를 보여줍니다.
>?
>- 리얼 서버를 바인딩 해제하면 CVM 인스턴스에서 CLB 인스턴스가 바인딩 해제되고 CLB는 즉시 해당 서버에 대한 요청 포워딩을 중지합니다.
>- 리얼 서버의 바인딩을 해제해도 CVM 인스턴스의 라이프사이클에는 영향을 미치지 않으며 리얼 서버 클러스터에 다시 추가될 수도 있습니다.
>- API를 사용하여 리얼 서버의 바인딩을 해제하는 방법에 대한 자세한 내용은 [DeregisterTargets](https://intl.cloud.tencent.com/document/product/214/33832)를 참고하십시오.
>
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
2. ‘인스턴스 관리’ 페이지에서 ‘CLB’ 인스턴스의 오른쪽에 있는 **리스너 구성**을 클릭합니다.
4. HTTP/HTTPS 리스너 섹션 왼쪽의 목록에서 펼치기 아이콘을 클릭하여 인스턴스 및 리스너 규칙을 표시하고 URL을 선택합니다.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. HTTP/HTTPS 리스너 섹션의 오른쪽 목록에서 바인딩된 리얼 서버의 바인딩을 해제합니다.
	- **방법1**: 단일 백엔드 CVM을 바인딩 해제합니다.
		1. 대상 CVM 인스턴스를 선택하고 **바인딩 해제**를 클릭합니다.
		![](https://main.qcloudimg.com/raw/c995daabbf0b6a710b21389b17b7760b.png)
		2. ‘바인딩 해제’ 팝업 창에서 선택한 CVM 인스턴스를 확인하고 **제출**을 클릭합니다.
	- **방법2**: 여러 백엔드 CVM을 바인딩 해제합니다.
		1. 바인딩 해제하려는 CVM 인스턴스 앞의 확인란을 클릭하고 **바인딩 해제**를 클릭합니다.
		![](https://main.qcloudimg.com/raw/b397ef434ce42cfaa9a48b9f4f08f09f.png)
		2. ‘바인딩 해제’ 팝업 창에서 선택한 CVM 인스턴스를 확인하고 **제출**을 클릭합니다.

