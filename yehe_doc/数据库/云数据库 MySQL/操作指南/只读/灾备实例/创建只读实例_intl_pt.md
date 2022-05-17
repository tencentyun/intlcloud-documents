## Visão geral
O TencentDB for MySQL permite que você crie uma ou mais instâncias somente leitura, que são adequadas para a separação de leitura/gravação e cenários de aplicações de “uma fonte e várias réplicas”, além de conseguirem melhorar muito a capacidade de carga de leitura do seu banco de dados.
Atualmente, os endereços unificados de separação de leitura/gravação (ou seja, as solicitações de leitura e gravação são separadas automaticamente) não são aceitos. As instâncias somente leitura precisam ser acessadas com IPs e portas separados.
>?
>- Para obter os preços de instância somente leitura, consulte [Preços do produto](https://buy.Intl.cloud.tencent.com/price/cdb).
- As instâncias somente leitura permitem a configuração de endereços de rede privada na página de detalhes da instância e a modificação personalizada de IP e porta privados.

#### Conceitos
- Grupo somente leitura: consiste em uma ou mais instâncias somente leitura ativadas para o balanceamento de carga. Se houver várias instâncias somente leitura em um grupo somente leitura, o volume de solicitação de leitura poderá ser distribuído uniformemente entre as instâncias. Os grupos somente leitura fornecem IPs e portas para acesso a bancos de dados.
- Instância somente leitura: uma instância de nó único (sem réplica) que aceita solicitações de leitura. Ela não pode existir de forma independente; deve estar em um grupo somente leitura.

#### Arquitetura
A funcionalidade de sincronização de binlog da origem-réplica do MySQL é adotada para instâncias somente leitura, que pode sincronizar as alterações na instância de origem (banco de dados de origem) para todas as instâncias somente leitura. Dada a arquitetura de nó único (sem uma réplica) de instâncias somente leitura, serão feitas repetidas tentativas de restaurar uma instância somente leitura com falha. Portanto, recomendamos que você escolha um grupo RO em vez de uma instância somente leitura para maior disponibilidade.
![](https://main.qcloudimg.com/raw/bf2ef3ecfc232f6e69a99ead319a5cb2.png)

## Limites da funcionalidade
- As instâncias somente leitura podem ser adquiridas apenas para **instâncias de origem (source) de dois ou três nós no MySQL 5.6 ou versão posterior com o mecanismo InnoDB com uma especificação de 1 GB de memória e 50 GB de capacidade de disco ou superior**. Se sua instância de origem (source) estiver abaixo dessa especificação, primeiro faça o upgrade dela.
- A especificação mínima de uma instância somente leitura é 1 GB de memória e 50 GB de capacidade de disco e deve ser maior ou igual ao tamanho de armazenamento adquirido da instância de origem (source).
- Uma instância de origem (source) pode criar até 5 instâncias somente leitura.
- As funcionalidades de backup e reversão não são aceitas.
- Os dados não podem ser migrados para instâncias somente leitura.
- A criação/exclusão do banco de dados não é permitida e nem o phpMyAdmin (PMA).
- As operações como criação/exclusão/autorização de conta e modificação de nome/senha de conta não são aceitas.

## Observações
- Não há necessidade de manter contas ou bancos de dados para instâncias somente leitura, que são sincronizadas com os da instância de origem (source).
- Se a versão do MySQL for a 5.6, mas o GTID não estiver ativado, você precisará ativar o GTID no console antes de criar uma instância somente leitura.
A operação leva muito tempo e a instância será desconectada por vários segundos. Recomendamos fazer isso fora dos horários de pico e adicionar um mecanismo de reconexão nos programas que acessam o banco de dados.
- As instâncias somente leitura aceitam apenas o mecanismo InnoDB.
- A inconsistência de dados entre várias instâncias somente leitura pode ocorrer devido ao atraso na sincronização de dados entre as instâncias somente leitura e a instância de origem (source). Você pode verificar o atraso no console.
- A especificação de uma instância somente leitura pode ser diferente daquela da instância de origem (source), o que facilita o upgrade da instância somente leitura de acordo com a carga. Recomendamos que você mantenha as mesmas especificações de instâncias somente leitura em um grupo RO.

## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de detalhes.
2. Clique em **Add Read-Only Instance (Adicionar instância somente leitura)** na seção **Instance Architecture Diagram (Diagrama de arquitetura de instância)** na guia **Instance Details (Detalhes da instância)** ou clique em **Create (Criar)** na guia **Read-Only Instance (Instância somente leitura)**.
3. Na página de aquisição exibida, especifique as seguintes configurações de instância somente leitura, verifique se tudo está correto e clique em **Buy Now (Comprar agora)**.
 - **Specify RO Group (Especificar grupo RO)**: você pode usar o grupo RO atribuído automaticamente pela alocação do sistema, criar um ou selecionar um existente.
    - **Assigned by system (Atribuído pelo sistema)**: se várias instâncias forem adquiridas ao mesmo tempo, cada uma delas será atribuída a um grupo RO independente e, por padrão, seus pesos serão atribuídos automaticamente pelo sistema.
    - **Create RO group (Criar grupo RO)**: cria um grupo RO. Se várias instâncias forem adquiridas ao mesmo tempo, todas elas serão atribuídas a esse novo grupo RO e, por padrão, seus pesos serão alocados pelo sistema automaticamente.
    - **Existing RO group (Grupo RO existente)**: especifique um grupo RO existente. Se várias instâncias somente leitura
    forem adquiridas ao mesmo tempo, todas elas serão atribuídas ao grupo RO.
    Os seus pesos serão alocados conforme configurado no grupo RO. Se a atribuição pelo sistema estiver definida para o grupo RO, as instâncias serão adicionadas ao grupo automaticamente de acordo com as especificações adquiridas. Se a alocação personalizada estiver definida, seus pesos serão zero, por padrão.
		Como o mesmo IP privado é compartilhado em um grupo RO, se uma VPC for usado, as mesmas configurações de grupo de segurança serão compartilhadas. Se um grupo RO for especificado, não será possível personalizar nenhum grupo de segurança quando as instâncias forem adquiridas.
 - Remove Delayed RO Instances (Remover instâncias RO atrasadas): essa opção indica se a política de remoção deve ser ativada. Se uma instância somente leitura for removida quando seu atraso exceder o limite, ela ficará inativa, seu peso será definido como 0 automaticamente e notificações de aviso serão enviadas. Para mais informações sobre como configurar os alarmes de remoção da instância somente leitura e os destinatários, consulte [Funcionalidade de alarme](https://intl.cloud.tencent.com/document/product/236/8457). A instância será colocada de volta no grupo RO quando seu atraso ficar abaixo do limite. Independentemente se essa opção estiver ativada, uma instância somente leitura que foi removida devido a uma falha de instância se juntará novamente ao grupo RO quando for reparada.
![](https://main.qcloudimg.com/raw/5c002d37fdeb72a5396a394133672338.png)
4. Após a conclusão da aquisição, você será redirecionado para a lista de instâncias. Depois que o status da instância somente leitura for exibido como **Running (Em execução)**, ela poderá ser usada normalmente.

## Perguntas frequentes
#### Quais são as regras para remover instâncias somente leitura?
Após a ativação de **Remove Delayed RO Instances (Remover instâncias RO atrasadas)**, o grupo RO determinará a regra de remoção com base no limite de atraso e no valor de “Least RO Instances (Mínimo de instâncias RO)”. Se o atraso de uma instância somente leitura atingir o limite, ela será removida e inativada, com seu peso definido em 0 e um alarme enviado ao usuário. Quando seu atraso ficar abaixo do limite, ela será devolvida ao grupo RO.
- Delay Threshold (Limite de atraso): define um limite de atraso para a instância somente leitura. Quando o limite for excedido, a instância será removida do grupo somente leitura.
- Least RO Instances (Mínimo de instâncias RO): essa é a quantidade mínima de instâncias que devem ser retidas no grupo somente leitura. Quando houver menos instâncias no grupo somente leitura, mesmo que uma instância exceda o limite de atraso, ela não será removida.

#### Se as instâncias somente leitura forem encerradas ou devolvidas, como a instância de origem (source) será afetada?
O encerramento e a devolução de instâncias somente leitura não afetam a instância de origem (source).
