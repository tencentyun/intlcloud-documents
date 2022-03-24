O **monitoramento e alarme** ajudam a garantir a alta confiabilidade, a alta disponibilidade e o alto desempenho dos CVMs. Este documento descreve as funcionalidades de monitoramento e de alarme do CVM. Para obter mais informações, consulte a documentação do [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248?).

## Visão geral
O monitoramento e o alarme do CVM apresentam dados completos de monitoramento de diferentes métricas importantes do CVM em tempo real. Com essa funcionalidade, você consegue obter um amplo entendimento do uso, desempenho e status de execução do recurso da instância do CVM. Você também pode configurar limites de alarme personalizados e regras de notificação.

## Funcionalidades básicas
Você pode acessar as seguintes funcionalidades de monitoramento e de alarmes do CVM no console do Cloud Monitor:

| Componente | Capacidade | Funcionalidades principais |
| ----- | -------------- | --------------------------------------- |
| [Visão geral do Monitor](https://console.cloud.tencent.com/monitor/overview)  | Exibe as informações gerais de monitoramento para os serviços do Tencent Cloud          | Fornece informações gerais e alarmes para os serviços do Tencent Cloud                     |
| [Política de alarmes](https://console.cloud.tencent.com/monitor/policylist)  | Exibe a lista de políticas de alarmes personalizadas   | Compatível com a configuração de alarmes para o CVM         |
| [Cloud Virtual Machine](https://console.cloud.tencent.com/monitor/product/cvm) | Exibe as informações específicas de monitoramento do CVM      | Permite que você visualize os dados de monitoramento do CVM |
| [Painel](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=8) | Exibe o painel de controle de monitoramento personalizado | Apresenta graficamente os dados de monitoramento para facilitar a análise métrica dinâmica |
| [Monitoramento personalizado](https://console.cloud.tencent.com/monitor/indicator-manage)| Exibe as métricas de monitoramento personalizadas | Permite a visualização das métricas de monitoramento personalizadas predefinidas e dos dados relatados            |
| [Monitoramento de tráfego](https://console.cloud.tencent.com/monitor/flow) | Exibe o monitoramento de tráfego           || Permite a visualização do seu uso geral da largura de banda                              |

Para obter mais informações sobre o Cloud Monitor, consulte a [Visão geral do produto](https://intl.cloud.tencent.com/document/product/248/32799)

## Casos de uso
- **Gerenciamento diário:** efetue login no console do Cloud Monitor e exiba o status de execução de cada produto monitorado.
- **Solução de problemas de exceções:** o Cloud Monitor enviará notificações de alarme imediatamente quando os dados de monitoramento atingirem o limite de alarme, para que você consiga resolver o problema.
- **Expansão gradativa:** você pode configurar políticas de alarme para largura de banda, quantidade de conexões, utilização de disco e outros itens de monitoramento para verificar o status geral dos seus serviços do Tencent Cloud. Você receberá notificações de alarme quando ocorrer uma sobrecarga de serviços e poderá expandir seus CVMs proporcionalmente.

## Itens de monitoramento
Para avaliar o desempenho da instância, você deve ao menos monitorar os seguintes itens:

| Item de monitoramento | Métrica de monitoramento |
|---------|---------|
| Utilização da CPU | cpu_usage |
| Utilização da memória | mem_usage |
| Largura de banda de saída da rede privada | lan_outtraffic |
| Largura de banda de entrada da rede privada | lan_intraffic |
| Largura de banda de saída da rede pública | wan_outtraffic |
| Largura de banda de entrada da rede pública | wan_intraffic |
| Utilização do disco | disk_usage |
| Tempo de espera de E/S do disco | disk_io_await |

## Dados de monitoramento
- **Intervalo de monitoramento:** o Cloud Monitor fornece dados de monitoramento em diferentes granularidades estatísticas, incluindo 1 minuto, 5 minutos, 1 hora e 1 dia. O CVM aceita a granularidade de monitoramento de 1 minuto, o que significa que os dados são coletados a cada 1 minuto. O intervalo padrão é de 5 minutos.
- **Armazenamento de dados:** os dados de monitoramento em uma granularidade de 1 minuto, 5 minutos e 1 hora serão mantidos por 31 dias; os dados de monitoramento em uma granularidade de 1 dia serão mantidos por meio ano.
- **Exibição de alarme:** os dados são exibidos em gráficos de fácil leitura. O console do Cloud Monitor exibe os dados de monitoramento de todos os produtos para fornecer uma visão geral completa do status de execução deles.
- **Configurações de alarme:** você pode estabelecer limites para as métricas de monitoramento. Quando a condição for atendida, a notificação de alarme será enviada ao grupo destinatário imediatamente. Para obter mais informações, consulte [Configuração de políticas de alarme](https://intl.cloud.tencent.com/document/product/248/38908).
- **Configurações do painel:** você pode criar um painel de métricas de monitoramento para analisar dinamicamente as métricas anormais e exibir sua mudança em tempo real, a fim de expandir imediatamente os recursos. Para obter mais informações, consulte [Criação de um painel](https://intl.cloud.tencent.com/document/product/248/38468).
