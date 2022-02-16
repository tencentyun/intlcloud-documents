O TcaplusDB fornece várias métricas de monitoramento de desempenho para ajudá-lo a monitorar e manter-se atualizado com as informações de execução. Ele permite o monitoramento de tabelas e proporciona uma visão de monitoramento independente para cada tabela, a fim de facilitar a consulta.
Você pode fazer login no [console do TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/table), clicar em um ID de tabela para acessar a página de gerenciamento da tabela e acessar a guia **Table Monitoring (Monitoramento de tabela)** para exibir a visualização de monitoramento.

>
>- Você também pode obter métricas de monitoramento de instâncias chamando a API de dados de monitoramento do TcaplusDB no Cloud Monitor.
>- Atualmente, você pode exibir os dados de monitoramento do TcaplusDB dos últimos 60 dias.

## Métricas de monitoramento de tabelas
O Tencent Cloud Monitor fornece as seguintes métricas de monitoramento para tabelas do TcaplusDB:

| Nome da métrica | Parâmetro | Descrição | Unidade |
| ----------------- | ---------------- | ------------------------------------------------------------ | -------- |
| Taxa de erros média | Average Error Rate | Porcentagem média de erros de operação da tabela | % |
| Taxa de erros geral | General Error Rate | Porcentagem geral de erros de operação da tabela | % |
| Unidades de capacidade de leitura real | Actual Read Capacity Units | Quantidade de unidades de capacidade de leitura real da tabela | Unidade/s |
| Latência de leitura média | Average Read Latency | Latência média na leitura de dados | us |
| Taxa de erros do sistema | System Error Rate | Porcentagem de erros do sistema | % |
| Capacidade de armazenamento | Storage Capacity | Capacidade de armazenamento usada por tabela | KB |
| Latência de gravação média | Average Write Latency | Latência média na gravação de dados | us |
| Unidades de capacidade de gravação real | Actual Write Capacity Units | Quantidade de unidades de capacidade de gravação real da tabela | Unidade/s |
