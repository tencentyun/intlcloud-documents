O Tencent Cloud fornece as imagens públicas do Linux com configurações padrão, mas recomendamos que você configure `sysctl` separadamente para se adaptar ao seu negócio específico. Este documento descreve as configurações padrão e ideais das imagens públicas do Tencent Cloud no Linux e ajuda a ajustá-las manualmente conforme necessário.
>?
>- Os parâmetros expressos como "-" em **Initial Configuration (Configuração inicial)** usam as configurações padrão da imagem oficial.
>- O comando `sysctl -w` faz com que as configurações entrem em vigor apenas temporariamente, já os parâmetros gravados em `/etc/sysctl.conf` entram em vigor permanentemente.


### Relacionados à rede
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th><th>Configuração inicial</th>
</tr>
<tr>
<td><code>net.ipv4.tcp_tw_recycle</code></td>
<td>Esse parâmetro é usado para reciclar a conexão TIME_WAIT rapidamente. Se ativado, o kernel vai verificar o carimbo de data/hora do pacote.<br>Não recomendamos ativar esse parâmetro, porque a perda de pacotes pode ocorrer quando o carimbo de data/hora não estiver aumentando monotonicamente. Esse parâmetro está desativado em versões posteriores do kernel.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.core.somaxconn</code></td>
<td>Esse parâmetro é usado para definir o estado ESTABLISH no final do handshake triplo quando não há fila ACCEPT. Uma fila ACCEPT mais longa indica baixa taxa de processamento do cliente ou uma intermitência de novas conexões em um curto espaço de tempo. Definir <code>net.core.somaxconn</code> muito baixo pode causar perda de pacotes porque a nova conexão SYN será descartada quando o servidor receber o pacote SYN e a tabela somaxconn estiver cheia. Definir um valor muito alto só é necessário para serviço de alta simultaneidade, mas a latência pode aumentar.
</td>
<td>128</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_max_syn_backlog</code></td>
<td>Esse parâmetro especifica a quantidade máxima de conexões na fila SYN_RECV, que já foi usada para defender contra ataques flood de syn comuns. No entanto, se <code>tcp_syncookies=1</code>, as conexões na fila SYN_RECV excederão o limite superior.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_syncookies</code></td>
<td>Esse parâmetro é usado para ativar os cookies de SYN, o que evita alguns ataques de SYN. Se ativado, as conexões ainda podem ser estabelecidas quando a fila de SYN estiver sobrecarregada. No entanto, SHA1 será usado para verificar os cookies, o que teoricamente aumenta a utilização da CPU.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.core.rmem_default</code><br>
<code>net.core.rmem_max</code><br>
<code>net.ipv4.tcp_mem</code><br>
<code>net.ipv4.tcp_rmem</code>
</td>
<td>Esses parâmetros são usados para configurar o tamanho do cache dos dados recebidos. Definir valores muito altos pode desperdiçar recursos de memória, já os definir muito baixo pode causar perda de pacotes. Você pode ajustá-los de acordo com a simultaneidade e a taxa de transferência do seu negócio.<ul><li>rmem_default: a configuração ideal na teoria é igual ao valor da largura de banda dividido pelo RTT, que substituirá as configurações de tcp_rmem e tcp_rmem </li><li>rmem_max: aproximadamente cinco vezes rmem_default</li><li>tcp_mem: memória TCP total consumida, que é automaticamente definida como 3/32, 1/8 ou 3/16 da memória disponível do CVM. Os parâmetros tcp_mem e rmem_default também determinam a quantidade máxima de conexões simultâneas.</li></ul></td>
<td><code>rmem_default<br>=655360</code><br>
<code>rmem_max<br>=3276800</code></td>
</tr>
<tr>
<td><code>net.core.wmem_default</code><br>
<code>net.core.wmem_max</code><br>
<code>net.ipv4.tcp_wmem</code>
</td>
<td>Esses parâmetros são usados para configurar o cache de transmissão de dados. O envio de dados no Tencent Cloud não costuma ter gargalos, então essas configurações são opcionais.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_keepalive_intvl</code><br>
<code>net.ipv4.tcp_keepalive_probes</code><br>
<code>net.ipv4.tcp_keepalive_time</code>
</td>
<td>Esses parâmetros são relevantes para o Keepalive TCP, cujo padrão é 75/9/7200. As configurações padrões indicam que o kernel iniciará a detecção quando uma conexão TCP estiver inativa por 7.200 segundos e enviará RST após 9 falhas de detecção (cada uma por 75 segundos). Esses valores são muito altos para um servidor. Você pode ajustá-los para 30/3/1800 conforme necessário.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_local_port_range</code></td>
<td>Esse parâmetro é usado para configurar o intervalo de portas disponível, que pode ser ajustado conforme necessário.</td>
<td>-</td>
</tr>
<tr>
<td><code>tcp_tw_reuse</code></td>
<td>Esse parâmetro é usado para reutilizar um soquete no estado TIME-WAIT para novas conexões TCP. Isso ajuda a reiniciar rapidamente links que usam portas fixas, mas pode envolver riscos na rede baseada em NAT. As versões posteriores do kernel aceitam os valores 0, 1 e 2 e configuram-no para 2.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_forward</code><br>
<code>net.ipv6.conf.all.forwarding</code>
</td>
<td>Esse parâmetro é usado para especificar o encaminhamento de IP. Você pode configurá-lo para 1 no cenário de encaminhamento de rota do Docker.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.rp_filter</code></td>
<td>Esse parâmetro é usado para especificar a regra de validação de caminho reverso de ENI em pacotes de dados recebidos. Os valores válidos incluem 0, 1 (recomendado pela RFC3704) e 2. A configuração recomendada é um modo estrito que pode evitar ataques de DDoS e atos de falsificação de IP.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.accept_source_route</code></td>
<td>Esse parâmetro é usado para especificar se os pacotes de IP contendo rotas de origem devem ser aceitos, o que não é permitido por padrão, conforme recomendado no site do CentOS.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.all.promote_secondaries</code><br>
<code>net.ipv4.conf.default.promote_secondaries</code></td>
<td>Esse parâmetro é usado para especificar se um endereço IP secundário se tornará um IP principal depois que o endereço IP principal original for excluído.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.ipv6.neigh.default.gc_thresh3</code><br>
<code>net.ipv4.neigh.default.gc_thresh3</code>
</td>
<td>Esse parâmetro é usado para definir a quantidade máxima de registros armazenada no cache ARP. O coletor de lixo inicia imediatamente quando os registros armazenados excedem o valor definido.</td>
<td>4096</td>
</tr>
</table>



### Relacionados à memória

<table>
<tr>
<th>Parâmetro</th><th>Descrição</th><th>Configuração inicial</th>
</tr>
<tr>
<td><code>vm.vfs_cache_pressure</code></td>
<td>Ele controla a tendência do kernel de recuperar a memória. No valor padrão de 100, o kernel tentará recuperar as dentries de volta para a memória. Os serviços baseados em curl costumam acumular dentries, que podem usar toda a memória livre e causar OOM ou bug no kernel. Nós o configuramos para 250 para equilibrar a frequência de recuperação e o desempenho, que é ajustável.</td>
<td>250</td>
</tr>
<tr>
<td><code>vm.min_free_kbytes</code></td>
<td>Esse parâmetro é usado para forçar a MEM do Linux a manter uma quantidade mínima de kilobytes de memória livre para uso pelas threads do kernel. O valor é calculado automaticamente de acordo com a memória física livre (MEM) na inicialização por: 4*raiz (MEM). Quando o servidor recebe microintermitências de pacotes, seu servidor pode ficar sutilmente interrompido e causar OOM. Em um servidor de alta configuração, recomendamos configurar <code>vm.min_free_kbytes</code> em cerca de 1% da memória total por padrão.
</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.printk</code></td>
<td>Ele especifica o nível da função de impressão printk do kernel. A configuração padrão é cinco ou superior. </td>
<td>5 4 1 7</td>
</tr>
<tr>
<td><code>kernel.numa_balancing</code></td>
<td>Ele indica que o kernel pode mover processos de forma automática para o nó NUMA correspondente, mas é ineficaz e afeta o desempenho. Você pode tentar ativá-lo nos casos de uso do Redis.</td>
<td>0</td>
</tr>
<tr>
<td><code>kernel.shmall</code><br>
<code>kernel.shmmax</code>
</td>
<td><ul><li>shmmax: define o tamanho máximo de um único segmento de memória compartilhada (em bytes) que um processo Linux pode alocar.</li><li>shmall: define a quantidade total de páginas de memória compartilhada em todo o sistema.</li></ul></td>
<td><code>kernel.shmmax<br>=68719476736</code><br>
<code>kernel.shmall<br>=4294967296</code>
</td>
</tr>
</table>

### Relacionados ao processo
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th><th>Configuração inicial</th>
</tr>
<tr>
<td><code>fs.file-max</code><br>
<code>fs.nr_open</code>
</td>
<td>Eles denotam a quantidade máxima de identificadores de arquivo que o kernel do Linux ou um processo pode alocar, respectivamente.<ul><li>file-max: configura de forma automática para aproximadamente 100.000/GB quando o sistema operacional inicia.</li><li>nr_open: define o valor fixo de 1048576, que limita o máximo de identificadores de arquivos abertos em um ambiente de modo de usuário. De forma geral, mantenha esse valor inalterado. Para modificar o máximo de identificadores de arquivos abertos, configure o parâmetro <code>ulimit -n</code> no arquivo de configuração /etc/security/limits.conf.</li></ul></td>
<td>
<code>ulimit -n=100001</code><br>
<code>fs.nr_open=1048576</code>
</td>
</tr>
<tr>
<td><code>kernel.pid_max</code></td>
<td>Ele especifica a quantidade máxima de processos em um sistema. A imagem oficial usa o valor padrão de 32768, que pode ser ajustado conforme necessário.</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.core_uses_pid</code></td>
<td>Ele determina se o nome do arquivo coredump gerado conterá .PID.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.sysrq</code></td>
<td>Ele permite que você opere em /proc/sysrq-trigger posteriormente.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.msgmnb</code><br>
<code>kernel.msgmax</code>
</td>
<td>Eles definem o tamanho máximo em bytes de uma única fila de mensagens e o tamanho máximo permitido em bytes de mensagens únicas em uma fila de mensagens, respectivamente</td>
<td>65536</td>
</tr>
<tr>
<td><code>kernel.softlockup_panic</code></td>
<td>Ele controla se o kernel entrará em estado de emergência quando um travamento temporário for detectado. Se ativado, um vmcore será gerado com base na configuração do kdump, que pode ser usado para analisar a causa do travamento temporário.</td>
<td>-</td>
</tr>
</table>


### Relacionados à E/S
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th><th>Configuração inicial</th>
</tr>
<tr>
<td><code>vm.dirty_background_bytes</code><br>
<code>vm.dirty_background_ratio</code><br>
<code>vm.dirty_bytes</code><br>
<code>vm.dirty_expire_centisecs</code><br>
<code>vm.dirty_ratio</code><br>
<code>vm.dirty_writeback_centisecs</code>
</td>
<td>Esses parâmetros são usados principalmente para configurar a política de E/S sendo gravada de volta no disco.<ul><li>dirty_background_bytes/dirty_bytes e dirty_background_ratio/dirty_ratio se refere à quantidade e à porcentagem de memória do sistema que pode ser preenchida com páginas "sujas", respectivamente. Em geral, a taxa será especificada.</li><li>dirty_background_ratio: refere-se a uma porcentagem de páginas sujas na memória do sistema (10% por padrão) na qual os processos de liberação do kernel em segundo plano começarão a gravar de volta no disco. </li><li>dirty_ratio: refere-se à quantidade máxima absoluta de memória do sistema que pode ser preenchida com páginas sujas antes que tudo seja confirmado no disco. Quando o sistema chega a este ponto, todas as E/S são bloqueadas até que as páginas sujas tenham sido gravadas no disco, causando longas pausas de E/S. Primeiro, o sistema obterá a condição `vm.dirty_background_ratio` na qual os processos de liberação iniciarão um write-back assíncrono e os aplicativos continuarão a gravar. Quando o sistema atingir o valor especificado de `vm.dirty_ratio`, o sistema operacional vai lidar com as páginas sujas de forma síncrona, bloqueando os aplicativos.<br>
</li><li>vm.dirty_expire_centisecs: especifica por quanto tempo a página suja pode ficar no cache antes de precisar ser gravada. É expresso em centésimos de segundo. Os dados que ficaram sujos na memória por mais tempo do que esse intervalo serão gravados na próxima vez que um processo de limpeza for ativado.</li><li>vm.dirty_writeback_centisecs: especifica com que frequência os processos de liberação do kernel são ativados. É expresso em centésimos de segundo.</li></ul>
</td>
<td>-</td>
</table>
