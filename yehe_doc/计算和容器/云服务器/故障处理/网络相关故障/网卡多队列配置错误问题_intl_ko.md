## 현상 설명
CVM ENI의 다중 큐 설정에 오류가 발생합니다.

## 예상 원인
기본적으로 CVM은 ENI에 대한 여러 큐로 설정되며 이 방법은 ENI 중단을 서로 다른 CPU에 분산하여 네트워크 처리 성능을 향상시킬 수 있습니다. 수정 시 ENI의 다중 큐 설정에 오류가 발생할 수 있습니다.

## 해결 방법
[처리 단계](#ProcessingSteps)를 참고하여 ENI 큐 수를 수정합니다.


## 처리 단계[](id:ProcessingSteps)
다음 단계에서 CVM의 기본 주 ENI는 'eth0'이고 ENI 큐의 수는 2입니다.
1. 다음 명령을 실행하여 현재 ENI 큐 수를 확인합니다.
```
ethtool -l eth0
```
다음 결과가 반환되면, 현재 큐 수가 최대 ENI 큐 수보다 작게 설정되어 있는 것입니다. 설정이 비합리적이므로 수정이 필요합니다.
```
Channel parameters for eth0:
Pre-set maximums:
RX:             0
TX:             0
Other:          0
Combined:       2         ### 서버에서 지원하는 최대 ENI 큐 수
Current hardware settings:
RX:             0
TX:             0
Other:          0
Combined:       1        ###현재 설정된 ENI 큐 수
```
2. 다음 명령을 실행하여 현재 ENI 큐 수를 설정합니다.
```
ethtool -L eth0  combined 2
```
명령어의 큐 개수는 2로 설정하며, 실제 상황에 따라 조정할 수 있습니다. 설정값은 서버에서 지원하는 ENI 큐의 최대 개수입니다.
2. 다음 명령을 실행하여 ENI 큐 수의 현재 설정을 확인합니다.
```
ethtool -l eth
```
서버에서 지원하는 최대 ENI 큐 수는 현재 설정된 ENI 큐 수와 같으므로 설정이 완료됩니다.
