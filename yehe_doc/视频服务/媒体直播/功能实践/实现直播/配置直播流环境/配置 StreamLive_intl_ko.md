[StreamLive 콘솔](https://console.tencentcloud.com/mdl/input)로 이동합니다. 왼쪽 사이드바에는 4개의 섹션이 표시됩니다.
● 보안 그룹 관리 Security Group Management.
● 입력 관리 Input Management.
● 채널 관리 Channel Management.
● 워터마크 관리 Watermark Management.
보안 그룹, 입력 및 채널(필수)과 워터마크(선택)를 구성하는 방법을 보여줍니다.

1. 왼쪽 사이드바에서 **Security Group Management**를 선택하고 **Create Security Group**을 클릭합니다. 팝업 창에서 보안 그룹 이름을 입력하고 IP 얼로우리스트를 지정합니다. IP 주소는 CIDR 형식이어야 합니다. 쉼표 또는 줄 바꿈으로 주소를 구분합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/46e60d979177b96851cb16dc890d6890.png)

2. 왼쪽 사이드바에서 **Input Management**를 선택하고 **Create Input**을 클릭한 후 팝업 창에서 설정을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8041139ea24469f261f31ebb1077f406.png)
- **Type**: 스트리밍 프로토콜입니다. 이 예시에서는 RTMP_PUSH를 선택합니다.
- **Security Group**: 연결할 보안 그룹입니다. 생성된 보안 그룹을 드롭다운 목록에서 선택합니다.
- **Destination**: 푸시 대상입니다. **AppName** 및 **StreamName**을 하나 이상 입력하십시오. 중복성을 제공하도록 두 개의 대상을 구성할 수 있습니다.

3. **Confirm**을 클릭합니다. **Input** 목록에서 생성한 Input을 찾아 세부 정보 페이지로 들어갑니다. 나중에 사용할 수 있도록 푸시 **Destination**을 기록해 둡니다.

4. 왼쪽 사이드바에서 **Channel Management**를 클릭하고 **Create Channel**을 클릭합니다. **Basic Information** 단계에서 채널 이름을 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dda466604218ebfd491cfbb0dd681fb0.png)

5. **Input Setting** 단계에서 방금 생성한 **Input**을 추가합니다(여러 Input을 추가할 수 있으며 다른 트랜스코딩 템플릿 및 출력을 구성할 수 있음).
![](https://qcloudimg.tencent-cloud.cn/raw/55c4b71f066c7e18804d029c30da04b1.png)

6. **Output Group Setting** 단계에서 채널에 대한 트랜스코딩 템플릿 및 출력을 구성합니다.
- 기본 정보에서 **Output Group** 이름을 입력하고 출력 그룹 유형을 선택합니다(2개의 프로토콜과 3개의 출력 유형이 지원됨). **Destination Information** 영역에 이전에 기록한 **StreamPackage Channel ID**를 입력합니다. 이를 통해 실시간 스트림에 대한 트랜스코딩 및 패키징을 빠르게 구현할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/04e6469dc287247e50bf0ff198b04c78.png)
- 이 페이지에서 세그먼트 유형, 세그먼트 기간 및 세그먼트 번호를 포함하여 **Segment Information**을 지정할 수도 있습니다. AppleTV와 같은 일부 장치의 경우 H.265로 인코딩된 비디오를 재생하려면 Segment Type으로 fmp4를 선택하고 Packing Type으로 hvc1을 선택해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/407322c8d120feec4f2fab998f33e4a6.png)

7. 템플릿 정보 영역까지 아래로 스크롤하여 트랜스코딩 템플릿을 구성합니다. 오디오 및 비디오에 대한 공동 트랜스코딩 템플릿 또는 별도의 트랜스코딩 템플릿을 구성할 수 있습니다. 다중 비트 레이트 출력도 지원됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1f0b9aa788821031bb573eb52d07bbef.png)

8. 출력 영역에서 각 출력의 이름을 입력하고 사용할 트랜스코딩 템플릿을 선택합니다. 완료를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/405e9167353c870d5f687bbc7ce8ecc1.png)

9. 채널 목록으로 돌아가서 **Operation** 열에서 **Start**를 클릭하여 채널을 시작합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7391eea01e3b76709be2a36f309a3f5a.png)