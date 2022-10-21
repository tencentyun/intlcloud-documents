## 배경
CLB에서 스트레스 테스트를 수행할 때 너무 많은 클라이언트 timewait(모든 포트가 짧은 시간에 점유됨)으로 인해 connect 실패가 발생할 수 있습니다. 원인과 솔루션은 다음과 같습니다.

## Linux 매개변수 설명
**tcp_timestamps:** tcp timestamps 활성화 여부입니다. timestamps는 tcp 3방향 핸드셰이크에서 협의됩니다. 당사자 중 하나가 이 매개변수를 지원하지 않으면 이 연결에서 사용되지 않습니다.
**tcp_tw_recycle:**  tcp time_wait 상태의 재사용 여부입니다.
**tcp_tw_reuse:** 활성화되면 1s를 초과하는 time_wait 상태의 연결을 직접 재사용할 수 있습니다.

## 원인 분석
클라이언트가 연결을 사전에 닫기 때문에 클라이언트에 너무 많은 timewait가 있습니다. 클라이언트가 연결을 닫으면 연결이 timewait 상태가 되고 기본적으로 60s 후에 다시 사용됩니다. 이 경우 `tcp_tw_recycle` 및 `tcp_tw_reuse` 매개변수를 활성화하여 timewait 상태에서 연결을 쉽게 재사용할 수 있습니다.
현재 CLB에서 `tcp_timestamps`가 비활성화되어 있으면 클라이언트에서 활성화한 `tcp_tw_recycle` 및 `tcp_tw_reuse` 매개변수가 적용되지 않으며 timewait 상태의 연결을 빠르게 재사용할 수 없습니다. 다음은 일부 Linux 매개변수와 CLB에서 `tcp_timestamps`를 활성화할 수 없는 이유를 설명합니다.
1. tcp_tw_recycle 및 tcp_tw_resuse는 tcp_timestamps가 활성화된 경우에만 적용됩니다.
2. FullNAT 시나리오에서는 공중망 클라이언트가 NAT 게이트웨이를 통해 서버에 액세스하지 못할 수 있으므로 tcp_timestamps 및 tcp_tw_recycle을 동시에 활성화할 수 없습니다. 원인은 다음과 같습니다.
tcp_tw_recycle/tcp_timestamps가 모두 활성화된 경우 동일한 원본 IP(동일 서버)의 socket connect 요청에 있는 timestamp는 60s 이내에 증분되어야 합니다. 2.6.32 커널을 예로 들면 세부 사항은 다음과 같습니다.
```
if(tmp_opt.saw_tstamp && tcp_death_row.sysctl_tw_recycle &&
(dst = inet_csk_route_req(sk,req))!= NULL &&
	(peer = rt_get_peer((struct rtable *)dst))!= NULL && 
	peer->v4daddr == saddr){
	if(get_seconds()< peer->tcp_ts_stamp + TCP_PAWS_MSL &&
		(s32)(peer->tcp_ts - req->ts_recent) > TCP_PAWS_WINDOW){
			NET_INC_STATS_BH(sock_net(sk),LINUX_MIB_PAWSPASSIVEREJECTED);
			goto ↓drop_and_release;
	}
}
```
>?tmp_opt.saw_tstamp: 이 socket은 tcp_timestamp를 지원합니다.
>sysctl_tw_recycle: 이 서버에 대해 tcp_tw_recycle이 활성화되었습니다.
>TCP_PAWS_MSL: 60s, 원본 IP의 마지막 TCP 통신이 60s 이내에 발생했습니다.
>TCP_PAWS_WINDOW: 1, 원본 IP의 마지막 tcp 통신 timestamp가 이 tcp 통신의 timestamp보다 큽니다.
>
3. CLB(레이어 7)에서는 공중망 클라이언트가 아래 예시와 같이 NAT 게이트웨이를 통해 서버에 액세스하지 못할 수 있으므로 tcp_timestamps가 비활성화됩니다.
a) 5개는 아직 time_wait 상태입니다. NAT 게이트웨이의 포트 할당 정책에서는 최대 세그먼트 수명(2MSL)의 2배에 동일한 5개를 재사용하고 syn 패킷을 전송합니다.
b) tcp_timestamps가 활성화되고 다음 두 가지 조건이 충족되면 syn 패킷이 삭제됩니다(timestamp 옵션이 활성화되어 패킷이 오래된 것으로 간주되기 때문).
i. 지난 타임스탬프 > 이번 타임스탬프입니다.
ii. 패킷은 24일 이내에 수신됩니다(타임스탬프 필드는 32비트이고 타임스탬프는 Linux에서 기본적으로 1ms당 한 번 업데이트됩니다. 타임스탬프는 24일 후에 래핑됩니다).
참고: 이 문제는 클라이언트가 ISP의 NAT 게이트웨이에서 제한된 공중망 IP를 공유하고 2MSL에서 5개를 재사용할 수 있기 때문에 모바일 장치에서 더 분명합니다. 다른 클라이언트에서 보낸 타임스탬프는 증가하지 않을 수 있습니다.
2.6.32 커널을 예로 들면 세부 사항은 다음과 같습니다.
```
static inline int tcp_paws_check(const struct tcp_options_received *rx_opt,int paws_win)
{
	if((s32)(rx_opt->ts_recent - rx_opt->rcv_tsval)<= paws_win)
	return 1;
	if(unlikely(get_seconds()>=rx_opt->ts_recent_stamp + TCP_PAWS_24DAYS))
	return 1;
	return 0;
}
```
>?rx_opt->ts_recent: 마지막 타임스탬프입니다.
>rx_opt->rcv_tsval: 이번에 수신된 타임스탬프입니다.
>get_seconds(): 현재 시간입니다.
>rx_opt->ts_recent_stamp: 이전 패킷을 수신한 시간입니다.
>

## 솔루션
클라이언트에 너무 많은 Timewait가 있는 경우 아래 솔루션을 참고하십시오.
- HTTP는 비지속 연결을 사용합니다(Connection: close). 이 경우 CLB는 사전에 연결을 닫고 클라이언트는 timewait를 생성하지 않습니다.
- 시나리오에 지속 연결이 필요한 경우 socket의 SO_LINGER 옵션을 활성화하고 rst를 사용하여 연결을 닫아 timewait 상태를 피하고 빠른 포트 재사용을 달성합니다.
