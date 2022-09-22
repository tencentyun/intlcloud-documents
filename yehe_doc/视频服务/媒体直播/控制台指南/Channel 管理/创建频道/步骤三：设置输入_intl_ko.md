Input List는 바인딩된 Input을 보여줍니다. **Setting**을 클릭하여 Input을 구성할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ab177f714962ce78c8c311a5e5d189c9.png)

## 오디오 셀렉터
RTP/UDP PUSH 입력의 경우 MPEGF-TS를 사용하는 경우 여러 오디오 트랙이 있을 수 있습니다. **Pid**를 입력하여 처리 및 출력할 오디오 트랙을 지정할 수 있습니다. 설정하지 않으면 오디오 트랙이 무작위로 선택됩니다. 오디오 셀렉터의 이름은 채널 전체에서 고유해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b82435f92e7a7081c1d80d7453729f76.png)

>! 
>- 입력한 PID가 소스 스트림의 PID와 동일한지 확인하십시오. 그렇지 않으면 오디오 셀렉터가 작동하지 않고 시스템이 출력할 오디오 트랙을 무작위로 선택합니다.
>- 입력 장애 조치(Failover)가 활성화된 경우 기본 입력에 대해 구성된 오디오 Selector가 백업 입력에도 적용됩니다.

## 풀 스트림 동작 설정
PULL 입력의 **Source End Behavior**를 설정하여 입력의 유효 시간을 제어할 수 있습니다:
- **LOOP**: 종료 후 입력을 다시 풀링합니다.
- **ONCE**: 입력을 한 번만 풀링합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/cb9adca89713d48324c87a4244a96eee.png)


## 장애 조치(Failover)
입력 예외로 인한 서비스 중단을 방지하기 위해 RTMP_PUSH/RTP_PUSH 입력에 대한 장애 조치를 활성화할 수 있습니다. 기본 입력이 다운되면 StreamLive는 자동으로 백업 입력으로 전환합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/83713e5b3dc6269d86d7f1972847bf04.png)

- **Input Failover**: Input에 대해 **Input Failover**를 활성화하려면 이 옵션을 켜십시오.
- **Select Backup Input**: 유형이 기본 Input과 동일해야 하는 백업 Input을 선택합니다.
- **Downtime Threshold**: 장애 조치를 위한 대기 시간(밀리초)을 설정합니다. 기본 입력이 중단된 경우 StreamLive는 대기 시간이 경과한 후 데이터 가용성을 보장하기 위해 백업 입력으로 전환합니다. 기본값은 3,000밀리초입니다.
- **Input Preference**: 복구 후 기본 입력으로의 재전환 여부를 설정합니다. CURRENT_PREFERRED(기본값): 현재 입력을 계속 사용합니다. PRIMARY_PREFERRED: 복구된 후 기본 입력으로 재전환합니다.
- **Confirm**을 클릭합니다. Input List에서 기본 입력의 **Bind Status**가 Primary로 변경되고 백업 입력의 바인딩 상태가 Backup으로 변경된 것을 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d672160e188307359c705442e009d8f1.png)
>! 
>- 각 Input에 대해 하나의 백업만 지정할 수 있으며 기본 입력과 유형이 동일하고 파이프라인 수가 동일해야 합니다.
>- Input이 Backup으로 사용되면 자동으로 입력에 대해 Failover 기능이 비활성화되므로 이 Input에 대한 백업을 구성할 수 없습니다. 두 Input의 기본 및 백업 역할을 변경하려면 먼저 기본 Input에 대한 Failover를 비활성화해야 합니다.
>- 구성에 성공하면 기본 및 백업 입력 이름 옆에 ‘Primary’ 및 ‘Backup’이 나타납니다.
>- input list에서 백업 입력은 기본 입력 아래에 나타납니다.


## 다른 작업
- **Details**: Input의 소스 주소 및 기타 정보를 봅니다.
- **Set as First**: Input을 기본값으로 설정합니다. 입력이 목록의 맨 위로 이동됩니다. 백업 입력은 기본값으로 설정할 수 없습니다.
- **Delete**: 입력을 삭제합니다.
- **Next**: 다음 단계로 진행하고 출력을 구성합니다.


