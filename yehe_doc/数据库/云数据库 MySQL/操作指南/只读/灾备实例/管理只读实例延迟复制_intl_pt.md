Este documento descreve como definir a replicação atrasada para instâncias somente leitura e ativar/desativar a replicação no console do TencentDB for MySQL. Você pode definir a replicação atrasada (ou seja, o atraso entre uma instância somente leitura e sua instância de origem (source)) e selecionar a reprodução por posição em flashback ou identificador de transação global (GTID, na sigla em inglês) durante o atraso para reverter dados com eficiência e corrigir falhas.
- Replicação atrasada: você pode ativar e configurar o atraso de replicação entre uma instância somente leitura e sua instância de origem (source) na página de configuração do grupo somente leitura (RO, na sigla em inglês) ou na página de gerenciamento.
- Ativação/desativação da replicação: você pode ativar ou desativar manualmente a sincronização de dados entre uma instância somente leitura e sua instância de origem (source).

## Descrição da replicação atrasada
- Após ativar a replicação atrasada para uma instância somente leitura, ela será removida do grupo RO com seu peso definido como 0, e um alarme de remoção será acionado. Nesse momento, o tráfego não será encaminhado para a instância removida se o VIP RO for usado para acessar o grupo RO. Além disso, a instância removida só poderá ser acessada por meio do VIP da instância.
- Após a replicação atrasada ser desativada para uma instância somente leitura (o grupo RO correspondente ativou a remoção de instância somente leitura de replicação atrasada), o peso dessa instância no grupo RO será recuperado somente se o tempo de atraso dela for menor que o limite de atraso do grupo RO.  E um alarme de restauração será acionado ao mesmo tempo.
- Durante a reprodução por posição em flashback, você não pode reiniciar a instância, ajustar sua configuração, fazer upgrade da sua versão nem fazer upgrade da sua versão secundária do kernel.

## Ativação da replicação atrasada
>?Por padrão, a **Delayed Replication (Replicação atrasada)** fica **disabled (desativada)** para uma instância somente leitura. Se for ativada, o tempo de replicação atrasada será exibido.

### Ativação na página de configuração do grupo RO da instância somente leitura
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância de origem (source) para acessar a sua página de gerenciamento.
2. Nessa página, selecione a guia **Read-Only Instance (Instância somente leitura)**, localize o grupo RO desejado e clique em **Configuration (Configuração)** para acessar a página de configuração do grupo RO.
![](https://qcloudimg.tencent-cloud.cn/raw/87041c7addd9dcfd058b2d3f7c417625.png)
3. Na página de configuração do grupo RO, ative a **Delayed Replication (Replicação atrasada)**, defina o **Replication Delay (Atraso da replicação)** e clique em **OK**.
   Você pode definir a replicação atrasada e selecionar a reprodução por posição em flashback ou identificador de transação global (GTID) durante o atraso para reverter dados com eficiência e corrigir falhas.
   - **Replication Delay (Atraso da replicação)**: você pode configurar o tempo de replicação atrasada entre uma instância somente leitura e sua instância de origem (source). O intervalo de valores é de 1 a 259.200 segundos.
   - **Remove Delayed RO Instances (Remover instâncias RO atrasadas)**: essa opção indica se a política de remoção deve ser ativada. Se uma instância somente leitura for removida quando seu atraso exceder o limite, seu peso será definido automaticamentecomo 0 e os alarmes serão enviados. Para mais informações sobre como configurar o alarme de remoção de instância somente leitura e os destinatários, consulte [Políticas de alarme (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
   - **Delay Threshold (Limite de atraso)**: define um limite de atraso para a instância somente leitura. Quando o limite for excedido, a instância será removida do grupo somente leitura.
   - **Least RO Instances (Mínimo de instâncias RO)**: essa é a quantidade mínima de instâncias que devem ser retidas no grupo RO. Quando houver menos instâncias no grupo RO, mesmo que uma instância exceda o limite de atraso, ela não será removida.
   - **Assign Read Weight (Atribuir peso de leitura)**: o grupo RO fornece dois métodos de atribuição de peso: atribuição automática pelo sistema e atribuição personalizada. O valor do peso deve ser um número inteiro entre 0 e 100.
   - **Load Rebalancing (Rebalanceamento de carga)**:
    - A modificação do peso só afetará as novas cargas se o rebalanceamento estiver desativado. A operação não afeta as instâncias somente leitura acessadas por conexões persistentes existentes e não causa desconexão momentânea do banco de dados.
    - Se o rebalanceamento estiver ativado, todas as conexões com o banco de dados serão temporariamente desconectadas, e as cargas das conexões recém-adicionadas serão balanceadas de acordo com os pesos definidos.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c40a92c3a6dcc083ac92f01169b259ff.png"  style="zoom:50%;">

### Ativação na página de gerenciamento da instância somente leitura
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique no ID de uma instância somente leitura ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de detalhes.
2. Nessa página, clique em **Enable (Ativar)** em **Deployment Info (Informações de implantação)** > **Delayed Replication (Replicação atrasada)**.
![](https://qcloudimg.tencent-cloud.cn/raw/280f08c04f692445f51b1ab4aa556f58.png)
3. Na janela pop-up, defina o atraso e clique em **OK**.
>?O atraso varia de 1 a 259.200 segundos.
>As instâncias somente leitura no mesmo grupo RO compartilham o mesmo atraso de replicação. Se uma instância for modificada, as demais serão modificadas automaticamente ao mesmo tempo.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/32877ca9c8ab4bb3030bbb508c899374.png"  style="zoom:80%;">

## Modificação da replicação atrasada
### Modificação na página de configuração do grupo RO da instância somente leitura
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância de origem (source) para acessar a sua página de gerenciamento.
2. Nessa página, selecione a guia **Read-Only Instance (Instância somente leitura)**, localize o grupo RO desejado e clique em **Configuration (Configuração)** para acessar a página de configuração do grupo RO.
3. Na página de configuração do grupo RO, modifique **Replication Delay (Atraso da replicação)** e clique em **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/437d781e478652416c166449b4420910.png"  style="zoom:60%;">

### Modificação na página de gerenciamento da instância somente leitura
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique no ID de uma instância somente leitura na lista de instâncias para acessar a sua página de detalhes.
2. Nessa página, clique em **Modify (Modificar)** em **Deployment Info (Informações de implantação)** > **Delayed Replication (Replicação atrasada)**.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/5098762edf0e478942ad060c5bd80da5.png"  style="zoom:80%;">
3. Na janela pop-up, defina o atraso e clique em **OK**.

## Desativação da replicação atrasada
### Desativação na página de configuração do grupo RO da instância somente leitura
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância de origem (source) para acessar a sua página de gerenciamento.
2. Nessa página, selecione a guia **Read-Only Instance (Instância somente leitura)**, localize o grupo RO desejado e clique em **Configuration (Configuração)** para acessar a página de configuração do grupo RO.
3. Na página de configuração do grupo RO, clique em **Delayed Replication (Replicação atrasada)** e clique em **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9191e1c61694da2970323b59a21c59f3.png"  style="zoom:70%;">

### Desativação na página de gerenciamento da instância somente leitura
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique no ID de uma instância somente leitura na lista de instâncias para acessar a sua página de detalhes.
2. Nessa página, clique em **Disable (Desativar)** em **Deployment Info (Informações de implantação)** > **Delayed Replication (Replicação atrasada)**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/5f3a33f7b23513b8766eb62455406478.png"  style="zoom:80%;">
3. Na caixa de diálogo pop-up, verifique se tudo está correto e clique em **OK**.
>?Se a replicação atrasada estiver desativada, o tempo da replicação atrasada será de 0 segundos, ou seja, a sincronização de dados em tempo real será retomada entre a instância somente leitura e sua instância de origem (source). 
> 

## Ativação da replicação de dados
>?O **Replication Status (Status de replicação)** de uma instância somente leitura é **Normal** por padrão. Se você definir a replicação atrasada e excluir dados acidentalmente durante o período da replicação atrasada, é possível restaurar a instância somente leitura para a posição especificada ou o GTID do arquivo de binlog para implementar a restauração rápida dos dados.
>
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique no ID de uma instância somente leitura na lista de instâncias para acessar a sua página de detalhes.
2. Nessa página, clique em **Enable (Ativar)** em **Deployment Info (Informações de implantação)** > **Replication Status (Status de replicação)**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/29703db36415992fda7e1767a7b830e8.png"  style="zoom:80%;">
3. Na janela pop-up, clique em **OK**.
>? Ativada a replicação, a sincronização de dados entre a instância somente leitura e a instância de origem (source) será retomada.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ab58491f328ffe447f8790105699f13b.png"  style="zoom:80%;">
4. Você também pode selecionar **Replay by Flashbacked Position (Reproduzir por posição em flashback)** em **Deployment Info (Informações de implantação)** > **Operation (Operação)**. Em seguida, os dados podem ser restaurados para o ponto de tempo especificado ou o GTID correspondente. Após a restauração, a replicação da instância somente leitura será desativada até que o modo de início seja alterado para **Replicate all (Replicar tudo)**.
    - Time (Hora): você pode selecionar um ponto de tempo entre a hora de término da replicação e a hora atual da instância de origem (source).
    - GTID: você pode selecionar todos os logs após o binlog não aplicado. Se o GTID for selecionado, os dados serão replicados até que o GTID especificado seja alcançado.
O comprimento da instância `server_uuid` é fixado em 36 bits, e o GTID deve estar no formato `server_uuid:transaction_id`.
>!
>- Se a posição do binlog já tiver sido aplicada na instância somente leitura ou estiver após a posição da instância de origem (source), a replicação não será ativada.
>- Quando você ativar a replicação, se houver algum ponto de interrupção no binlog, ela não será ativada.
>- Para evitar o uso excessivo do espaço em disco de uma instância somente leitura atrasada quando a replicação estiver desativada para ela, o thread de E/S da instância somente leitura será pausado quando seu espaço em disco disponível cair abaixo de 5 GB.
> 
<img src="https://qcloudimg.tencent-cloud.cn/raw/92671ad35d5ef5acbfdf3bfbb47f967a.png"  style="zoom:85%;">
5. Durante o processo de reprodução por posição em flashback, você pode clicar em **Replaying (Reprodução)** após **Replication Status (Status de replicação)** para consultar e atualizar os detalhes da tarefa.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/39274c3aa8e92e6c4dfe0a242de0392e.png"  style="zoom:85%;">
6. Após a conclusão da replicação, clique em **Enable (Ativar)** após **Replication Status (Status da replicação)** e a instância somente leitura poderá continuar a replicar.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/b27f75181ebae1e8c9b833762ba9388d.png"  style="zoom:85%;">


## Desativação da replicação de dados
>?
>- Somente após ativar a replicação atrasada, ela pode ser desativada; caso contrário, o botão **Disable (Desativar)** ficará inativo.
>- Depois que a replicação for desativada, os threads de E/S e SQL também serão encerrados.
>
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique no ID de uma instância somente leitura na lista de instâncias para acessar a sua página de detalhes.
2. Nessa página, clique em **Disable (Desativar)** em **Deployment Info (Informações de implantação)** > **Replication Status (Status de replicação)**.
<img src="https://main.qcloudimg.com/raw/8921d228b70bf42ca5120d6fcf44e92c.png"  style="zoom:85%;">
3. Na caixa de diálogo pop-up, verifique se tudo está correto e clique em **OK**.

## Perguntas frequentes
#### Como obtenho o GTID?
Recomendamos que você execute o comando `flush log` para obter o arquivo binlog para localizar a posição e o GTID da operação incorreta.

#### Como verificar a exibição do atraso?
Você pode acessar o atraso entre uma instância somente leitura e sua instância de origem (source) na página de detalhes da instância no [console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/0b975dfca0c575735b94445f11e30d67.png)

#### Como verifico as informações da tarefa de reprodução por posição em flashback?
Você pode checar o progresso e os detalhes da tarefa na página da lista de tarefas no [console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/f3c0cb3ed4d9488c66fc02cbd96b770d.png)

