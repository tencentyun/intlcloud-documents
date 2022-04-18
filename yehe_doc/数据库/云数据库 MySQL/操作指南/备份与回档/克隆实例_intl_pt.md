Este documento descreve como clonar uma instância do TencentDB for MySQL e restaurar rapidamente os dados para o clone recém-adquirido no console.

## Visão geral
Você pode restaurar uma instância do TencentDB for MySQL para qualquer momento dentro do período de retenção do backup de log ou de um backup físico específico definido por clonagem. O clone é uma nova instância criada a partir dos dados de backup de acordo com o momento de restauração que você especificou. Após a verificação do clone, você pode migrar os respectivos dados de volta para a instância original com [DTS](https://intl.cloud.tencent.com/document/product/571/13709) ou pode começar a usar o clone.

#### Modo clone
- Clone uma instância e restaure o clone para qualquer momento dentro do período de retenção de backup de log que você definiu.
- Clone uma instância e restaure o clone de um conjunto de backup físico específico dentro do período de retenção de backup de dados que você definiu.

#### Faturamento do clone
- O clone adota o modo de faturamento de pagamento conforme o uso. Para obter mais informações sobre esse modo de faturamento e cálculo de taxas, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/236/18335).
- O clone não será cobrado até que o processo de clonagem seja concluído.  

## Pré-requisitos
- Arquiteturas de instâncias suportadas: MySQL de dois ou três nós
- A instância original deve estar no status **Running (Em execução)**.
- Se o modo clone estiver definido como **By backup set (Por conjunto de backup)**, a instância original deverá ter criado pelo menos um backup físico. Você pode fazer login no [console](https://console.cloud.tencent.com/cdb), selecionar **Database Backup (Backup de banco de dados)** na barra lateral esquerda e visualizar o status do backup na guia **Backup List (Lista de backup)**.
- O saldo da sua conta deve ser positivo.

## Observações
- O espaço em disco rígido da instância clone deve ser maior que a quantidade de dados a serem clonados, caso contrário, a tarefa de clonagem poderá falhar.
- A zona de disponibilidade, a versão do banco de dados, o modo de replicação e os parâmetros de banco de dados padrão do clone devem ser os mesmos da instância original.
- O clone não será exibido na lista de instâncias no console até que o processo de clonagem seja concluído.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a respectiva página de gerenciamento.
2. Selecione **Backup and Restoration (Backup e restauração)** > **Data Backup List (Lista de backup de dados)**, clique em **Clone** no canto superior esquerdo ou localize o backup desejado e clique em **Clone** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/b53e3c4f249a5f22638c32f4c92c7f75.png)
2. Na página de aquisição exibida, especifique o modo do clone e clique em **Buy Now (Comprar agora)**.
 - **By time point (Por instante no tempo)**: você pode restaurar uma instância para qualquer instante no tempo dentro do período de retenção do backup de log.
 - **By backup set (Por conjunto de backup)**: você pode restaurar dados de um conjunto de backup para uma nova instância. Os conjuntos de backup disponíveis dependem do período de retenção do backup de dados.
 >?Você pode fazer login no [console](https://console.cloud.tencent.com/cdb), selecionar **Database Backup (Backup de banco de dados)** na barra lateral esquerda e visualizar o período de retenção de backup na guia **Backup list (Lista de backup)**.
 >
![](https://main.qcloudimg.com/raw/f2fcdd5471326b60f6ee7ea8872f00bc.png)
4. Após a compra, você pode visualizar os detalhes do clone na guia **Backup and Restore (Backup e restauração)** > **Cloned Instance List (Lista de instâncias clonadas)**.
![](https://main.qcloudimg.com/raw/3b6a2781adafd4cbde550ea00f3898a8.png)
5. Depois que o processo de clonagem for concluído, você poderá visualizar a instância de clone recém-criada na lista de instâncias.

## Documentos relacionados
- Para obter mais informações sobre restauração de bancos de dados e tabelas individuais, consulte [Reversão de banco de dados](https://intl.cloud.tencent.com/document/product/236/7276).
- Para obter mais informações sobre como restaurar dados para uma instância autocriada, consulte [Restauração de bancos de dados de backups físicos](https://intl.cloud.tencent.com/document/product/236/31910) e [Restauração de bancos de dados de backups lógicos](https://intl.cloud.tencent.com/document/product/236/31909).

## Perguntas frequentes
#### O acesso à instância original será afetado durante o processo de clonagem?
O conjunto de backup original e os binlogs carregados na COS são usados ​​para clonagem, o que não afetará o acesso à instância de origem.
