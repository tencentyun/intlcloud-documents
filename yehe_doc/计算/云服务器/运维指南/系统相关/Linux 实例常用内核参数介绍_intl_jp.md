Tencent Cloudは、Linuxパブリックイメージにデフォルト構成を提供しますが、sysctlの構成は高度にパーソナライズされているため、ユーザーが自分のビジネス特性に従ってsysctlを個別に構成することをお勧めします。このドキュメントでは、Tencent Cloud Linuxパブリックイメージのデフォルト構成および最適な構成について説明し、必要に応じて手動で調整するのに役立ちます。
>?
>- 「初期設定」項目で「-」と表示されているパラメータは、公式イメージのデフォルト構成を使用しています。
>- sysctl -wコマンドを使用して、構成を一時的に有効にするだけですが、/etc/sysctl.confに書き込まれた構成は永続的に有効になります。


### ネットワーク関連
<table>
<tr>
<th>パラメータ</th><th>説明</th><th>初期設定</th>
</tr>
<tr>
<td><code>net.ipv4.tcp_tw_recycle</code></td>
<td>このパラメーターは、TIME_WAIT接続をすばやくリサイクルするために使用されます。無効にする場合は、カーネルはパケットのタイムスタンプをチェックしません。有効にする場合は、カーネルはパケットのタイムスタンプをチェックします。<br>タイムスタンプが単調に増加していない場合にパケット損失が発生する可能性があるため、このパラメータを有効にすることはお勧めしません。Linux のカーネルパラメータ net.ipv4.tcp_tw_recycle は、バージョン4.12から廃止されました。</td>
<td>0</td>
</tr>
<tr>
<td><code>net.core.somaxconn</code></td>
<td>このパラメーターは、ACCEPTキューがない場合に、3ウェイ・ハンドシェイクの終了時にEstablished状態を定義するために使用されます。 ACCEPTキューが長い場合は、クライアントの処理速度が遅いか、短時間で新しい接続がバーストしていることを示します。 net.core.somaxconnの設定値が低すぎると、サーバーがSYNパケットを受信し、somaxconnテーブルがいっぱいになると、新しいSYN接続が破棄されるため、パケット損失が発生する可能性があります。複数の業務を同時進行させなければいけない場合、net.core.somaxconnの設定値を増やすことができますが、遅延が長くなる可能性があります。
</td>
<td>128</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_max_syn_backlog</code></td>
<td>このパラメーターは、SYN_RECVキュー内の接続の最大量を決定します。一般的なシンフラッド攻撃から防御するために使用されます。ただし、tcp_syncookies = 1の場合、SYN_RECVキュー内の接続数が上限を超えます。</td>
<td>-</td>
</tr>
</tr>
<td><code>net.ipv4.tcp_syncookies</code></td>
<td>このパラメータは、SYN Cookieが有効かどうかを決定し、一部のSYN攻撃を防ぎます。有効にすると、SYNキューがオーバーフローしたときに接続を確立できます。ただし、SHA1は、このパラメータを有効にした後にCookieを検証するために使用されるため、理論的にはCPU使用率が増加します。</td>
<td>1</td>
</tr>
<tr>
<td><code>net.core.rmem_default</code><br>
<code>net.core.rmem_max</code><br>
<code>net.ipv4.tcp_mem</code><br>
<code>net.ipv4.tcp_rmem</code>
</td>
<td>これらのパラメーターは、受信データのキャッシュサイズを設定するために使用されます。サイズを高く設定しすぎるとメモリリソースが浪費される可能性があり、サイズを低く設定しすぎるとパケット損失が発生する可能性があります。自身のビジネスが高並列接続に属しているのか、並列性の低い高スループットの状況に属しているのかを判断し、構成を最適化することをお勧めします。<ul><li>rmem_default：理論的に最適な構成ポリシーは、帯域幅/RTT の積（帯域幅遅延積）です。</li><li> rmem_max構成は、rmem_defaultの約5倍です。</li><li>tcp_memはシステム全体でTCP が消費できるメモリの最大値。通常、CVMの使用可能なメモリの3/32、1/8、または3/16に自動的に設定されます。パラメータtcp_memおよびrmem_defaultは、同時接続する最大数を決定します。</li></ul></td>
<td><code>rmem_default<br>=655360</code><br>
<code>rmem_max<br>=3276800</code></td>
</tr>
<tr>
<td><code>net.core.wmem_default</code><br>
<code>net.core.wmem_max</code><br>
<code>net.ipv4.tcp_wmem</code>
</td>
<td>これらのパラメーターは、データ送信キャッシュを構成するために使用されます。通常、Tencent Cloudプラットフォームでのデータ送信にボトルネックはなく、構成は必要ありません。</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_keepalive_intvl</code><br>
<code>net.ipv4.tcp_keepalive_probes</code><br>
<code>net.ipv4.tcp_keepalive_time</code>
</td>
<td>これらのパラメータはTCP KeepAliveに関連しており、デフォルトは75/9/7200です。デフォルト設定では、TCP接続が7,200秒間アイドル状態になるとカーネルが検出を開始し、9回の検出失敗（毎回75秒）後にRSTを送信します。サーバーにとってデフォルト値が高すぎます、ビジネスに応じて 30/3/1800に調整できます。</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_local_port_range</code></td>
<td>このパラメーターは、使用可能なポート範囲を構成するために使用されます。必要に応じて調整できます。</td>
<td>-</td>
</tr>
<tr>
<td><code>tcp_tw_reuse</code></td>
<td>このパラメーターは、新しいTCP接続でTIME_WAIT状態のソケット再利用することを許可します。これにより、固定ポートを使用するリンクをすばやく再起動できますが、NATベースのネットワークにリスクを伴う可能性があります。カーネルの上位バージョンは0/1/2の3つの値に変更され、2に構成されます。</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_forward</code><br>
<code>net.ipv6.conf.all.forwarding</code>
</td>
<td>このパラメーターは、IP転送を指定するために使用されます。 Dockerのルーティング転送シナリオで1に構成できます。</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.rp_filter</code></td>
<td>このパラメータは、受信したデータパケットに対するENIのリバースパス検証ルールを指定するために使用されます。0、1（RFC3704で定義された厳密なモード、推奨され）、2に設定できます。RFC3704 における現在の推奨プラクティスは DDos 攻撃によるIPスプーフィングを回避するために厳密モードを有効にすることです。</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.accept_source_route</code></td>
<td>CentOSの公式Webサイトの推奨事項によると、ソースルーティング情報を含むIPパケットはデフォルトで受け入れられません。</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.all.promote_secondaries</code><br>
<code>net.ipv4.conf.default.promote_secondaries</code></td>
<td>このパラメータは、元のプライマリIPアドレスが削除された後にセカンダリIPアドレスがプライマリIPになるかどうかを指定するために使用されます。</td>
<td>1</td>
</tr>
<tr>
<td><code>net.ipv6.neigh.default.gc_thresh3</code><br>
<code>net.ipv4.neigh.default.gc_thresh3</code>
</td>
<td>ARP キャッシュに保存されるエントリ数のハードな最大値。キャッシュのエントリがこの数を越えると、ガベージ・コレクタはただちに実行されます。</td>
<td>4096</td>
</tr>
</table>



### メモリ関連

<table>
<tr>
<th>パラメータ</th><th>説明</th><th>初期設定</th>
</tr>
<tr>
<td><code>vm.vfs_cache_pressure</code></td>
<td>既定値は 100で、このパーセント値はカーネルがディレクトリとiノードオブジェクトのキャッシュに使用されるメモリを再利用するときの傾向を制御します。vfs_cache_pressureを100より大きくすると、カーネルはdentryとiノードキャッシュのメモリをより積極的に再利用するようになります。多くのカールベースのビジネスでは、dentryの蓄積により、メモリが一杯になり、OOMやカーネルのバグなど、想定外の問題が発生する可能性があります。再利用の頻度とパフォーマンスのバランスをとるために、250に設定することをお勧めします。必要に応じて調整できます。</td>
<td>250</td>
</tr>
<tr>
<td><code>vm.min_free_kbytes</code></td>
<td>このパラメーターは、起動時にシステムの使用可能な物理メモリMEMに従って自動的に計算されます：4 * sqrt（MEM）。min_free_kbytes を使用して、カーネルスレッドで使用するための最小キロバイト数の空きメモリを保持するように強制します。この値を大きく設定する必要はありません。サーバーがパケットのマイクロバーストを受信すると、OOM状態が発生する可能性があります。高構成サーバーでは、デフォルトでvm.min_free_kbytesを合計メモリの約1％になるように構成することをお勧めします。
</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.printk</code></td>
<td>printkの出力レベルを指定します。printkはカーネル内でのロギング（情報出力）のために使用しますが、その情報量を制御できます。デフォルトの構成は5以上です。</td>
<td>5 4 1 7</td>
</tr>
<tr>
<td><code>kernel.numa_balancing</code></td>
<td>このパラメータは、カーネルがプロセスデータを対応するNUMAノードに自動的に移動できることを示していますが、効果が良くない、パフォーマンスに影響を与える可能性があります。Redisユースケースでこのパラメータを有効にすることができます。</td>
<td>0</td>
</tr>
<tr>
<td><code>kernel.shmall</code><br>
<code>kernel.shmmax</code>
</td>
<td><ul><li>Linux プロセスが仮想アドレス空間に割り当てることができる1つの共有メモリーセグメントの最大サイズをバイト単位で定義します。</li><li>システム全体で使用できる共有メモリーページの合計を定義します。</li></ul></td>
<td><code>kernel.shmmax<br>=68719476736</code><br>
<code>kernel.shmall<br>=4294967296</code>
</td>
</tr>
</table>

### プロセス関連
<table>
<tr>
<th>パラメータ</th><th>説明</th><th>初期設定</th>
</tr>
<tr>
<td><code>fs.file-max</code><br>
<code>fs.nr_open</code>
</td>
<td>これらの2つのパラメーターはそれぞれ、システム内のすべてのプロセスと単一プロセスが同時にオープンできるファイル数の最大値を制御します。<ul><li>file-maxは、OS起動時に自動的に構成され、約100,000/GBです。</li><li> nr_openのデフォルト値は 1,048,576であり、このパラメーターはユーザーモード環境で開くことができる最大ファイル数が制限されます。通常、この値は変更しないでください。最大オープンファイル数を変更するには、/etc/security/limits.conf 構成ファイルでulimit -nパラメーターを構成してください。</li></ul>
<td>
<code>ulimitが開いているファイルの数は100001です。</code><br>
<code>fs.nr_open=1048576</code>
</td>
</tr>
<tr>
<td><code>kernel.pid_max</code></td>
<td>このパラメーターは、システム内のプロセスID(PID)の最大値を指定します。公式イメージのデフォルト値は32768で、必要に応じて調整できます。</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.core_uses_pid</code></td>
<td>この構成により、コアダンプファイルの生成時にpidが含まれるかどうかが決まります。</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.sysrq</code></td>
<td>このパラメータを有効にした後、/proc/sysrq-triggeで関連する操作を実行できます。</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.msgmnb</code><br>
<code>kernel.msgmax</code>
</td>
<td>kernel.msgmaxパラメータはメッセージキューでの単一メッセージの最大許容サイズをバイト単位で定義します。</td>
<td>65536</td>
</tr>
<tr>
<td><code>kernel.softlockup_panic</code></td>
<td>ソフトロックアップが検出されたときにカーネルでパニックを発生させるどうかを制御します。kdump構成に基づいてvmcoreが生成され、ソフトロックアップの原因を分析するために使用できます。</td>
<td>-</td>
</tr>
</table>


### IO関連
<table>
<tr>
<th>パラメータ</th><th>説明</th><th>初期設定</th>
</tr>
<tr>
<td><code>vm.dirty_background_bytes</code><br>
<code>vm.dirty_background_ratio</code><br>
<code>vm.dirty_bytes</code><br>
<code>vm.dirty_expire_centisecs</code><br>
<code>vm.dirty_ratio</code><br>
<code>vm.dirty_writeback_centisecs</code>
</td>
<td>これらのパラメーターは主に、ディスクに書き戻されるIOポリシーを構成するために使用されます。<ul><li>dirty_background_bytes/dirty_bytesとdirty_background_ratio/dirty_ratioは、それぞれメモリダーティページしきい値の絶対数と比率に対応します。一般的に、ratioが指定されます。</li><li>dirty_background_ratio は、パーセントの値を定義します。ダーティーデータのwriteout は (pdflush 経由で) ダーティーデータがメモリ合計のこのパーセントを占める際にバックグラウンドで開始されます。デフォルト値は10です。</li><li>dirty_ratioはpdflushが書き込みを始めるまでのダーティページの最大割合です。メモリ全体の中でダーティページの割合がこの値を超えると、すべてのダーティデータをディスクに書き込む必要があります。ダーティデータがディスクに書き込まれるまですべての新しいIOがブロックされます。システムは最初にvm.dirty_background_ratioの条件に到達し、次に flushプロセスをトリガーして非同期ライトバック操作を実行します。この時点でも、アプリケーションプロセスは書き込み操作を実行できます。vm.dirty_ratioパラメーターで設定された値に達すると、OSはダーティページを同期的に処理し、アプリケーションプロセスをブロックします。<br>
</li><li>vm.dirty_expire_centisecs はダーティーデータがディスクに書き戻されるまでにページキャッシュにとどまる時間を1/100 秒単位で指定します。</li><li>vm.dirty_writeback_centisecsはディスクキャッシュのフラッシュが開始される頻度、単位は1/100秒です。</li></ul>
</td>
<td>-</td>
</table>
