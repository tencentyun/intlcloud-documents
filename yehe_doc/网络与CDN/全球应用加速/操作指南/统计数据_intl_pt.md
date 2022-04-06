Faça login no [console do GAAP](https://console.cloud.tencent.com/gaap) e selecione **Statistics (Estatísticas)** na barra lateral esquerda. A página **Statistics (Estatísticas)** exibe os dados nas quatro dimensões a seguir: conexão, grupo de conexões, listener e servidor de origem.

## Conexão

Você pode exibir as estatísticas de conexão, conforme mostrado abaixo:

- **Connection Type (Tipo de conexão)**: conexão única, por padrão. Você também pode selecionar um grupo de conexões que foi criado anteriormente.
- **Connection (Conexão)**: selecione uma conexão do **Access Management (Gerenciamento de acesso)** ou do grupo de conexões.
- **Data Type (Tipo de dados)**: selecione um ou todos os tipos de dados (largura de banda, tráfego, volume de pacotes, conexões simultâneas, HTTP QPS, HTTPS QPS, latência e taxa de perda de pacotes).
- **Time Period (Período)**: selecione um período.
- **Time Granularity (Granularidade de tempo)**: selecione uma granularidade de tempo. O tempo máximo de consulta é de 15 dias se você selecionar a granularidade de 1 minuto, 31 dias para a granularidade de 5 minutos, 93 dias para a granularidade de 1 hora e 186 dias para a granularidade de 1 dia.

![](https://qcloudimg.tencent-cloud.cn/raw/4d3f9eaea3e2ca9442ec8cfabf0ad73f.jpg)

## Grupo de conexões

Você pode exibir as estatísticas do grupo de conexões, conforme mostrado abaixo:

- **Connection Group (Grupo de conexões)**: selecione um ou mais grupos de conexões.
- **Data Type (Tipo de dados)**: selecione um ou todos os tipos de dados (largura de banda e tráfego).
- **Time Period (Período)**: selecione um período.
- **Time Granularity (Granularidade de tempo)**: selecione uma granularidade de tempo. O tempo máximo de consulta é de 15 dias se você selecionar a granularidade de 1 minuto, 31 dias para a granularidade de 5 minutos, 93 dias para a granularidade de 1 hora e 186 dias para a granularidade de 1 dia.

![](https://qcloudimg.tencent-cloud.cn/raw/fce7e20b2dcaa474095a117380f41e85.jpg)

## Listener

Você pode exibir as estatísticas de listener, conforme mostrado abaixo:

- **Connection/Connection Group (Conexão/Grupo de conexões)**: selecione uma conexão ou grupo de conexões para o listener.
- **Listener**: selecione um listener.
- **Data Type (Tipo de dados)**: selecione um ou todos os tipos de dados (largura de banda, tráfego, volume de pacotes e conexões simultâneas).
- **Time Period (Período)**: selecione um período.
- **Time Granularity (Granularidade de tempo)**: selecione uma granularidade de tempo. O tempo máximo de consulta é de 15 dias se você selecionar a granularidade de 1 minuto, 31 dias para a granularidade de 5 minutos, 93 dias para a granularidade de 1 hora e 186 dias para a granularidade de 1 dia.

![](https://qcloudimg.tencent-cloud.cn/raw/b1975214d1f82e89dcded5c4280d0bb9.jpg)

## Servidor de origem

Você pode exibir as estatísticas do status de integridade do servidor de origem, conforme mostrado abaixo:

- **Connection/Connection Group (Conexão/Grupo de conexões)**: selecione uma conexão ou grupo de conexões para o servidor de origem.
- **Listener**: selecione um listener para o servidor de origem.
- **Origin (Origem)**: selecione um servidor de origem.
- **Time Period (Período)**: selecione um período.
- **Time Granularity (Granularidade de tempo)**: selecione uma granularidade de tempo. O tempo máximo de consulta é de 15 dias se você selecionar uma granularidade de 1 minuto e 31 dias para uma granularidade de 5 minutos.

![](https://qcloudimg.tencent-cloud.cn/raw/75ce6339c8d51048a066fd3df481a642.jpg)

## Exportação de dados

Acesse a página **Statistics (Estatísticas)** e clique no ícone de download para exportar os dados.
![](https://qcloudimg.tencent-cloud.cn/raw/7646c6fb333f613b5dc1059de73b9847.jpg)

## Configuração de política de alarme
Acesse a página [Statistics (Estatísticas)](https://console.cloud.tencent.com/gaap/data) e clique em **Configure Alarm (Configurar alarme)** no canto superior direito para configurar uma política de alarme. Para mais detalhes, consulte [Monitoramento do acesso em nuvem](https://intl.cloud.tencent.com/document/product/608/17541).
