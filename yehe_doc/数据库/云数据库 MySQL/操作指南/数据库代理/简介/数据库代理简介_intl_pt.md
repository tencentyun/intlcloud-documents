
Este documento descreve os recursos e casos de uso do serviço de proxy de banco de dados no TencentDB for MySQL.

O proxy de banco de dados é um serviço de proxy de rede entre o serviço TencentDB e o serviço de aplicativo. Ele é usado para efetuar proxy de todas as solicitações quando o serviço de aplicativo acessa o banco de dados.
O endereço de acesso do proxy do banco de dados é independente do endereço de acesso do banco de dados original. As solicitações que chegam no endereço do proxy são todas retransmitidas por meio do cluster do proxy para acessar os nós de origem e de réplica do banco de dados. As solicitações de leitura/gravação são separadas para que as solicitações de leitura sejam encaminhadas para instâncias somente leitura, o que reduz a carga do banco de dados de origem.
>?Atualmente, o serviço de proxy de banco de dados está em fase de teste beta e pode ser usado gratuitamente.
>
## Funcionalidades
- **Alta estabilidade**
O proxy de banco de dados adota a arquitetura de cluster para implantação, com vários nós garantindo failover suave.
- **Isolamento robusto**
O proxy de banco de dados usa recursos independentes para fornecer serviço de proxy para a instância atual (os recursos de diferentes proxies são isolados e não compartilhados).
- **Desempenho ultra-alto**
Cada proxy pode processar até 100.000 solicitações por segundo.
- **Capacidade de escalar de maneira rápida e conveniente**
Você pode adicionar dinamicamente de 1 a 60 nós de proxy (apenas 6 nós são suportados durante o teste beta).
- **Monitoramento de desempenho abrangente)**
As métricas de desempenho são monitoradas no segundo nível, como o número de solicitações de leitura/gravação, CPU e memória. O número de proxies pode ser ajustado de acordo com os [dados de monitoramento](https://intl.cloud.tencent.com/document/product/236/42055) e planejamento de negócios.
- **Recarga automática**
Quando uma instância de origem é alternada, ou sua configuração é alterada, ou uma instância somente leitura é adicionada/removida, o proxy de banco de dados pode recarregar automaticamente a configuração sem causar desconexões ou reinicializações de rede.   
- **Permite a [separação automática de leitura/gravação](https://intl.cloud.tencent.com/document/product/236/42054)**
Ele pode reduzir efetivamente a carga de leitura da instância de origem quando o recurso de separação de leitura/gravação do proxy de banco de dados está habilitado. Instâncias somente leitura podem ser adicionadas para dimensionar horizontalmente o cluster de banco de dados e implementar automaticamente a separação de leitura/gravação, o que elimina a complexidade de separar manualmente as solicitações de leitura e gravação do negócio. Isso é especialmente adequado para cenários com alta carga de leitura.
Por exemplo, depois que o recurso de separação de leitura/gravação do proxy de banco de dados é habilitado, apenas um endereço de conexão de proxy precisa ser configurado no aplicativo. Esse endereço implementará automaticamente a separação de leitura/gravação e enviará solicitações de leitura para instâncias somente leitura e solicitação de gravação para a instância de origem. Mesmo se você adicionar ou remover instâncias somente leitura, não será necessário ajustar as configurações do aplicativo.

## Casos de uso
- Negócios com baixo desempenho quando há um grande número de conexões não persistentes.
- As empresas usam várias instâncias somente leitura e a separação de leitura/gravação é implementada manualmente nos aplicativos, resultando em custos e riscos de manutenção mais altos.
- Alta carga de instâncias causado por muitas conexões.

