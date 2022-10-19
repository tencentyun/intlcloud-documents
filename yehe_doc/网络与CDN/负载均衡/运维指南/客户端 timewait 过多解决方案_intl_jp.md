## このドキュメントの背景
お客様がCLBのストレステストを行う際、クライアントのtimewaitが多すぎるためにすべてのポートがすぐに占有され、connectに失敗するケースがよくみられます。その原因と対処方法についてご説明します。

## Linuxパラメータの説明
**tcp_timestamps ：** tcp timestampsオプションを有効にするかどうか。timestampsはtcpの3ウェイハンドシェイクのプロセスでネゴシエートするもので、どちらか一方がサポートしていなければ、その接続にはtimestampsオプションが使用されません。
**tcp_tw_recycle ：**  tcp time_wait状態の回収を有効にするかどうか。
**tcp_tw_reuse ：** 有効にすると、1秒を超えるtime_wait状態の接続を直接回収できます。

## 原因の分析
クライアントのtimewaitが多すぎる原因は、クライアントが能動的に接続を切断する際、クライアントが1つの接続を切断するたびにその接続がtimewait状態になり、デフォルトでは60秒を超えてから回収されるためです。一般的にこのような状況になった場合、お客様は`tcp_tw_recycle`および`tcp_tw_reuse`の2つのパラメータを有効化し、timewait状態の接続を回収しやすくすることができます。
ただし、その際にCLBが`tcp_timestamps`オプションを有効にしていなければ、クライアントが有効にした`tcp_tw_recycle`と`tcp_tw_reuse`はどちらも効力を発揮せず、timewait状態の接続を速やかに回収することができません。以下、いくつかのLinuxパラメータの意味と、CLBが`tcp_timestamps`を有効にできない原因について説明します。
1. tcp_tw_recycleとtcp_tw_reuseは、tcp_timestampsが有効になっている場合にのみ有効です。
2. FullNATのシーンでは、tcp_timestampsとtcp_tw_recycleは同時に有効にすることはできません。パブリックネットワークのクライアントがNAT Gatewayを経由してサーバーにアクセスすると問題が生じるからです。その理由は次のとおりです。
tcp_tw_recycle/tcp_timestampsがどちらも有効という条件下では、同一ソースIPのホストのsocket connectリクエスト内にあるtimestampは、60秒間インクリメントする必要があります。2.6.32カーネルを例に挙げると、具体的な実装は次のようになります。
```
if(tmp_opt.saw_tstamp && tcp_death_row.sysctl_tw_recycle &&
(dst = inet_csk_route_req(sk,req))!= NULL &&
	(peer = rt_get_peer((struct rtable *)dst))!= NULL && 
	peer->v4daddr == saddr){
	if(get_seconds()< peer->tcp_ts_stamp + TCP_PAWS_MSL &&
		(s32)(peer->tcp_ts - req->ts_recent) > TCP_PAWS_WINDOW){
			NET_INC_STATS_BH(sock_net(sk),LINUX_MIB_PAWSPASSIVEREJECTED);
			goto ↓drop_and_release；
	}
}
```
>?tmp_opt.saw_tstamp：このsocketはtcp_timestampをサポートします。
>sysctl_tw_recycle：このマシンのシステムではtcp_tw_recycleオプションが有効化されています。
>TCP_PAWS_MSL：60s。この条件から、このソースIPの前回のtcp通信が60秒以内に発生したと判断できます。
>TCP_PAWS_WINDOW：1。この条件から、このソースIPの前回のtcp通信のtimestampが今回のtcpのものより大きいと判断できます。
>
3. CLB（レイヤー7）がtcp_timestampsを無効にした原因は、パブリックネットワークのクライアントがNAT Gatewayを経由してサーバーにアクセスすると、次の例のような問題が生じる可能性があるためです。
a)	ある5つ組はまだtime_wait状態にあります。NAT Gatewayのポート割り当てポリシーにより、2MSLの間に同じ5つ組が再利用され、synパケットが送信されます。
b)	tcp_timestampsが有効な場合、次の2つの条件が同時に満たされると、このsynパケットは破棄されます（タイムスタンプオプションを有効にしているため、古いパケットと判断されます）。
i.	前回のタイムスタンプ > 今回のタイムスタンプ。
ii.	24日以内に受信したパケットである（タイムスタンプのフィールドは32桁で、Linuxではデフォルトで1ミリ秒に1回タイムスタンプを更新するため、24日でタイムスタンプのラップアラウンドが生じます）。
備考：この問題はモバイル端末でより顕著になります。クライアントはすべてキャリアのNAT Gateway下で有限のパブリックIPを共有しているため、5つ組は2MSLのうちに再利用される可能性があり、各クライアントから渡されるタイムスタンプのインクリメントを保証することができない場合があるためです。
2.6.32カーネルの場合の具体的な実装例は次のとおりです。
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
>?rx_opt->ts_recent：前回のタイムスタンプです。
>rx_opt->rcv_tsval：今回受信したタイムスタンプです。
>get_seconds（）： 現在時刻です。
>rx_opt->ts_recent_stamp： 前回のパケット受信時刻です。
>

## 対処方法
クライアントのTimewaitが多すぎる問題には次のような対処方法があります。
- HTTPが短時間接続を使用する（Connection: close）。この場合、CLBは能動的に接続を切断するため、クライアントではtimewaitが発生しません。
- 長時間接続が必要なシーンでは、socketのSO_LINGERオプションを有効にし、rstを使用して接続を切断することでtimewaitになるのを避け、ポートの高速回収という目的を果たすことができます。
