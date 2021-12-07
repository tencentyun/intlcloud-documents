## Informações gerais
Ao realizar o teste de estresse no CLB, é possível encontrar falhas de conexão causadas por muito TIME-WAIT (todas as portas são ocupadas em pouco tempo) de cliente. Abaixo estão os motivos e soluções:

## Descrição de parâmetro Linux
**tcp_timestamps:** se deseja ativar os carimbos de data/hora do TCP. Um carimbo de data/hora é negociado no handshake de três vias do TCP. Se qualquer uma das partes não oferecer suporte a esse parâmetro, ele não será usado nesta conexão.
**tcp_tw_recycle:** se deve ativar a reutilização do estado TIME-WAIT do TCP.
**tcp_tw_reuse:** quando habilitado, as conexões no estado TIME_WAIT que excedem 1 segundo podem ser reutilizadas diretamente.

## Análise de causa
O cliente tem muito TIME_WAIT porque ele fecha conexões proativamente. Quando o cliente fecha uma conexão, a conexão entrará no estado TIME_WAIT e será reutilizada após 60 segundos por padrão. Neste caso, você pode habilitar os parâmetros `tcp_tw_recycle` e `tcp_tw_reuse` para facilitar a reutilização de conexões no estado TIME_WAIT.
Se `tcp_timestamps` estiver atualmente desabilitado no CLB, os parâmetros`tcp_tw_recycle` e `tcp_tw_reuse` habilitados pelo cliente não terão efeito e as conexões no estado TIME_WAIT não poderão ser reutilizadas rapidamente. O seguinte descreve alguns parâmetros do Linux e os motivos pelos quais `tcp_timestamps` não pode ser habilitado no CLB:

1. tcp_tw_recycle e tcp_tw_reuse só têm efeito quando tcp_timestamps está habilitado.

2. tcp_timestamps e tcp_tw_recycle não podem ser habilitados ao mesmo tempo, porque o cliente da rede pública pode falhar ao acessar o servidor através do NAT Gateway. As razões são as seguintes:

Se tcp_tw_recycle e tcp_timestamps estiverem ativados, o carimbo de data/hora nas solicitações de conexão de soquete do mesmo IP de origem (mesmo servidor) deve ser incremental em 60 segundos. Tomando o kernel 2.6.32 como exemplo, os detalhes são os seguintes:

![](https://mc.qcloudimg.com/static/img/2199611fec3b323a7b8fd3bb38459913/Linux1.png)

> tmp_opt.saw_tstamp: este soquete suporta tcp_timestamp
sysctl_tw_recycle: tcp_tw_recycle foi habilitado para este servidor
TCP_PAWS_MSL: 60s; a última comunicação TCP do IP de origem ocorreu em 60 segundos
TCP_PAWS_WINDOW: 1; o carimbo de data/hora da última comunicação TCP do IP de origem é maior do que o desta comunicação TCP

3. No CLB (Camada 7), tcp_timestamps é desativado porque o cliente da rede pública pode falhar ao acessar o servidor através do NAT Gateway, conforme mostrado no exemplo abaixo:

a. Um quíntuplo ainda está no estado TIME_WAIT. Na política de alocação de portas do NAT Gateway, o mesmo quíntuplo é reutilizado no dobro do tempo de vida máximo do segmento (2MSL), e um pacote SYN é enviado.

b. Quando tcp_timestamps estiver habilitado e as duas condições a seguir forem atendidas, o pacote SYN será descartado (porque a opção carimbo de data/hora está habilitada e o pacote é considerado antigo).
i. Carimbo de data/hora da última vez > Carimbo de data/hora desta vez
ii. 	Os pacotes são recebidos em 24 dias (o carimbo de data/hora é de 32 bits e o carimbo de data/hora é atualizado uma vez a cada 1 milissegundo por padrão no Linux. O carimbo de data/hora reinicia após 24 dias).
Observação: Este problema é mais óbvio em dispositivos móveis porque os clientes compartilham IPs de rede pública limitados sob o NAT Gateway do ISP e um quíntuplo pode ser reutilizado em 2MSL. Os carimbos de data/hora enviados de clientes diferentes não podem ser incrementais.
Tomando o kernel 2.6.32 como exemplo, os detalhes são os seguintes:

![](https://mc.qcloudimg.com/static/img/6228a7dc25c670d4d2fbddc9ea400779/Linux2.png)

> rx_opt-> ts_recent: carimbo de data/hora da última vez
rx_opt-> rcv_tsval: carimbo de data/hora recebido neste momento
get_seconds (): hora atual
rx_opt-> ts_recent_stamp: hora em que o pacote anterior foi recebido

## Solução
Se o cliente tiver muito TIME_WAIT, confira as soluções abaixo:

**1. O HTTP usa conexões não persistentes (Conexão: fechar). Nesse caso, o CLB fecha proativamente a conexão e o cliente não gera TIME_WAIT**.

**2. Se o cenário exigir uma conexão persistente, habilite a opção SO_LINGER do soquete e use RST para fechar a conexão para evitar o estado TIME_WAIT e obter uma rápida reutilização da porta**.
