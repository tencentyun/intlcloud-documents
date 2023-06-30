Tencent Cloud는 Linux 공용 이미지에 기본적으로 일부 매개변수가 설정되어 있습니다. 그러나 sysctl은 고도로 개성화된 설정으로, 비즈니스 특성에 따라 sysctl 단독 설정을 권장합니다. 본 문서를 통해 Tencent Cloud의 공유 클라우드 Linux 공유 이미지에 대한 특수한 기본 최적화 설정 및 일반적인 설정을 확인할 수 있으며 비즈니스에 따라 수동으로 최적화 설정을 할 수 있습니다.
>?
>- “초기화 설정”은 “-” 매개변수 항목으로 공식 이미지 기본 설정이 유지됩니다.
>- sysctl -w 명령어를 사용하여 설정을 임시 적용할 수 있으며 /etc/sysctl.conf를 입력하여 설정을 영구 적용할 수 있습니다.


### 네트워크 유형
<table>
<tr>
<th>매개변수</th><th>설명</th><th>초기화 설정</th>
</tr>
<tr>
<td><code>net.ipv4.tcp_tw_recycle</code></td>
<td>해당 매개변수는 빠르게 TIME_WAIT 연결을 회수하는 데 사용합니다. 비활성화 시 커널이 패킷의 타임스탬프를 검사하지 않으며, 활성화 시 검사합니다.<br>해당 매개변수 활성화를 권장하지 않으며, 타임스탬프가 비단조로 증가하는 상황의 경우 패킷 손실 문제가 발생하며 고급 버전 커널에서는 해당 매개변수가 삭제되어 있습니다.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.core.somaxconn</code></td>
<td>3회의 핸드셰이크 대응이 종료되어도 큐를 accept할 때의 establish 상태가 존재하지 않습니다. accept 큐가 많은 경우는 클라이언트 accept 효율이 낮거나 단시간 내에 돌발적으로 대량의 신규 연결이 생성되었다는 의미입니다. 해당 값이 너무 낮은 경우 서버가 syn을 수신해도 롤백하지 않으며, somaxconn 리스트가 포화되어 생성한 syn 연결을 삭제합니다. 동시 연결이 많은 비즈니스의 경우 해당 값을 높일 수 있으나 딜레이가 발생할 수 있습니다.
</td>
<td>128</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_max_syn_backlog</code></td>
<td>반연결(semi-connected) 대응 최댓값으로 일반적인 synflood 공격을 방어합니다. 그러나 tcp_syncookies=1일 경우 반연결은 해당 최댓값을 초과할 수 있습니다.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_syncookies</code></td>
<td>SYN Cookies 활성화 대응은 Cookies를 활성화하여 처리하는 것을 의미하며, 일부 SYN 공격을 방지할 수 있고 SYN 대기 큐 오버플로우 발생 시에도 지속적으로 연결할 수 있습니다. 그러나 활성화 후 SHA1 인증 Cookies를 사용하여 이론적으로는 CPU 사용률을 증가시킵니다.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.core.rmem_default</code><br>
<code>net.core.rmem_max</code><br>
<code>net.ipv4.tcp_mem</code><br>
<code>net.ipv4.tcp_rmem</code>
</td>
<td>해당 매개변수는 데이터가 수신하는 캐시 크기를 설정합니다. 너무 크게 설정하는 경우 커널 리소스 낭비가 발생할 수 있으며, 너무 작게 설정하는 경우 패킷 손실이 발생할 수 있습니다. 비즈니스가 동시 연결 수요가 높은지, 또는 동시 연결 수요는 적으나 처리량이 많은지 여부를 판단하여 설정을 최적화하십시오.<ul><li>이론적으로 rmem_default 최적화 설정 정책은 대역폭/RTT 누적으로, 해당 설정은 tcp_rmem을 덮어쓰기하여 tcp_rmem이 단독 설정되지 않습니다.</li><li>rmem_max는 rmem_default의 약 5배로 설정합니다.</li><li>tcp_mem은 총 TCP 메모리 점유율로, 일반적으로 OS가 CVM 가용 메모리의 3/32, 1/8 또는 3/16으로 자동 설정합니다. 또한 tcp_mem과 rmem_default는 최대 동시 연결 수를 결정합니다.</li></ul></td>
<td><code>rmem_default<br>=655360</code><br>
<code>rmem_max<br>=3276800</code></td>
</tr>
<tr>
<td><code>net.core.wmem_default</code><br>
<code>net.core.wmem_max</code><br>
<code>net.ipv4.tcp_wmem</code>
</td>
<td>해당 매개변수는 데이터 발송 캐시 설정에 사용되며, Tencent Cloud 플랫폼 상에서의 데이터 발송은 통상적으로 병목 현상이 발생하지 않아 설정하지 않습니다.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_keepalive_intvl</code><br>
<code>net.ipv4.tcp_keepalive_probes</code><br>
<code>net.ipv4.tcp_keepalive_time</code>
</td>
<td>해당 매개변수는 TCP KeepAlive와 관련되어 있으며 기본적으로 75/9/7200으로 설정되어 있습니다. TCP 연결이 7200초 유휴 후에 메모리가 탐색을 시작한다는 의미로, 탐색에 9번(한 번당 75초) 실패해야만 메모리에서 RST를 시작합니다. 서버 입장에서 기본값이 비교적 큰 경우 비즈니스와 결합하여 30/3/1800으로 변경할 수 있습니다.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_local_port_range</code></td>
<td>가용 포트의 범위를 설정합니다. 필요에 따라 조정하십시오.</td>
<td>-</td>
</tr>
<tr>
<td><code>tcp_tw_reuse</code></td>
<td>해당 매개변수는 TIME-WAIT 상태의 socket을 새로운 TCP 연결에 사용하는 것을 허용합니다. 고정 포트를 점유하고 있는 링크를 빠르게 재활성화하는 데 도움을 주지만, NAT 네트워크 기반에서는 잠재적인 위험이 있어 고급 버전의 커널에서는 0/1/2 세 개 값으로 변경되었으며, 2로 설정되어 있습니다.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_forward</code><br>
<code>net.ipv6.conf.all.forwarding</code>
</td>
<td>IP 포워딩 기능은 docker의 라우터 포워딩 시나리오에 사용하는 경우 1로 설정합니다.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.rp_filter</code></td>
<td>해당 매개변수는 ENI가 수신하는 데이터 패키지에 리버스 라우터 인증 규칙을 진행하며, 0/1/2로 설정합니다. RFC3704 권장사항에 따라 1로 설정하는 것이 좋으며, 엄격한 리버스 라우터 인증을 활성화하면 일부 DDos 공격과 IP Spoofing 등을 방지할 수 있습니다.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.accept_source_route</code></td>
<td>CentOS 공식 사이트 권장사항에 따라 기본적으로 원본 라우터 정보가 포함된 IP 패킷 수신을 허용하지 않습니다.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.all.promote_secondaries</code><br>
<code>net.ipv4.conf.default.promote_secondaries</code></td>
<td>메인 IP 주소가 삭제된 경우, 두 번째 IP 주소를 새로운 메인 IP 주소로 설정할지 여부를 설정합니다.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.ipv6.neigh.default.gc_thresh3</code><br>
<code>net.ipv4.neigh.default.gc_thresh3</code>
</td>
<td>ARP 고속 캐시에 저장하는 최대 기록 수량을 제한합니다. 고속 캐시의 개수가 설정값을 초과하면 휴지통이 즉시 실행됩니다.</td>
<td>4096</td>
</tr>
</table>



### 메모리 유형

<table>
<tr>
<th>매개변수</th><th>설명</th><th>초기화 설정</th>
</tr>
<tr>
<td><code>vm.vfs_cache_pressure</code></td>
<td>초기값은 100으로, dentry 스캔을 나타냅니다. 100을 기준으로 값이 커질수록 커널 회수 알고리즘에서 메모리 회수 가중치가 높아집니다. curl을 기반으로 하는 비즈니스는 통상적으로 dentry 누적으로 인해 모든 가용 메모리가 꽉 차서 OOM 또는 커널 bug 유형의 문제가 쉽게 발생합니다. 종합적으로 회수율과 성능을 고려하여 250으로 설정하였으며, 필요에 따라 조절할 수 있습니다.</td>
<td>250</td>
</tr>
<tr>
<td><code>vm.min_free_kbytes</code></td>
<td>해당 값은 실행 시 시스템에 따라 가용 물리적 메모리 MEM을 자동으로 4 * sqrt(MEM)로 계산합니다. 이는 시스템 실행 시 최소한 남겨 놓아야 하는 KB 메모리를 의미하며, 일반적으로 커널 스레드 사용으로 제공됩니다. 해당 값을 너무 크게 설정할 필요는 없으며, 기기 패킷량에 약간의 돌발 상황이 발생하는 경우 일정한 확률로 vm.min_free_kbytes가 손상되어 OOM이 발생합니다. 크게 설정한 기기에서 vm.min_free_kbytes는 기본적으로 총 메모리의 1% 정도로 설정하는 것을 권장합니다.
</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.printk</code></td>
<td>커널 printk 함수의 출력 레벨은 기본적으로 5 이상으로 설정되어 있습니다.</td>
<td>5 4 1 7</td>
</tr>
<tr>
<td><code>kernel.numa_balancing</code></td>
<td>해당 매개변수는 커널에서 발송하여 프로세스되는 데이터를 해당하는 NUMA로 이동하는 것을 의미합니다. 그러나 실제 애플리케이션 효과가 좋지 않고 기타 성능에 영향을 미치므로 redis 시나리오에서 활성화를 테스트해 볼 수 있습니다.</td>
<td>0</td>
</tr>
<tr>
<td><code>kernel.shmall</code><br>
<code>kernel.shmmax</code>
</td>
<td><ul><li>shmmax는 한 번에 할당하는 shared memory의 최대 길이를 설정하며, 단위는 byte입니다.</li><li>shmall은 할당할 수 있는 총 shared memory의 최대 길이를 설정하며, 단위는 page입니다.</li></ul></td>
<td><code>kernel.shmmax<br>=68719476736</code><br>
<code>kernel.shmall<br>=4294967296</code>
</td>
</tr>
</table>

### 프로세스 유형
<table>
<tr>
<th>매개변수</th><th>설명</th><th>초기화 설정</th>
</tr>
<tr>
<td><code>fs.file-max</code><br>
<code>fs.nr_open</code>
</td>
<td>각 시스템의 모든 프로세스와 단일 프로세스에서 동시에 열고 제어할 수 있는 파일 최대 수량입니다.<ul><li>file-max는 OS 실행 시 자동으로 설정하며 약 10만/GB입니다.</li><li>nr_open은 1048576 고정값이나 사용자 상태에 맞춰 열 수 있는 최대 수량을 제한할 수 있으며 일반적으로는 해당 값을 변경하지 않습니다. 통상적으로 ulimit -n을 설정하여 구현하며 해당하는 설정 파일은 /etc/security/limits.conf입니다.</li></ul></td>
<td>
<code>ulimit의 open files는 100001개입니다.</code><br>
<code>fs.nr_open=1048576</code>
</td>
</tr>
<tr>
<td><code>kernel.pid_max</code></td>
<td>시스템 내에서의 프로세스 최대 수량으로, 공식 이미지는 기본적으로 32768개로 설정되어 있으며 필요에 따라 조절할 수 있습니다.</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.core_uses_pid</code></td>
<td>해당 설정은 coredump 파일 생성 시 pid를 포함할지 여부를 결정합니다.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.sysrq</code></td>
<td>해당 매개변수를 활성화하면, 이후 /proc/sysrq-trigger에 관련 작업을 진행할 수 있습니다.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.msgmnb</code><br>
<code>kernel.msgmax</code>
</td>
<td>각 메시지 큐 상의 최대 바이트 수와 단일 메시지 큐의 최대 용량을 나타냅니다.</td>
<td>65536</td>
</tr>
<tr>
<td><code>kernel.softlockup_panic</code></td>
<td>softlockup_panic을 설정한 경우, 커널에서 프로세스 softlockup 점검 시 panic이 발생하며 kdump의 설정과 결합하여 vmcore를 생성해 softlockup의 원인을 분석하는 데 사용할 수 있습니다.</td>
<td>-</td>
</tr>
</table>


### IO 유형
<table>
<tr>
<th>매개변수</th><th>설명</th><th>초기화 설정</th>
</tr>
<tr>
<td><code>vm.dirty_background_bytes</code><br>
<code>vm.dirty_background_ratio</code><br>
<code>vm.dirty_bytes</code><br>
<code>vm.dirty_expire_centisecs</code><br>
<code>vm.dirty_ratio</code><br>
<code>vm.dirty_writeback_centisecs</code>
</td>
<td>해당 부분의 매개변수는 주로 IO 후기록 디스크 정책을 설정합니다.<ul><li>dirty_background_bytes/dirty_bytes와 dirty_background_ratio/dirty_ratio는 각 메모리 더티 페이지 임계값의 절대 수량과 비율 수량으로, 일반적으로 ratio를 설정합니다.</li><li>dirty_background_ratio란 파일 시스템 캐시의 더티 페이지 수량이 시스템 메모리의 n%가 되면(기본 10%) 커널 flush 등의 프로세스를 wake up하고 디스크에 후기록합니다.</li><li>dirty_ratio는 더티 페이지 최대 비율로, 더티 페이지가 해당 비율이 되면 모든 오손 데이터를 디스크로 제출하며, 이와 동시에 오손 데이터가 디스크에 기록이 완료될 때까지 모든 신규 IO를 차단하여 IO 랙이 발생하게 됩니다. 시스템은 먼저 vm.dirty_background_ratio 조건을 만족하면 flush 프로세스가 트리거되어 비동기화 후기록 작업을 진행하며, 이때 애플리케이션 프로세스에서는 쓰기 작업을 진행할 수 있습니다. vm.dirty_ratio 매개변수에서 설정한 값을 만족하는 경우에는 운영 체제가 더티 페이지 동기화 프로세스로 전환되어 애플리케이션 프로세스가 차단됩니다.<br>
</li><li>vm.dirty_expire_centisecs는 더티 페이지가 유지되는 시간으로, flush 프로세스에서 데이터가 해당 시간을 초과하였는지 여부를 점검하며 단위는 1/100초입니다.</li><li>vm.dirty_writeback_centisecs는 flush 프로세스의 wake up 주기로 단위는 1/100초입니다.</li></ul>
</td>
<td>-</td>
</table>
