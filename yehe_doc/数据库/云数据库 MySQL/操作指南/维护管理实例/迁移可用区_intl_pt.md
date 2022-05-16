
Você pode migrar uma instância do TencentDB for MySQL para outra zona de disponibilidade (AZ, na sigla em inglês) na mesma região. Todos os seus atributos, configurações e endereço de conexão permanecerão inalterados após a migração. O tempo necessário para migrar a instância está sujeito ao volume de dados da instância.

Por exemplo, você pode migrar para uma nova AZ nos seguintes cenários:
- Se você deseja modificar o tipo de uma instância, mas a AZ atual não aceita o novo tipo de instância, você pode migrar a instância para uma AZ que aceite esse novo tipo.
- Se a AZ atual não tiver recursos restantes para dimensionamento, você também poderá migrar a instância para outra AZ na mesma região com recursos suficientes para atender às necessidades de suas operações.

## Pré-requisitos
- A instância está em execução.
- A região em que a instância está localizada tem várias AZs para permitir a migração entre AZs.

## Descrição do faturamento
Essa funcionalidade é gratuita. Não há cobrança nem mesmo para migrar uma instância de uma única AZ para várias AZs.

## Descrição da funcionalidade
- A instância será momentaneamente afetada quando sua AZ for alternada; portanto, certifique-se de que sua aplicação tenha um mecanismo de reconexão automática.
- A migração de AZ não resultará em uma mudança de VIP.
- A instância de origem (source) não é desacoplada das instâncias somente leitura após a migração de AZ e ainda pode ser sincronizada com elas.
- Você pode escolher a AZ de instâncias somente leitura.
- As instâncias somente leitura não permitem a migração entre regiões.
- Nenhum acesso por meio do grupo RO (remoção) pode ser feito durante a alternância de migração.
- Se a instância em questão tiver um bloqueio de tarefa na plataforma de nuvem durante a tarefa DTS, a migração entre AZs não poderá ser executada.
- Se houver tarefas DTS em andamento, após a migração de AZ, você precisará reiniciar essas tarefas.
- A exportação de DTS falhará se a instância de origem (source) passar por uma alternância de migração entre AZs durante a exportação do dumper.
- Para migração de AZ na arquitetura de dois ou três nós, a escolha das AZs de origem (source) e de réplica está sujeita aos recursos restantes na nova AZ e região. Você pode escolher a nova AZ durante a migração no console, e a opção de réplica de AZ será atualizada automaticamente.

## Tipo de migração

| Tipo de migração | Cenário aplicável | Tipos de instância compatíveis |
|---------|---------|---------|
| Migração de uma AZ para outra AZ | A AZ em que a instância está localizada está com carga total ou outras condições que afetam o desempenho da instância. | Instâncias de origem (source), somente leitura e DR |
| Migração de uma AZ para várias AZs | Você pode melhorar a capacidade de recuperação de desastres da instância e implementar a recuperação de desastres entre data centers. As instâncias de origem (source) e réplica estão localizadas em AZs diferentes. As instâncias Multi-AZ podem aguentar níveis mais altos de desastres do que as instâncias de AZ única. Por exemplo, as últimas podem tolerar falhas no nível do servidor e do rack, já as primeiras podem tolerar falhas no nível do data center. | Instâncias de origem (source), somente leitura e DR |
| Migração de várias AZs para uma AZ | Você deseja atender a requisitos de funcionalidades específicos. | Instâncias de origem (source), somente leitura e DR |

## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um **instance ID (ID de instância)** ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de detalhes.
2. Na página **Instance Details (Detalhes da instância)**, selecione **Basic Info (Informações básicas)** > **Region/AZ (Região/AZ)** e clique em **Migrate to New AZ (Migrar para nova AZ)**, ou selecione **Availability Info (Informações de disponibilidade)** > **Deployment Mode (Modo de implantação)** e clique em **Modify Replica AZ (Modificar AZ de réplica)**.
![](https://qcloudimg.tencent-cloud.cn/raw/cd1bd1b09029548391ba986c61027907.png)
3. Na janela pop-up, ajuste as configurações relevantes e clique em **Submit (Enviar)** após verificar se tudo está correto.
 - **New AZ (Nova AZ)**: você pode alterar a AZ de origem (source) na lista suspensa ou selecionar **Yes (Sim)** para **Multi-AZ Deployment (Implantação Multi-AZ)** para modificar a AZ de réplica.
 - **Delay Threshold for Data Consistency Check (Limite de atraso para verificação de consistência de dados)**: esta opção fica disponível somente quando você altera a AZ de origem (source). O limite pode ser um número inteiro entre 1 e 10 segundos.
>! Pode haver um atraso durante a verificação de consistência de dados. Você precisa definir um limite de atraso de dados. A verificação de consistência do banco de dados será pausada quando o atraso exceder o valor definido e será retomada quando o atraso ficar abaixo do limite. Se o valor do limite for muito pequeno, a migração poderá demorar mais.
 - **Switch Time (Hora de alternância)**: você pode optar por alternar durante o período de manutenção ou após a conclusão da migração. Para mais informações, consulte [Configuração do período de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
![](https://qcloudimg.tencent-cloud.cn/raw/33577bc75f50cb9805478f71b372e07f.png)

