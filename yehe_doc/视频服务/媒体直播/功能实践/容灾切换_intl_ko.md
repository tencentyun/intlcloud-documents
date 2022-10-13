StreamLive는 중복성을 제공하고 장애 조치를 지원하여 라이브 스트림 소스의 안정성을 보장합니다. 장애 조치를 구성하려면 아래 단계를 따르십시오.

1. 채널 관리 페이지에서 채널 생성을 클릭합니다. 기존 채널에 대한 입력 장애 조치를 구성하려면 편집을 클릭하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/2299ba64984e13565781af9235aeb430.png)

2. **Input Setting** 단계에서 **Input**을 추가합니다. 장애 조치(Failover)에 사용되는 백업 입력은 기본 **Input Type**과 동일한 유형이어야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d05b8b563e4a124e0fbd09514c9ae290.png)

3. 장애 조치를 구성할 **Input**을 찾고 **Setting**을 클릭하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/9bec3699f616ac1ee76472728a46b557.png)

4. **Input Failover**를 활성화하면 옵션 설정으로 자동 전환됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2b28b7c0495c2718358b2f7823603b9a.png)
현재 Channel에 바인딩된 Input에서 백업 입력(**Backup Input**)을 선택합니다. 시스템이 백업 입력으로 전환되기 전에 기본 입력의 데이터가 없을 때 대기하는 시간(ms)을 나타내는 가동 중지 시간 임계값을 지정합니다. 이 값을 3000으로 설정하는 것이 좋습니다. 가동 중지 시간 임계값이 낮을수록 장애 조치가 빨라집니다. 그러나 다운타임 임계값이 낮다는 것은 일시적인 패킷 손실로 인해 입력이 자주 전환될 수 있음을 의미합니다. 마지막으로 기본 입력이 복구된 후 시스템에서 수행할 작업을 지정합니다. **CURRENT_PREFERRED**를 선택하면 시스템은 현재 입력을 계속 사용합니다. **PRIMARY_PREFERRED**를 선택하면 백업이 현재 사용 중인 경우 시스템이 기본 입력으로 다시 전환합니다.

5. **Confirm**을 클릭하여 **Input 설정** 페이지로 돌아갑니다. 이제 두 Input의 바인딩 상태가 각각 기본 및 백업임을 알 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a9b76c8ce82c4cea993e8edf858aa646.png)
이제 Input 장애 조치를 구성했으며 채널에 대한 Output을 계속 구성할 수 있습니다. 자세한 지침은 Channel 관리 4단계 출력 그룹 구성을 참고하십시오.

