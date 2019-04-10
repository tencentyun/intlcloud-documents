## 일반 사례
사용자 로컬 IDC는 물리적 직접 연결을 통해 전통 전용 채널을 사용하여 클라우드화합니다. 토폴로지는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/e11798e61637bc0a8d73aa60464fe0b2.png)

### VPC 라우팅 테이블 구성 조회
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com)에 로그인하고 [클라우드 제품]>[클라우드 컴퓨팅과 네트워크]>[VPC]를 선택하여 VPC 콘솔에 진입합니다.
2. 왼쪽 목록의 [라우팅 테이블]을 클릭하고 'VPC 소재 지역'을 선택한 뒤, 'VPC'를 선택하여 '라우팅 테이블 ID'를 클릭합니다. 본문은 '베이징', 'Default-VPC(172.21.0.0/16)', 'rtb-2kanpxjb'를 예로 합니다.
![](https://main.qcloudimg.com/raw/289f0d1e4568da441ac506843e35df68.png)
3. 진입하면 VPC 라우팅 테이블 구성 세부 정보를 조회할 수 있습니다. 다음 그림과 같습니다. 
![](https://main.qcloudimg.com/raw/3fa9826a367155c001eff718440da810.png)

### 전용 채널 구성 조회
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com)에 로그인하여 [DC 콘솔](https://console.cloud.tencent.com/dc/dcConn)에 진입합니다.
2. 왼쪽 목록의 [전용 채널]을 클릭한 뒤, '전용 채널 ID'를 클릭하고 세부 정보 페이지에 진입합니다. 본문은 'dcx-4xls4yx2'를 예로 합니다.
![](https://main.qcloudimg.com/raw/4d924207e0dffa832ea6822e02a3a5e6.png)
4. [고급 구성]을 클릭하면 전용 채널의 고급 구성을 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/d1c0b3a1a10fc28631e73eb41cb6d27b.png)

이상의 정보를 종합해 보면, 대상 IP 주소 범위 192.168.0.0/24를 향한 VPC의 트래픽은 VPC 라우팅 테이블 전략에 따라 직접 연결 게이트웨이 dcg-019f9l0q 경로 방향을 선택하여 발송됩니다.

## 전환 절차
1. CCN 직접 연결 게이트웨이를 생성합니다.
 1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com)에 로그인하고 [클라우드 제품]>[클라우드 컴퓨팅과 네트워크]>[VPC]를 선택하여 VPC 콘솔에 진입합니다.
 2. 왼쪽 목록의 [직접 연결 게이트웨이](https://console.cloud.tencent.com/vpc/dcGw?rid=8)를 클릭하고 [생성]을 클릭한 뒤, 직접 연결 게이트웨이 이름을 입력하고 연결 네트워크를 'CCN'으로 선택합니다. 본문은 'dcg-dx8kvqto'를 예로 하고 있습니다. 
![](https://main.qcloudimg.com/raw/3a5f479742998239283cf23fd64ee268.png)
 3. [확인]을 클릭합니다.
 
 >!생성한 CCN 직접 연결 게이트웨이의 지역은 물리적 직접 연결의 연결 액세스 포인트와 동일 지역이어야 합니다.
2. CCN 전용 채널을 생성합니다.
 1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com)에 로그인하여 [DC 콘솔](https://console.cloud.tencent.com/dc/dcConn/create)에 진입합니다.
 2. 왼쪽 목록에서 [전용 채널]을 클릭하고 [생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/aece2f4003c62d5fb3fbde0548477b90.png)
 3. 전용 채널 생성에 진입하여 '기본 구성' 페이지에서 이름을 입력한 뒤, '직접 연결 유형', '물리적 직접 연결', '액세스 네트워크', '직접 연결 게이트웨이'의 매개변수를 선택합니다. 본문은 'test'를 예로 하고 있습니다.
![](https://main.qcloudimg.com/raw/bd097cdd58f42eaa8d6daff2a9be84b3.png)
>?
>- 물리적 직접 연결은 ID가 dc-dqggvxad인 기존의 물리적 직접 연결을 사용합니다.
>- 액세스 네트워크는 CCN을 선택합니다.
>- 직접 연결 게이트웨이는 절차 1에서 생성한 CCN 직접 연결 게이트웨이, 즉 이름이 dcg-dx8kvqto인 CCN 직접 연결 게이트웨이를 선택합니다.
 4. [다음 단계]를 클릭하여 고급 구성에 진입한 뒤, 'VLAN ID'를 입력합니다. 본문은 '501'을 예로 하고 있습니다.
![](https://main.qcloudimg.com/raw/f6bb1944403b288fd48e67d924958e7c.png)
>!VLAN ID 이름은 반드시 새로운 ID여야 합니다.
 5. [다음 단계]를 클릭하여 IDC 장치 구성에 진입한 뒤, [제출]을 클릭합니다.
3. CCN 직접 연결 게이트웨이에 사용자 IDC IP 주소 범위를 추가합니다.
 1. [직접 연결 게이트웨이 콘솔](https://console.cloud.tencent.com/vpc/dcGw?rid=8)에 로그인한 뒤, 절차 1에서 생성한 CCN 직접 연결 게이트웨이 ID(이름이 '테스트 직접 연결 게이트웨이')를 선택하여 'dcg-dx8kvqto' 세부 정보 페이지에 들어간 후 [IDC IP 주소 범위], 그리고 [추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/fe57c56980c4a8775705a4bcbb76b80d.png)
 2. 추가 페이지에 들어가 IDC IP 주소 범위를 입력하고 [저장]을 클릭합니다. 본문은 '192.168.0.0/24'를 예로 하고 있습니다.
![](https://main.qcloudimg.com/raw/1e97fe05d1ea75fe965cb3be73a00f27.png)
 3. 저장에 성공하면 추가한 IDC IP 주소 범위를 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/91ee51c43216435bb57aba406d37ef44.png)
>?
>- IDC IP 주소 범위 정적 추가 뿐만 아니라 IDC IP 주소 범위 자동 학습을 선택할 수 있습니다.
>- 현재 IDC IP 주소 범위 자동 학습 대기 시간은 1분이며, 요구에 부합하지 않으면 우선 정적 추가를 선택하십시오.
4. CCN 인스턴스를 생성합니다.
 1. [CCN 콘솔](https://console.cloud.tencent.com/vpc/ccn)에 로그인한 뒤, [생성]을 클릭하여 CCN 인스턴스 이름을 입력하고 인스턴스 VPC를 연결한 뒤 [생성]을 클릭합니다. 본문은 'ccn-msg8kju5', 'vpc-gu64ju2u'를 예로 하고 있습니다.
![](https://main.qcloudimg.com/raw/08fd52950a6285af04fb4a585470e39a.png)
 2. CCN 생성이 완료되면, CCN 리스트 페이지에서 인스턴스 ID를 클릭하여 CCN 인스턴스 세부 정보 페이지에 들어갑니다. 본문은 ccn-msg8kju5를 예로 하고 있습니다.
![](https://main.qcloudimg.com/raw/be26e13c848bab9c8b1333bd16df6276.png)
 3. [라우팅 테이블]을 클릭합니다.
![](https://main.qcloudimg.com/raw/1408028fc2f22d61a5513bb94ee6a464.png)

 >?전통 전용 채널 VPC가 IDC에 발표한 것은 CIDR 큰 IP 주소 범위이고, VPC가 CCN에 발표한 것은 VPC의 서브넷입니다.
5. IDC의 VPC를 향한 트래픽 경로를 전환합니다.
 1. '테스트 CCN(ccn-msg8kju5)' 페이지에서 [인스턴스 연결]을 클릭한 뒤, [인스턴스 새로 추가]를 클릭합니다. 본문은 '직접 연결 게이트웨이', '베이징', 'dcg-dx8kvqto'를 예로 하고 있으며 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/c6db304e2186c2f18e7ea2c0e1454446.png)
 2. [제출]을 클릭하면 ID가 dcg-dx8kvqto인 인스턴스가 CCN에 연결됩니다.
![](https://main.qcloudimg.com/raw/90495973efd23bcf585869b1ab2a94b6.png)
 3. [라우팅 테이블]을 클릭합니다. CCN의 라우팅 테이블은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/9a8f62a335c1463df026c7d0ddbdad3f.png)
>?
>- 전용 채널은 정적 라우팅이며, VPC 방향으로의 IDC 트래픽을 CCN 채널 경로로 전환하려면, 사용자 CPE 라우팅을 새로운 서브 API CCN 채널로 지향하기만 하면 됩니다.
>- 전용 채널은 모두 BGP 라우팅일 경우, 클라우드 액세스 장치의 이전 채널이 IDC에 발송한 것은 CIDR 대규모 IP 주소 범위이며, 새로운 CCN 채널이 IDC에 발송한 것은 서브넷 세부 라우팅입니다. **라우팅 마스크 최장 매칭 원칙에 따라 VPC 방향을 향한 IDC 트래픽은 CCN 전용 채널로 자동 전환됩니다.**
>- CCN 내의 VPC 또는 직접 연결 게이트웨이 라우팅을 사용 금지하거나 활성화하여 VPC를 향한 IDC의 트래픽 경로를 제어할 수 있습니다.
6. VPC의 IDC를 향한 트래픽 경로를 전환합니다.
 1. ID가 rtb-2kanpxjb인 라우팅 테이블을 클릭한 뒤, [VPC 라우팅 테이블 전략 변화](https://console.cloud.tencent.com/vpc/route?rid=8)를 조회합니다. VPC는 CCN 라우팅 테이블 자동 학습 능력을 갖추고 있으며, 나중에 가입한 등가 라우팅은 기본적으로 사용하지 않습니다. IDC 방향을 향한 VPC의 트래픽 경로는 이전 전용 채널을 선택합니다.
![](https://main.qcloudimg.com/raw/369984d65c6ddf72cc874ee29ec96ace.png)
 2. 이전 직접 연결 게이트웨이의 라우팅 전략을 사용 금지하고 다음 홉이 CCN인 라우팅 전략을 사용해야 합니다.
![](https://main.qcloudimg.com/raw/c26b3b21f26e35df00c7123ab6eafe64.png)
작업이 완료되면, IDC 방향을 향한 VPC의 트래픽 경로가 CCN 전용 채널로 전환됩니다.
 
 >!사용을 금지했다 다시 사용하는 과정에서 IDC 방향을 향한 VPC의 트래픽은 중단됩니다. 비즈니스 보안을 위해 비즈니스를 중단할 수 있는 시간창을 선택하여 작업해야 합니다.

원활하게 전환해야 할 경우, 절차는 다음과 같습니다.
 a. IDC 라우팅을 두 개의 세부 라우팅으로 가릅니다. 192.168.0.0/24를 192.168.0.0/25와 192.168.0.128/25로 가릅니다.
 b. VPC 라우팅 테이블에 두 개의 세부 라우팅 전략을 추가합니다.
![](https://main.qcloudimg.com/raw/cd9b09904fd356d91d30d3aca7d1a28d.png)
 c. IDC 방향을 향한 VPC 트래픽은 25비트 마스크의 세부 라우팅 전략을 선택하게 됩니다. 이때, 대상 IP 주소 범위 192.168.0.0/24 다음 홉인 직접 연결 게이트웨이의 라우팅 전략은 이미 무효이므로 라우팅 전략을 사용 중지하거나 삭제할 수 있습니다.
 d. VPC 라우팅 테이블은 다음 홉이 CCN 대상 IP 주소 범위가 192.168.0.0/24인 라우팅 전략을 사용합니다. 이때 IDC를 향한 VPC 경로는 이전 직접 연결 게이트웨이의 세부 라우팅 전략을 계속 선택하게 됩니다.
![](https://main.qcloudimg.com/raw/8c72c7b05cd9829417038acfbc8ab980.png)
 e. VPC 라우팅 테이블은 세부 라우팅의 라우팅 전략을 점차 사용 중지하거나 삭제하고, IDC를 향한 VPC 트래픽도 CCN 채널로 점차 전환됩니다.
![](https://main.qcloudimg.com/raw/54b0dea5e4f29ae7acbc2918887ddc3c.png)

7. 채널과 직접 연결 게이트웨이를 삭제합니다.
이상의 절차를 통해 전환이 완료됩니다. 우선 일정 시간 관찰한 뒤, 네트워크가 안정되면 이전 채널과 이전 직접 연결 게이트웨이를 삭제할 수 있습니다.

