## 개요
인스턴스 자체 점검 CVM 인스턴스의 성능, 비용, 네트워크, 디스크 등 상태를 점검하고 인스턴스의 실행 상태를 이해하는 데 도움이 될 수 있습니다. 이 기능을 사용하여 즉각 인스턴스 관련 문제를 발견하고 해결할 수 있습니다.

## 시나리오
인스턴스 자체 점검을 사용하려면 다음 두 가지 시나리오를 추천합니다.
- 장애 처리: 인스턴스 작업 프로세스 중 장애 또는 문제가 발생하면 인스턴스 자체 점검을 사용하여 문제를 해결하고 추적하고 해당 제안에 따라 이상 상황을 처리할 수 있습니다.
- 인스턴스의 포괄적인 점검: 일상적인 실행 프로세스 중, 인스턴스 자체 점검을 사용하여 인스턴스의 전체 실행 상태를 이해하고 즉각 문제를 찾아 해결하여 비즈니스의 정상적인 실행을 보장할 수 있습니다.

## 점검 항목 설명
인스턴스 자체 점검 항목의 설명은 다음과 같습니다.

<dx-accordion>
::: 로컬 네트워크 점검
<table>
<tr><th style="
    width: 18%;
">점검 항목</th><th style="
    width: 35%;
">점검 설명</th><th style="
    width: 8%;
">리스크<br>레벨</th><th style="
    width: 39%;
">솔루션</th></tr>
<tr>
<td>네트워크 딜레이</td>
<td>HTTP 요청 전송을 통해 인스턴스 네트워크 딜레이가 높은지 점검합니다. 기준은 다음과 같습니다.
<ul style="margin-bottom:0px">
<li>600ms 이상이면 네트워크 연결 상태가 좋지 않은 것으로 판단</li>
<li>5s 이상 응답이 없으면 요청이 시간 초과된 것으로 간주</li>
<li>모든 요청에 시간이 초과되면 네트워크 장애로 판단 </li>
</ul>
</td>
<td>이상</td>
<td rowspan=4>로컬 네트워크 문제를 확인하고 구체적인 문제를 수정하십시오.</td>
</tr>
<tr>
<td>네트워크 지터</td>
<td>인접한 요청 간의 딜레이 값 차이를 구하고 평균값이 네트워크 지터 값입니다. 네트워크 지터 값/네트워크 딜레이 값이 0.15보다 작거나 같으면 네트워크가 안정적이고 0.15 보다 크면 네트워크가 변동이 있음을 나타냅니다.
</td>
<td>-</td>
</tr>
<tr>
<td>업스트림 대역폭</td>
<td>인스턴스 업스트림 대역폭을 계산하기 위해 인스턴스에 데이터 패킷 업로드</td>
<td>-</td>
</tr>
<tr>
<td>다운스트림 대역폭</td>
<td>인스턴스에서 데이터 패킷을 다운로드하여 인스턴스의 다운스트림 대역폭 계산</td>
<td>-</td>
</tr>
</table>
:::
::: 보안 그룹 규칙 점검
<table>
<tr><th style="
    width: 18%;
">점검 항목</th><th style="
    width: 35%;
">점검 설명</th><th style="
    width: 8%;
">리스크<br>레벨</th><th style="
    width: 39%;
">솔루션</th></tr>
<tr>
<td>보안 그룹 규칙이 상용 포트의 인터넷 개방 여부</td>
<td>보안 그룹으로 인해 인바운드 TCP 프로토콜의 22, 3389 등 상용 포트 요청 금지 여부.</td>
<td>경고</td>
<td>인스턴스 보안 그룹에서 인바운드(Ingress) 규칙의 TCP 프로토콜 포트 22 요청이 금지되어 SSH 로그인이 실패할 수 있습니다. 필요한 포트를 인터넷 개방할 수 있으며, 자세한 사항은 <a href="https://intl.cloud.tencent.com/document/product/213/32369">보안 그룹 응용 사례</a>를 참고하십시오.</td>
</tr>
</table>
:::
::: 계정 요금 점검
<table>
<tr><th style="
    width: 18%;
">점검 항목</th><th style="
    width: 35%;
">점검 설명</th><th style="
    width: 8%;
">리스크<br>레벨</th><th style="
    width: 39%;
">솔루션</th></tr>
<tr>
<td rowspan=4>
CBS 만료 여부, 인스턴스와 CBS의 만료 시간 동일 여부
<td>인스턴스와 연결된 CBS 만료 여부, CBS를 읽기/쓰기 불가능 여부</td>
<td>이상</td>
<td>이 인스턴스의 CBS가 만료되었습니다. <a href="https://console.cloud.tencent.com/cvm/cbs">CBS 콘솔</a>로 이동하여 최대한 빨리 연장하십시오.</td>
</tr>
<tr>
<td>종량제 과금 인스턴스의 CBS, CBS 만료로 인한 CBS 사용 불가 여부</td>
<td>경고</td>
<td rowspan=2>이 인스턴스의 CBS는 자동 연장으로 설정되어 있지 않으며 CBS가 만료되어 사용할 수 없게 될 수 있습니다. <a href="https://console.cloud.tencent.com/cvm/cbs">CBS 콘솔</a>로 이동하여 CBS 자동 연장을 설정하십시오.</td>
</tr>
</table>

:::
::: 인스턴스 스토리지 점검
<table>
<tr>
<tr><th style="
    width: 18%;
">점검 항목</th><th style="
    width: 35%;
">점검 설명</th><th style="
    width: 8%;
">리스크<br>레벨</th><th style="
    width: 39%;
">솔루션</th></tr>
</tr>
<tr>
<td>CBS의 딜레이가 높은지 여부</td>
<td>IO 성능 svctm 지표 이상 여부</td>
<td>경고</td>
<td>이 인스턴스의 CBS는 딜레이가 높은 문제가 있으므로 CBS의 사용에 주의하십시오.</td>
</tr>
<tr>
<td>CBS에 IO HANG 표시 여부</td>
<td>CBS에 IO HANG 표시 여부</td>
<td>경고</td>
<td>이 인스턴스의 CBS에 IO HANG 문제가 있으므로 CBS 사용에 주의하시기 바랍니다.</td>
</tr>
<tr>
<td>시스템 디스크 inode 사용량</td>
<td>CBS의 inode 사용량 100% 도달 여부</td>
<td>경고</td>
<td rowspan=4>CBS 사용에 주의하십시오. 장애 처리는 <a href="https://intl.cloud.tencent.com/document/product/213/41974">커널 및 IO 관련 문제</a>를 참고하십시오.
</td>
</tr>
<tr>
<td>시스템 디스크 읽기 전용 여부</td>
<td>CBS가 현재 읽기 전용 상태인지 여부</td>
<td>이상</td>
</tr>
<tr>
<td>시스템 디스크 공간 사용량</td>
<td>CBS 디스크 사용량 100% 도달 여부</td>
<td>경고</td>
</tr>
<tr>
<td>디스크 파티션에 총 시간에 대한 IO 작업이 있는 시간의 백분율</td>
<td>CBS의 io_util 100% 도달 여부</td>
<td>경고</td>
</tr>
</table>
:::
::: 인스턴스 상태 점검
<table>
<tr><th style="
    width: 18%;
">점검 항목</th><th style="
    width: 35%;
">점검 설명</th><th style="
    width: 8%;
">리스크<br>레벨</th><th style="
    width: 39%;
">솔루션</th></tr>
<tr>
<td>인스턴스 종료 여부</td>
<td>현재 인스턴스의 종료 여부</td>
<td>경고</td>
<td>인스턴스가 종료되었습니다. <a href="https://console.cloud.tencent.com/cvm/index">CVM 콘솔</a>로 이동하여 시작할 수 있습니다.</td>
</tr>
<tr>
<td>인스턴스 재시작 여부</td>
<td>지난 12시간 동안 인스턴스 재시작 여부</td>
<td>경고</td>
<td>지난 12시간 이내에 인스턴스가 재시작되었습니다. 인스턴스의 실행 상태에 주의하시기 바랍니다.</td>
</tr>
<tr>
<td rowspan=3>인스턴스 커널 크래쉬</td>
<td>지난 12시간 동안 인스턴스에 hangtask 존재 여부</td>
<td>이상</td>
<td rowspan=3>지난 12시간 동안 인스턴스에 hangTask/panic/soft lockup이 있었습니다. 인스턴스의 실행 상태에 주의하십시오. 장애 처리는 <a href="https://intl.cloud.tencent.com/document/product/213/41974">커널 및 IO 관련 문제</a>를 참고하십시오.</td>
</tr>
<tr>
<td>최근 12시간 동안 인스턴스가 panic 상태가 되었는지 여부</td>
<td>이상</td>
</tr>
<tr>
<td>지난 12시간 동안 인스턴스에 soft lockup 존재 여부</td>
<td>이상</td>
</tr>
</table>
:::
::: 인스턴스 성능 점검
<table>
<tr><th style="
    width: 18%;
">점검 항목</th><th style="
    width: 35%;
">점검 설명</th><th style="
    width: 8%;
">리스크<br>레벨</th><th style="
    width: 39%;
">솔루션</th></tr>
<tr>
<td>CPU 사용량</td>
<td>지난 12시간 동안 인스턴스 CPU 부하가 높았는지 여부</td>
<td>경고</td>
<td rowspan=3>
비즈니스 병목 현상을 방지하려면 CPU 사용량을 확인하고 즉시 설정 변경하는 것이 좋습니다. 장애 처리는 해당 인스턴스의 운영 체제에 따라 다음 문서를 참고하십시오.
<ul style="margin:0">
<li>Windows 예시: <a href="https://intl.cloud.tencent.com/document/product/213/32405">CPU 또는 메모리 점유율이 높아 로그인 불가</a></li>
<li>Linux 참고: <a href="https://intl.cloud.tencent.com/document/product/213/32387">CPU 또는 메모리 점유율이 높아 로그인 불가</a></li>
</ul>
</td>
</tr>
<tr>
<td>메모리 사용량</td>
<td> 지난 12시간 동안 인스턴스 메모리 부하가 높았는지 여부</td>
<td>경고</td>
</tr>
<tr>
<td>기본 CPU 사용량</td>
<td>지난 12시간 동안 인스턴스 CPU 부하가 높았는지 여부</td>
<td>경고</td>
</tr>
</table>
:::
::: 인스턴스 네트워크 점검
<table>
<tr><th style="
    width: 18%;
">점검 항목</th><th style="
    width: 35%;
">점검 설명</th><th style="
    width: 8%;
">리스크<br>레벨</th><th style="
    width: 39%;
">솔루션</th></tr>
<tr>
<td>외부 네트워크 IP 연체 여부</td>
<td>외부 네트워크 IP의 연체 및 격리 여부</td>
<td>이상</td>
<td>외부 네트워크 IP는 연체로 인해 외부 네트워크 통신 불가, <a href="https://console.cloud.tencent.com/expense/recharge">과금 센터</a>로 이동하여 가능한 한 빨리 계정을 충전하여 연장하는 것이 좋습니다.</td>
</tr>
<tr>
<td>외부 네트워크 IP 유무</td>
<td>인스턴스에 외부 네트워크 IP 유무</td>
<td>경고</td>
<td>인스턴스에 외부 네트워크 IP가 없습니다. 외부 네트워크 액세스를 위해 외부 네트워크 IP가 필요한 경우, <a href="https://console.cloud.tencent.com/cvm/eip">EIP 콘솔</a>로 이동하여 EIP를 바인딩합니다.</td>
</tr>
<tr>
<td>외부 네트워크 IP가 DDOS에 의해 차단되는지 여부</td>
<td>외부 네트워크 IP가 DDOS에 의해 차단되는지 여부</td>
<td>이상</td>
<td>인스턴스의 외부 네트워크 IP가 DDOS 공격에 의해 차단되었습니다.</td>
</tr>
<tr>
<td rowspan=2>외부 네트워크 대역폭 사용률</td>
<td>지난 12시간 동안 인스턴스 외부 네트워크 Inbound 대역폭이 높았는지 여부</td>
<td>경고</td>
<td rowspan=4>비즈니스 병목 현상을 방지하려면 네트워크 사용량을 확인하는 것이 좋습니다. 장애 처리는 <a href="https://intl.cloud.tencent.com/document/product/213/32542">높은 대역폭 점유율로 인해 로그인할 수 없음</a>을 참고하십시오.</td>
</tr>
<tr>
<td>지난 12시간 동안 인스턴스 외부 네트워크 대역폭이 높았는지 여부</td>
<td>경고</td>
</tr>
<tr>
<td rowspan=2>내부 네트워크 대역폭 사용률</td>
<td>지난 12시간 동안 인스턴스 내부 네트워크 Inbound 대역폭이 높았는지 여부</td>
<td>경고</td>
</tr>
<tr>
<td>지난 12시간 동안 인스턴스 내부 네트워크 Outbound 대역폭 이 높았는지 여부</td>
<td>경고</td>
</tr>
<tr>
<td rowspan=3>패킷 손실 상황</td>
<td>지난 12시간 동안 인스턴스 속도 제한을 트리거하고 TCP 패킷 손실 존재 여부</td>
<td>경고</td>
<td rowspan=8>비즈니스 병목 현상을 방지하려면 비즈니스 상태를 확인하는 것이 좋습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/41952">CVM 네트워크 액세스 패킷 손실</a>을 참고하십시오.</td>
</tr>
<tr>
<td>지난 12시간 동안 인스턴스 속도 제한 트리거로 인한 UDP 패킷 손실 존재 여부</td>
<td>경고</td>
</tr>
<tr>
<td>인스턴스가 지난 12시간 동안 소프트웨어 인터럽트 패킷 손실 트리거 여부</td>
<td>경고</td>
</tr>
<tr>
<td rowspan=4>커널 네트워크 사용량</td>
<td>지난 12시간 동안 인스턴스 UDP 전송 버퍼가 가득 찼는지 여부</td>
<td>경고</td>
</tr>
<tr>
<td>지난 12시간 동안 인스턴스 UDP 수신 버퍼가 가득 찼는지 여부</td>
<td>경고</td>
</tr>
<tr>
<td>지난 12시간 동안 인스턴스 TCP 전체 연결 큐가 가득 찼는지 여부</td>
<td>경고</td>
</tr>
<tr>
<td>지난 12시간 동안 인스턴스 TCP 요청 오버플로우 유무</td>
<td>경고</td>
</tr>
<tr>
<td>연결 수 사용량</td>
<td>지난 12시간 동안 인스턴스 연결 수 최댓값 도달 여부</td>
<td>경고</td>
</tr>
</table>

:::
</dx-accordion>




## 관련 작업
[인스턴스 자체 점검 사용](https://intl.cloud.tencent.com/document/product/213/45275)을 참고하여 인스턴스 점검 결과 보고서를 생성하거나 점검 이력 보고서를 조회할 수 있습니다.

