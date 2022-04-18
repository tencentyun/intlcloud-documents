Este documento descreve como criar políticas de alarme e associar objetos de alarme no console do Cloud Monitor.

## Visão geral
Você pode criar políticas de alarme para acioná-los e enviar notificações quando o status do serviço da Tencent Cloud mudar. As políticas de alarme criadas podem determinar se um alarme precisa ser acionado de acordo com a diferença entre o valor da métrica de monitoramento e o limite determinado em intervalos.
É possível adotar medidas preventivas ou corretivas apropriadas, em tempo hábil, quando o alarme for disparado em função de alteração no status do produto. Portanto, alarmes criados corretamente podem ajudá-lo a melhorar a robustez e a confiabilidade de seus aplicativos. Para obter mais informações sobre alarmes, consulte [Criação de política de alarme](https://intl.cloud.tencent.com/document/product/248/38916) no Cloud Monitor.

Se quiser enviar uma mensagem de alarme para um status específico de um produto, primeiro você precisa criar uma política de alarme, que possui três componentes obrigatórios: o nome, o tipo e a condição de disparo do alarme. Cada política de alarme é um conjunto de condições de disparo de alarme na relação lógica "or", ou seja, desde que uma das condições de disparo seja satisfeita, o alarme será disparado. A notificação de alarme será enviada a todos os usuários associados à política de alarme. Eles podem tomar as medidas adequadas quando receberem a notificação.

>!Certifique-se de ter definido o destinatário do alarme padrão; caso contrário, a política de alarme padrão do TencentDB não conseguirá enviar notificações.

## Instruções
### Criação de uma política de alarme
Faça login no console do [Cloud Monitor] (https://console.cloud.tencent.com/monitor/overview) e selecione **Alarm Configuration (Configuração de alarme)** > [**Alarm Policy (Política de alarme)** na barra lateral esquerda.
2. Na lista de políticas de alarme, clique em **Create (Criar)**.
3. Na página **Create Alarm Policy (Criar política de alarme)**, defina o nome da política, o tipo de política, o objeto de alarme e a condição de disparo.
 - **Policy Type (Tipo de política)**: divide-se em monitoramento de origem e monitoramento de réplica, aplicáveis ​​a diferentes tipos de instâncias.
    - Implantar monitoramento na origem: quando a instância monitorada é uma instância de origem que não é uma réplica de nenhuma instância, os dados de monitoramento relacionados à replicação são inválidos para a origem e os threads de E/S e SQL são desabilitados. Os dados de monitoramento relacionados à replicação são válidos e os threads de E/S e SQL podem ser habilitados somente quando a instância monitorada é uma recuperação de desastre ou uma réplica somente leitura.
    - Implantar o monitoramento na réplica: a instância de origem de dois ou três nós e a instância de recuperação de desastres vêm em uma arquitetura de origem/réplica por padrão. Como resultado, os dados de monitoramento relacionados à replicação são válidos para a réplica somente quando a instância monitorada é uma instância de origem ou de recuperação de desastres. Esses dados de monitoramento podem refletir a distância e o tempo de atraso da replicação entre a origem ou a instância de recuperação de desastres e seus nós de réplica ocultos. É recomendável ficar atento a esses dados de monitoramento da réplica. Se a instância de recuperação de desastres ou de origem falhar, seus nós de réplica ocultos monitorados podem ser promovidos para a instância de origem rapidamente.
  - **Alarm Object (Objeto de alarme)**: a instância a ser associada ao alarme da política. Você pode encontrar a instância desejada selecionando a região onde ela está localizada ou pesquisando seu ID.
 - **Trigger Condition (Condição de disparo)**: um disparo de alarme é uma condição semântica composta por métrica, comparação, limite, período estatístico e duração. Por exemplo, se a métrica for a utilização do disco, a comparação for >, o limite for 80%, o período estatístico for 5 minutos e a duração for dois períodos estatísticos, os dados sobre a utilização do disco de um banco de dados serão coletados uma vez a cada cinco minutos e um alarme será acionado se a utilização do disco exceder 80% por duas vezes consecutivas.
 - **Configure Alarm Notification (Configurar notificação de alarme)**: modelos padrão do sistema e modelos personalizados são suportados. Cada política de alarme pode ser associada a até três modelos de notificação.
4. Depois de confirmar todas as informações, clique em **Complete (Concluir)**.

### Associar objetos de alarmes
Depois que a política de alarme for criada, você poderá associar alguns objetos de alarme a ela. Quando um objeto de alarme satisfizer uma condição de disparo de alarme, uma notificação de alarme será enviada.
1. Na lista [política de alarme](https://console.cloud.tencent.com/monitor/alarm2/policy), clique no nome de uma política para entrar na respectiva página de gerenciamento.
2. Clique em **Add Object (Adicionar objeto)** na seção **Alarm Object (Objeto de alarme)**.
![](https://main.qcloudimg.com/raw/00833b7ad2a481ec65b1eb14c0d2cad4.png)
3. Na caixa de diálogo pop-up, selecione os objetos de alarme a serem associados e clique em **OK**.


