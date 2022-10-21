## 오류 설명
CLB UDP 상태 확인에서 상태 확인 결과가 리얼 서버 포트의 실제 상태와 다릅니다.

## 가능한 원인
UDP 상태 확인에서 CLB 인스턴스는 리얼 서버에 UDP 프로브 메시지를 보냅니다. PING 명령이 성공하고 응답 제한 시간 내에 ` port XX unreachable` 오류 메시지가 반환되지 않으면 리얼 서버는 정상적인 것으로 간주됩니다. 그렇지 않으면 리얼 서버가 비정상으로 간주됩니다.

이 오류에는 두 가지 가능한 원인이 있습니다.
- 응답 제한 시간이 너무 짧아서 리얼 서버가 ICMP 메시지 `reply` 또는 `port unreachable`을 상태 확인 노드에 반환하여 부정확한 상태 확인 결과를 초래합니다.
- 리얼 서버는 ICMP 메시지가 생성되는 속도를 제한합니다. 이 경우 서비스 예외가 발생하면 `port XX unreachable` 오류 메시지를 반환할 수 없으며 CLB 인스턴스는 ICMP 응답을 받지 못하므로 상태 확인이 성공한 것으로 간주합니다. 따라서 상태 확인 결과는 리얼 서버 상태와 일치하지 않습니다.

## 처리 단계
1. 응답 제한 시간이 너무 짧은지 확인하십시오. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 UDP 리스너의 제한 시간을 늘립니다. 자세한 내용은 [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518)를 참고하십시오.
>? UDP 상태 확인은 다른 상태 확인과 다릅니다. 상태 확인 제한 시간이 너무 짧으면 상태 확인 결과가 정상과 비정상 간에 전환됩니다.
2. 오류가 지속되면 리얼 서버가 ICMP 메시지의 빈도를 제한하는지 확인하십시오. 리얼 서버에 로그인하고 다음 명령어를 실행하여 속도 제한을 확인합니다.
```
sysctl -q net.ipv4.icmp_ratelimit
sysctl -q net.ipv4.icmp_ratemask
```
3. 첫번째 명령 `net.ipv4.icmp_ratelimit`의 반환 값이 0인지 1000(기본값)인지 확인합니다. 기본값 1000을 사용하는 것이 좋습니다.
4. 오류가 지속되면 다음 명령을 실행하여 ICMP `port unreachable` 메시지의 속도 제한을 비활성화합니다.
>!ICMP `port unreachable` 메시지의 속도 제한이 해제되면 리얼 서버가 공중망에 연결되어 UDP 포트 스캐닝 공격이 발생하면 `port unreachable` 메시지를 계속 반환합니다.
>
```
# 2단계의 net.ipv4.icmp_ratemask 매개변수 쿼리 결과에 따라 아래 코드 중의 “xxxx” 값을 수정합니다.
# 다음 코드에서 "xxxx"를 처음 세 자리 값은 변경하지 않고 마지막 숫자에서 8을 뺀 값으로 수정합니다(예: 6168을 6160으로, 1819를 1811로 수정).
sysctl -w net.ipv4.icmp_ratemask=xxxx
```


