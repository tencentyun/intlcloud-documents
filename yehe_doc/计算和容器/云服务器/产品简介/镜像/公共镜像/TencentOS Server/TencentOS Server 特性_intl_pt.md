## Personalização do kernel
Baseado no Kernel Linux versão 4.14.105 estável e de longo prazo, o TencentOS Server traz novas funcionalidades voltadas a cenários em nuvem, melhora o desempenho do kernel e corrige defeitos relevantes.

## Otimizações de desempenho para cenários de container
O TencentOS Server otimiza os cenários de container fornecendo isolamento aprimorado e desempenho otimizado:
- Isolamento meminfo, vmstat, cpuinfo, stat e loadavg.
- Isolamento sysctl, tais como tcp_no_delay_ack, tcp_max_orphans.
- Corrige bugs em sistemas de arquivos e redes.
- Corrige exceções causadas pela reutilização de conexões em cenários de alta simultaneidade no modo IPVS.
- Corrige falhas de rede causadas por regras excessivas de IPVS em nós de alta especificação (com uma grande quantidade de núcleos de CPU) no modo IPVS.
- Corrige falhas de rede causadas quando o cAdvisor trava por muito tempo no estado do kernel, enquanto esse faz a leitura do memcg nos cenários de container de alta densidade (uma grande quantidade de containers em um único nó).
- Corrige falhas de rede causadas pelo balanceamento de carga da CPU em cenários de nós de alta especificação (com uma grande quantidade de núcleos de CPU) e de grandes pods (ocupando muitos núcleos com alto uso por núcleo).
- Corrige o problema de variação de sinal constante de rede causado pelo monitoramento de conexão TCP (por exemplo, a configuração do cAdvisor é implantada separadamente para monitorar a conexão TCP) em cenários de alta simultaneidade.
- Otimiza a interrupção lenta ao receber pacotes para melhorar o desempenho da rede.

## Funcionalidades do container personalizado
### Exibições isoladas dos recursos de container
- Adiciona um switch de nível de host: o TencentOS Server executa uma funcionalidade semelhante ao LXCFS em seu kernel. Em vez de implantar nós no sistema de arquivos LXCFS ou modificar a especificação do POD, você só precisa executar o comando `sysctl -w kernel.stats_isolated=1` para ativar um switch global em nós, e então os arquivos gerados, como `/proc/cpuinfo` e `/proc/meminfo`, serão isolados pelo container.
- Adiciona um switch de nível de container: o TencentOS Server adiciona um switch de nível de container `kernel.container_stats_isolated` para containers especiais, como o componente de monitoramento de nó. Quando o switch de nível de host estiver habilitado, você só precisará executar o comando `sysctl -w kernel.container_stats_isolated=0` no script de inicialização do container para desativar o switch de nível de container e, em seguida, as informações do host serão obtidas pela leitura de arquivos, como `/proc/cpuinfo` e `/proc/meminfo`, nos containers.

### Isolamento dos parâmetros do kernel
O TencentOS Server isola os seguintes parâmetros do kernel por namespace:
- `net.ipv4.tcp_max_orphans`
- `net.ipv4.tcp_workaround_signed_windows`
- `net.ipv4.tcp_rmem`
- `net.ipv4.tcp_wmem`
- `vm.max_map_count`

### Otimização dos parâmetros padrão do kernel do container
O TencentOS Server aumenta o valor padrão do `net.core.somaxconn` no namespace da rede do container para 4096, evitando assim a perda de pacotes causada por uma fila SYN completa em situações de alta simultaneidade.

## Otimização de desempenho
- O TencentOS Server otimiza os cálculos, o armazenamento e os subsistemas de rede:
- Otimiza a alocação de memória do XFS para resolver o alarme de falha kmem_alloc do XFS.
- Otimiza a alocação de memória dos pacotes de rede recebidos para resolver o uso excessivo de memória ao receber uma grande quantidade de pacotes UDP.
- Limita o uso da memória dos caches de página do sistema para manter o desempenho ideal do serviço e evitar erros de memória insuficiente (OOM, na sigla em inglês).

## Pacotes de software
- Personalizado com base nos pacotes de software CentOS 7.
- Os pacotes de software do modo de usuário são compatíveis com o CentOS 7 e podem ser usados diretamente no TencentOS Server.
- Atualizado e instalado via Yellowdog Updater Modified (YUM).
- Os pacotes de software no repositório Extra Packages for Enterprise Linux (EPEL) podem ser usados depois que o pacote epel-release for instalado via YUM.

## Correções de defeitos
- A funcionalidade Kdump é fornecida em caso de falha do sistema operacional.
- O patch dinâmico do kernel é compatível.

## Atualizações de segurança
O TencentOS Server oferece atualizações contínuas para aprimorar sua segurança e funcionalidades.
