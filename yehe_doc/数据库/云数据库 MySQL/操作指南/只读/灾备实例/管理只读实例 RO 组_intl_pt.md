
## Visão geral
O TencentDB for MySQL permite que você crie uma ou mais instâncias somente leitura para formar um grupo somente leitura (RO, na sigla em inglês), que é adequado para a separação de leitura/gravação e cenários de aplicações de “uma fonte e várias réplicas”, além de conseguir melhorar muito a capacidade de carga de leitura do seu banco de dados.

Um grupo RO é um conjunto de instâncias somente leitura que compartilham o mesmo endereço de rede privada. Você pode definir seus pesos para equilibrar a carga de tráfego, definir a política de remoção de instâncias somente leitura atrasadas e realizar outras configurações. Você pode implantar um grupo RO conforme necessário e enviar as solicitações de leitura correspondentes para instâncias somente leitura de acordo com determinadas regras. Além disso, você pode implementar a recuperação de desastres configurando várias instâncias somente leitura no mesmo grupo RO.

## Pré-requisitos
- Primeiro, é necessário criar uma instância de origem (source), para que seja possível criar uma instância somente leitura. Para mais informações, consulte [Guia de aquisição](https://intl.cloud.tencent.com/document/product/236/5160).
- Antes do uso, é necessário inicializar uma instância do TencentDB for MySQL. Para mais informações, consulte [Inicialização de instância do TencentDB for MySQL](/doc/product/236/3128).

## Instruções
### Criação de grupo RO
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de gerenciamento.
2. Clique em **Add Read-Only Instance (Adicionar instância somente leitura)** na seção **Instance Architecture Diagram (Diagrama de arquitetura de instância)** na guia **Instance Details (Detalhes da instância)** ou clique em **Create (Criar)** na guia **Read-Only Instance (Instância somente leitura)**.
![](https://main.qcloudimg.com/raw/83e817ae1b9205d6cdf061684f7d3c12.png)
3. Na página de aquisição exibida, especifique as seguintes configurações de instância somente leitura, verifique se tudo está correto e clique em **Buy Now (Comprar agora)**.
 - **Specify RO Group (Especificar grupo RO)**: selecione **Create RO group (Criar grupo RO)**. Se várias instâncias forem adquiridas ao mesmo tempo, todas elas serão atribuídas a esse novo grupo RO e, por padrão, seus pesos serão alocados pelo sistema automaticamente.
 - **RO Group Name (Nome do grupo RO)**: o nome do grupo RO não precisa ser exclusivo e pode conter até 60 letras, dígitos, hifens, sublinhados e pontos.
 - **Remove Delayed RO Instances (Remover instâncias RO atrasadas)**: essa opção indica se a política de remoção deve ser ativada. Se uma instância somente leitura for removida, seu peso será automaticamente definido como 0.
 Se uma instância somente leitura for removida quando seu atraso exceder o limite, ela ficará inativa, seu peso será automaticamente definido como 0 e serão enviados alarmes. Para mais informações sobre como configurar o alarme de remoção de instância somente leitura e os destinatários, consulte [Políticas de alarme (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457). A instância será colocada de volta no grupo RO quando seu atraso ficar abaixo do limite.
 Independentemente se a remoção de instância somente leitura atrasada estiver ativada, uma instância somente leitura que foi removida devido a uma falha de instância se juntará novamente ao grupo RO quando for reparada.
 - **Delay Threshold (Limite de atraso)**: define um limite de atraso para a instância somente leitura. Quando o limite for excedido, a instância será removida do grupo RO.
 - **Least RO Instances (Mínimo de instâncias RO)**: essa é a quantidade mínima de instâncias que devem ser retidas no grupo RO. Quando houver menos instâncias no grupo RO, mesmo que uma instância exceda o limite de atraso, ela não será removida.
 - **Assign Read Weight (Atribuir peso de leitura)**: é atribuído pelo sistema.
 - **Billing Mode (Modo de faturamento)**: instâncias somente leitura são com pagamento conforme o uso.
![](https://main.qcloudimg.com/raw/a8f80ce3f01cbaa1847978bec455aa0d.png)
 - **Region (Região)**: por padrão, é a mesma da instância de origem (source).
 - **Database Version (Versão do banco de dados)**: por padrão, é a mesma da instância de origem (source).
 - **Architecture (Arquitetura)**: é um nó único. Embora a arquitetura de nó único seja econômica, há riscos de pontos únicos de falhas. Recomendamos que você adquira pelo menos duas instâncias somente leitura no grupo RO de suas operações que exigem alta disponibilidade.
 - **Data Replication Mode (Modo de replicação de dados)**: por padrão, é o mesmo da instância de origem (source).
 - **AZ (Zona de disponibilidade)**: se houver várias AZs na região atual, você poderá escolher uma, conforme necessário.
>?O atraso da rede em AZs na mesma região, em regiões diferentes e em regiões fora da China Continental é de cerca de alguns milissegundos, dezenas de milissegundos e mais de 100 milissegundos, respectivamente. Portanto, você deve escolher uma AZ com cuidado.
5. Retorne à lista de instâncias. O status da instância criada é **Delivering (Em entrega)**. Se o status mudar para **Running (Em execução)**, a instância somente leitura foi criada com êxito.

### Configuração de grupo RO
Na página de configuração do grupo RO, você pode configurar as informações básicas do grupo, como o ID, o nome, a replicação atrasada, a política de remoção, o limite de atraso, o mínimo de instâncias somente leitura e o peso de leitura.
>?
>- As instâncias somente leitura em um grupo RO podem usar especificações diferentes e seus pesos de tráfego de leitura também podem ser diferentes.
>- As instâncias somente leitura no mesmo grupo RO podem ter datas de expiração e modos de faturamento diferentes.
>- Após ativada, a replicação atrasada terá efeito para todas as instâncias somente leitura nesse grupo RO, mas não alterará seus status de replicação.
>- A opção de atraso de replicação será exibida somente depois que a replicação atrasada for ativada.
>
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância de origem (source) para acessar a sua página de gerenciamento.
2. Nessa página, selecione a guia **Read-Only Instance (Instância somente leitura)**, localize o grupo RO desejado e clique em **Configuration (Configuração)** para acessar a página de configuração do grupo RO.
![](https://main.qcloudimg.com/raw/f03a6fc7e5460181e1e933157b4922cb.png)
3. Nessa página, configure as informações do grupo RO e clique em **OK**.
   Você pode definir a replicação atrasada e selecionar a reprodução por posição em flashback ou identificador de transação global (GTID, na sigla em inglês) durante o atraso para reverter dados com eficiência e corrigir falhas.
   - **Replication Delay (Atraso da replicação)**: você pode configurar o tempo de replicação atrasada entre uma instância somente leitura e sua instância de origem (source). O intervalo de valores é de 1 a 259.200 segundos.
   - **Remove Delayed RO Instances (Remover instâncias RO atrasadas)**: essa opção indica se a política de remoção deve ser ativada. Se uma instância somente leitura for removida quando seu atraso exceder o limite, seu peso será definido como 0 automaticamente e os alarmes serão enviados. Para mais informações sobre como configurar o alarme de remoção de instância somente leitura e os destinatários, consulte [Políticas de alarme (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
   - **Delay Threshold (Limite de atraso)**: define um limite de atraso para a instância somente leitura. Quando o limite for excedido, a instância será removida do grupo RO.
   - **Least RO Instances (Mínimo de instâncias RO)**: essa é a quantidade mínima de instâncias que devem ser retidas no grupo RO. Quando houver menos instâncias no grupo RO, mesmo que uma instância exceda o limite de atraso, ela não será removida.
   - **Assign Read Weight (Atribuir peso de leitura)**: o grupo RO fornece dois métodos de atribuição de peso: atribuição automática pelo sistema e atribuição personalizada. O valor do peso deve ser um número inteiro entre 0 e 100. Veja abaixo a lista de pesos de leitura definidos automaticamente para instâncias do MySQL de dois e três nós pelo sistema:
<table>
<thead><tr>
<th>Especificação de memória (MB)</th>
<th>1000</th><th>2000</th><th>4000</th><th>8000</th><th>12000</th><th>16000</th><th>24000</th><th>32000</th><th>48000</th><th>64000</th><th>96000</th><th>128000</th><th>244000</th><th>488000</th>
</tr></thead>
<tbody><tr>
<td>Peso</td>
<td>1</td><td>1</td><td>2</td><td>2</td><td>4</td><td>4</td><td>8</td><td>8</td><td>10</td><td>12</td><td>14</td><td>16</td><td>26</td><td>50</td></tr>
</tbody></table>
 - **Rebalanceamento**:
    - A modificação do peso só afetará as novas cargas se o rebalanceamento estiver desativado. A operação não afetará as instâncias somente leitura acessadas por conexões persistentes existentes, nem causará desconexão momentânea do banco de dados.
    - Se o rebalanceamento estiver ativado, todas as conexões com o banco de dados serão desconectadas temporariamente, e as cargas das conexões recém-adicionadas serão balanceadas de acordo com os pesos definidos.
<img src="https://main.qcloudimg.com/raw/94a42aa7ed813d8ba68560c40749998f.png"  style="zoom:55%;">


### Encerramento e exclusão de grupo RO
>?
>
>- Não é possível excluir manualmente os grupos RO.
>- Um grupo RO será excluído automaticamente quando a última instância somente leitura nele for eliminada.
>- Os grupos RO vazios não podem ser retidos.
>
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância de origem (source) para acessar a sua página de gerenciamento.
2. Nessa página, selecione a guia **Read-Only Instance (Instância somente leitura)**, localize o grupo RO desejado e exclua todas as instâncias somente leitura clicando em **Terminate/Return (Encerrar/Devolver)** à direita.
![](https://qcloudimg.tencent-cloud.cn/raw/ef06e1a956370519e0c0b652b8a07c72.png)
3. Na janela pop-up, leia e concorde com as **Termination Rules (Regras de encerramento)** e clique em **Terminate Now (Encerrar agora)**.

