Considere as informações a seguir e mantenha sua empresa intacta ao usar o espelho de tráfego.
- Atualmente, o espelho de tráfego está em teste beta. Para solicitá-lo, [envie um tíquete](https://console.cloud.tencent.com/workorder/category). Recomendamos salvar o link do console do Espelho de tráfego, para que você possa fazer login no console sem precisar solicitar novamente.
- O espelho de tráfego consome recursos do CVM como CPU, memória e largura de banda proporcionalmente.
  O tráfego espelhado é contabilizado para a largura de banda da instância. O impacto depende do volume e do tipo de tráfego. Considere como exemplo você espelhar uma interface de rede que tem 1 Gbps de tráfego de entrada e 1 Gbps de tráfego de saída. Nesse caso, a instância precisa lidar com 1 Gbps de tráfego de entrada e 3 Gbps de tráfego de saída (1 Gbps para o tráfego de saída, 1 Gbps para o tráfego de entrada espelhado e 1 Gbps para o tráfego de saída espelhado).
- Os Logs de fluxo não capturam o tráfego espelhado.
- Limites em relação a um grupo de segurança:
 - Origem: o tráfego espelhado não está sujeito às políticas do grupo de segurança. 
 - Destino: o tráfego recebido está sujeito às políticas do grupo de segurança.
- O espelho de tráfego não está disponível para:
 - Protocolo de resolução de endereço
 - DHCP
 - Serviço de metadados de instância
 - NTP
 - Ativação do Windows
- O espelho de tráfego permite a coleta de tráfego de um ENI nos seguintes tipos de CVM:
S1 padrão, S2 padrão, S3 padrão, Memória otimizada M1, Memória otimizada M2, Memória otimizada M3, Alta E/S I1, Alta E/S I2, Alta E/S I3, Computação C2, Computação C3, Computação com rede otimizada CN3 e Big Data D1.

