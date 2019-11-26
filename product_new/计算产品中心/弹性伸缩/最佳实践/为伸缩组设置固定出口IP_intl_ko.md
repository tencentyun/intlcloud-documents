이 페이지는 클러스터가 액티브 외부 액세스를 해야 하는 경우 고정 외부 액세스 IP를 설정하는 방법에 대해 설명합니다.

## 시나리오 요구 사항

스케일링 그룹의 클러스터에 세 가지 요구 사항이 동시에 존재할 경우:
- Cloud Load Balancer CLB의 요청을 수락합니다.
- 클러스터 기기는 액티브 외부 액세스가 필요합니다.
- 외부 액세스할 때 **고정**된 공용 IP를 사용을 권장합니다.

사용자는 아래 솔루션에 따라 설정하면 됩니다.

## 솔루션 요약
1. Cloud Load Balancer CLB를 통해 외부 요청을 수락하고 응답합니다.
2. VPC의 서브넷에 기기를 배치하고 라우팅 테이블을 NAT 게이트웨이로 가리키며, 액티브 외부 액세스 요청은 모두 NAT 게이트웨이의 공용 IP를 통해 전송됩니다.
3. 스케일링 그룹의 네트워크 속성은 서브넷으로 설정되어 있으며, 이렇게 확장된 기기는 모두 NAT 게이트웨이를 사용하여 액티브 외부 액세스를 실행합니다.

다음 이미지 참고:

![](https://main.qcloudimg.com/raw/04d27325ce883c3b8ac8e1a604c7aad7.png)



## 설정 방법

### 1단계: VPC 및 서브넷 생성

#### **1. VPC 생성**

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 사이드바의 [Virtual Private Cloud]를 클릭 또는 Tencent Cloud [Virtual Private Cloud 소개 페이지](https://cloud.tencent.com/product/vpc.html)의 [즉시 체험]을 클릭하면 [Virtual Private Cloud 콘솔](https://console.cloud.tencent.com/vpc/)로 이동합니다.

2. 목록 위의 드롭다운 리스트에서 리전을 선택하고 [생성]을 클릭하면 Virtual Private Cloud가 생성됩니다. 예를 들면 "화북지역(베이징)"을 리전으로 선택합니다.

3. Virtual Private Cloud 및 서브넷의 이름과 CIDR을 입력하고 서브넷의 가용 영역을 선택하십시오.

4. [생성]을 클릭하십시오.


#### **2. 서브넷 생성**

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 사이드바의 [Virtual Private Cloud]를 클릭한 후 왼쪽 사이드바에서 [서브넷]을 클릭하십시오. 드롭다운 리스트에서 리전 및 Virtual Private Cloud를 선택하십시오.
![2](https://main.qcloudimg.com/raw/8c04a129eabe941ad8ef9758347e028f.png)



2. [신규]를 클릭하여 서브넷 이름, CIDR, 가용 영역 및 관련 라우팅 테이블을 입력합니다. 그리고 [생성]을 클릭하여 확인하십시오.

3. 생성 완료 후 기기를 구매하고 이 서브넷에 들어갈 수 있습니다.


### 2단계: NAT 게이트웨이 생성
#### **1. 구매**
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 [Virtual Private Cloud] 탭을 선택한 후 [NAT 게이트웨이]를 선택하십시오.

2. 왼쪽 상단에서 [생성] 버튼을 클릭하고 팝업 상자에서 다음 파라미터를 입력하고 확인하십시오.
	- 게이트웨이 이름
	- 게이트웨이 유형(게이트웨이 유형은 생성 후 변경 가능)
	- NAT 게이트웨이 서비스의 Virtual Private Cloud(즉, 방금 생성한 Virtual Private Cloud)
	- NAT 게이트웨이를 위해 EIP를 할당하고, 해당 IP는 향후 기기 외부 액세스의 고정 IP입니다.

3. 선택 완료 후 [확인] 버튼을 클릭하여 NAT 게이트웨이 생성을 완료하십시오.

4. NAT 게이트웨이를 생성한 후 Virtual Private Cloud 콘솔 라우팅 테이블 페이지에서 서브넷 트래픽을 NAT 게이트웨이로 가리키도록 라우팅 규칙을 구성해야 합니다.

#### **2. 라우팅 테이블 설정(중요 사항)**
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 사이드바의 [Virtual Private Cloud]를 클릭하여 [Virtual Private Cloud 콘솔] (https://console.cloud.tencent.com/vpc/vpc?rid=8)로 들어가서 [라우팅 테이블]을 선택하십시오.

2. 라우팅 테이블 목록에서 Internet에 액세스할 서브넷과 연결된 라우팅 테이블 ID를 클릭하여 라우팅 테이블 세부 정보 페이지에 진입하고, 라우팅 정책에서 [편집] 버튼을 클릭하십시오.

3. 한 줄 추가를 클릭하여 목적 단말기(예 :이 환경에서 0.0.0.0/0을 입력할 수 있음)를 입력 후 다음 단계 유형에서 [NAT 게이트웨이]를 선택하고 생성된 NAT 게이트웨이 ID를 선택한 다음 확인을 클릭합니다.
![3](https://main.qcloudimg.com/raw/e5029e42a6570c26814375f2264a7f4b.png)


이로써 서브넷에 있는 기기는 공용 네트워크 IP가 없어도 NAT 게이트웨이를 통해 액티브 외부 액세스할 수 있으며 대외적으로 여전히 고정 IP입니다.

아래 그림과 같이 공용 네트워크 IP 주소가 없고 대역폭이 0인 호스트를 구입한 경우에도 액티브 외부 액세스할 수 있습니다.
![4](https://mc.qcloudimg.com/static/img/17ed153e06272885b56764781d9ab581/49.jpg)

그러나 스케일링 그룹은 이 서브넷을 식별하고 기기가 모두 해당 서브넷에서 생성하도록 합니다.

### 3단계: 스케일링 그룹 설정
이 단계의 목적은 서브넷 정보를 스케일링 그룹으로 지정하는 것이며 스케일링 그룹은 새로 확장된 기기를 서브넷에서 여는 것입니다.
**이런 방식으로 용량 확장된 기기는 자동으로 NAT 게이트웨이의 IP 주소를 액세스하여 고정 출구 IP에 도달하는 효과를 볼 수 있습니다. **

[Auto Scaling 콘솔](https://console.cloud.tencent.com/autoscaling/config)에서 생성을 클릭하십시오.

- 스케일링 그룹 이름, 작동 사양(사전에 작동 사양 설정 완료), 최대 스케일링 수, 최소 스케일링 수 및 최초 용례 수 등 정보를 입력하십시오.
- "네트워크" 및 "서브넷"을 선택하여 방금 설치한 VPC 및 서브넷을 가리킵니다.**(중요 사항)**

다음 이미지 참고:
![5](https://main.qcloudimg.com/raw/f752a1ae61b9a49c97d50626f33f76da.png)


이상 설정이 완료되었습니다.
