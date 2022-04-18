Este documento descreve como visualizar o espaço de backup e a camada gratuita da instância MySQL no console.

## Visão geral
O espaço de backup ocupado pelos arquivos de backup da instância do TencentDB for MySQL é alocado por região. É equivalente ao espaço de armazenamento total usado por todos os backups de banco de dados MySQL em uma região, incluindo backups de dados automáticos, manuais e de log. Aumentar o tempo de retenção de backup ou a frequência de backup manual usará mais espaço de backup do banco de dados.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e selecione **Database Backup (Backup de banco de dados)** na barra lateral esquerda.
2. Selecione uma região na parte superior para visualizar suas informações de backup na guia **Overview (Visão geral)**, incluindo backup total, tendência de backup e estatísticas de backup em tempo real.
 - Backup total: esta seção exibe o tamanho e a quantidade de todos os backups, dados e logs, bem como a camada gratuita ocupada por todos eles. 
>?
>- Verde: o espaço total de backup usado não excede a camada gratuita.
>- Laranja: o espaço total de backup usado excedeu a camada gratuita e incorreu em taxas. Para obter mais informações, consulte [Faturamento de espaço de backup](https://intl.cloud.tencent.com/document/product/236/32344).
>
![](https://main.qcloudimg.com/raw/e9489e74614d7708d357de6943837c3c.png)
 - Tendência de backup: esta seção exibe as tendências de backup total, de dados, de log, além do espaço livre.
 - Estatísticas de backup em tempo real: esta seção exibe os IDs/nomes da instância (você pode clicar em um ID/nome para entrar na página de detalhes da instância), espaço de backup (que pode ser classificado por tamanho) e backups de dados/log na região selecionada. Você pode pesquisar uma instância por ID/nome na caixa de pesquisa no canto superior direito.
3. Selecione **Backup List (Lista de backup)** na parte superior, onde a lista de backup é dividida em **Data Backup List (Lista de backup de dados)** e **Log Backup List (Lista de backup de log)**. Você pode clicar em um ID/nome de instância na lista para entrar na respectiva página de detalhes. A lista de backup permite filtragem por período de tempo e pesquisa difusa por ID/nome da instância.
![](https://main.qcloudimg.com/raw/0587e4f22b33960c349b2e2dbbe81d10.png)
 - **Data backup list (Lista de backup de dados)**
    - Aceita a filtragem por campo de lista:
Tipo: todos, backup lógico frio, backup físico frio.
Modo de backup: todos, automático, manual.
Método de backup: atualmente, apenas o backup completo é suportado.
    - Os backups podem ser classificados por horário de backup, horário de início da tarefa, horário de término da tarefa e tamanho do backup.
    - Clique em **Details (Detalhes)** na coluna **Operation (Operação)** para entrar na página de backup e restauração da instância, onde você pode clicar em **Download** para fazer download dos backups. Somente backups manuais podem ser excluídos.
 - **Log backup list (Lista de backup de log)**
    - Os backups podem ser classificados por horário de início e horário de término dos dados de log.
    - Clique em **Details (Detalhes)** na coluna **Operation (Operação)** para entrar na página de backup e restauração da instância, na qual você pode clicar em **Download** para baixar os logs.

## Perguntas frequentes
#### Como é cobrado o espaço de backup que excede a camada gratuita? Como reduzir o custo do espaço de backup?
Para obter mais informações, consulte [Faturamento de espaço de backup](https://intl.cloud.tencent.com/document/product/236/32344).
