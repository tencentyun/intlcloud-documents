Para evitar que os dados sejam perdidos ou corrompidos, você pode fazer backup de um banco de dados de maneira automática ou manual.

## Visão geral de backup
### Modos de backup
Instâncias do TencentDB for MySQL de dois e três nós são compatíveis com **backup automático** e **backup manual** de bancos de dados.

### Tipos de backup
As instâncias do TencentDB for MySQL de dois e três nós são compatíveis com dois tipos de backup:
- **Backup físico**, que replica dados físicos completos (disponível tanto para backup automático quanto para backup manual).
- **Backup lógico**, que faz backup de instruções SQL (disponível apenas para backup manual).
>?
>- Para restaurar um banco de dados de um backup físico, o xbstream deve primeiro descompactar os arquivos de backup. Para obter mais informações, consulte [Restauração de bancos de dados de backups físicos](https://intl.cloud.tencent.com/document/product/236/31910).
>- Se o número de tabelas em uma única instância exceder um milhão, o backup poderá falhar e o monitoramento do banco de dados poderá ser afetado. Certifique-se de que o número de tabelas em uma única instância não seja superior a um milhão.
>- Como os dados das tabelas criadas pelo mecanismo de armazenamento MEMORY são armazenados na memória, não é possível criar backups físicos para essas tabelas. Para evitar a perda de dados, recomendamos convertê-los em tabelas do InnoDB.
>- Se houver um grande número de tabelas em uma instância sem chave primária, o backup poderá falhar e a alta disponibilidade da instância poderá ser afetada. Crie chaves primárias ou índices secundários para essas tabelas.

| Vantagens do backup físico | Desvantagens do backup lógico |
|---------|---------|
| <li>Alta velocidade de backup. <li>O backup e a compactação de streaming são compatíveis. <li>Alta taxa de sucesso. <li>Restauração simples e eficiente. <li>Operações de acoplamento baseadas em backup mais rápidas, como adicionar réplicas somente leitura e instâncias de recuperação de desastres. <li>1/8 do tempo médio necessário para criar um backup lógico. <li>Dez vezes mais rápido que os backups lógicos durante a importação. | <li>Muito tempo necessário para restaurar, pois leva tempo para executar instruções SQL e construir índices. <li>Baixa velocidade de backup, especialmente quando há grandes quantidades de dados. <li>Possível aumento no atraso da réplica de origem devido à pressão nas instâncias durante o backup. <li>Possível perda de informações de precisão de pontos flutuantes. <li>Potenciais falhas de backup devido a visualizações erradas e outros problemas. <li>Operações de acoplamento baseadas em backup mais lentas, tais como adicionar réplicas somente leitura e instâncias de recuperação de desastres. |

### Objetos de backup
| Backup de dados | Backup de log |
|---------|---------|
| TencentDB for MySQL de dois e três nós: <li>O backup automático permite backup físico completo. <li>O backup manual permite backup físico completo, backup lógico completo e backup lógico de banco de dados único/tabela. <li>Os backups automáticos e manuais podem ser compactados e baixados. | O TencentDB for MySQL de dois e três nós permite backup de binlog: <li>Os arquivos de log ocupam o espaço de backup da instância. <li>Os arquivos de log podem ser baixados, mas não podem ser compactados. <li>Os períodos de retenção podem ser definidos para arquivos de log. |

## Observações
- Desde 26 de fevereiro de 2019, o recurso de backup automático do TencentDB for MySQL aceita apenas backup físico (tipo padrão) e não fornece mais backup lógico. Os backups lógicos automáticos existentes serão alternados para backups físicos automaticamente.
Isso não afetará seu acesso dos seus negócios, mas pode afetar seus hábitos de backup automático. Se precisar de backups lógicos, você pode usar o recurso de backup manual no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) ou chamar a [API CreateBackup](https://intl.cloud.tencent.com/document/product/236/15844) para gerar backups lógicos.
- Os arquivos de backup de instância ocupam espaço de backup. Recomendamos que você planeje o uso do espaço de backup adequadamente. O uso do espaço de backup que excede a camada gratuita incorrerá em taxas. Para obter mais informações, consulte [Faturamento de espaço de backup](https://intl.cloud.tencent.com/document/product/236/32344).
- Recomendamos que você faça backup de seus dados fora do horário de pico.
- Recomendamos que você baixe os arquivos de backup localmente antes que eles sejam excluídos após o término do período de retenção.
- Não execute operações de DDL durante o processo de backup para evitar falhas de backup devido ao bloqueio de tabela.
- Não é possível fazer backup de instâncias do TencentDB for MySQL de nó único.

## Backup automático de dados MySQL
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID de instância na página da lista de instâncias para acessar a página de gerenciamento da instância e selecione **Backup and Restore (Fazer backup e restaurar)** > **Auto Backup Settings (Configurações de backup automático)**.
![](https://main.qcloudimg.com/raw/69fed1aac393a518bd8cc2ad1fea550f.png)
2. Selecione os parâmetros de backup na janela pop-up (os detalhes são exibidos conforme abaixo) e clique em **OK**:
>?
>- O [recurso de reversão](https://intl.cloud.tencent.com/document/product/236/7276) depende do ciclo de backup e dos dias de retenção de backups de dados e backups de log (binlog). A reversão será afetada se você reduzir a frequência de backup automático e o período de retenção. Selecione os parâmetros conforme necessário.
>Por exemplo, se o ciclo de backup for definido para segunda-feira e quinta-feira e o período de retenção for definido para sete dias, você poderá reverter um banco de dados para qualquer ponto do tempo nos últimos sete dias (que são os dias de retenção reais dos backups de dados e backups de log).
>- Os backups automáticos não podem ser excluídos manualmente. Você pode definir o período de retenção para backups automáticos e os backups serão excluídos automaticamente quando expirarem.
>
<table>
<thead><tr><th>Parâmetro</th><th>Descrição</th></tr></thead>
<tbody>
<tr>
<td>Programação de backup</td><td>Para garantir a segurança dos dados, faça backup pelo menos duas vezes por semana. Todos os sete dias da semana serão selecionados por padrão.</td></tr>
<tr>
<td>Horário de início de backup</td><td><ul><li>A horário padrão de início de backup é atribuído automaticamente pelo sistema. <li>Você pode definir um horário de início conforme necessário. Recomendamos que você o defina para horários fora de pico. Trata-se apenas do horário de início do processo de backup e não indica o horário de término. <br>Por exemplo, se o horário de início do backup estiver definido de 02:00 às 06:00, o sistema iniciará um backup em um momento entre 02:00 e 06:00, o que depende da política de backup de back-end e das condições do sistema de backup.</td></tr>
<tr>
<td>Tempo de retenção de backup de dados</td><td>Os arquivos de backup de dados podem ser retidos por 7 (valor padrão) a 1830 dias.</td></tr>
<tr>
<td>Tempo de retenção de backup de log</td><td>Os arquivos de backup de log podem ser retidos de 7 (valor padrão) a 1830 dias. </td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/a371d4ba960264aa5630b59a3bfe5096.png"  style="margin:0;">

## [Backup manual de dados MySQL](id:manual-backup)
O recurso de backup manual permite iniciar uma tarefa de backup manualmente.
>?
>- O backup manual suporta backup físico completo, backup lógico completo e backup lógico de banco de dados único/tabela.
>- Os backups manuais podem ser excluídos manualmente da lista de backups no console. Você pode excluir backups manuais que não estão mais em uso para liberar espaço. Os backups manuais podem ser mantidos permanentemente, desde que não sejam excluídos.
>- Quando a instância está executando backup automático diário, nenhuma tarefa de backup manual pode ser iniciada.
>
1. Na página da lista de instâncias, clique em um ID de instância para acessar a página de gerenciamento da instância e selecione **Backup and Restore (Fazer backup e restaurar)** > **Manual Backup (Backup manual)**.
2. Selecione o modo de backup e o objeto na janela pop-up e clique em **OK**.
![](https://main.qcloudimg.com/raw/a16e644f51756b6a98597945e45329cd.png)
>?Para backup lógico de banco de dados único/tabela, selecione o banco de dados ou tabela a ser copiado em **Select database & table (Selecionar banco de dados e tabela)** na coluna da esquerda e adicione o item selecionado à coluna da direita. Se você não tiver um banco de dados, crie primeiro um banco de dados/tabela.
>
![](https://main.qcloudimg.com/raw/76924e2c76ac348b68ed113d679d6907.png)

## Perguntas frequentes
#### 1. Posso baixar ou restaurar arquivos de backup que excedam o período de retenção?
Os conjuntos de backup expirados serão excluídos automaticamente e não poderão ser baixados ou restaurados.
- Recomendamos que você configure um período de retenção de backup com base nas necessidades de negócios ou baixe os arquivos de backup localmente por meio do [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb).
- Também é possível fazer backup manual dos dados da instância no console. Os backups manuais serão mantidos permanentemente.
>?Os backups manuais também ocuparão o espaço de backup. Recomendamos que você planeje o uso do espaço de backup adequadamente para reduzir custos.

#### 2. Posso excluir backups manualmente?
- Os backups automáticos não podem ser excluídos manualmente. Você pode definir o período de retenção para backups automáticos e eles serão excluídos automaticamente quando expirarem. 
- Os backups manuais podem ser excluídos manualmente da lista de backups no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Os backups manuais podem ser mantidos permanentemente, desde que não sejam excluídos.

#### 3. Posso desabilitar backups de dados e logs?
Não. No entanto, você pode reduzir a frequência de backup e excluir backups manuais que não são mais usados ​​por meio do [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) para diminuir o uso da capacidade.

#### 4. Como posso reduzir os custos de capacidade de backup?
- Exclua backups manuais que não são mais usados ​​(você pode fazer login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID de instância para acessar a página de gerenciamento da instância e exclua backups manuais na guia **Backup and Restore (Fazer backup e restaurar)**. 
- Reduza a frequência de backup automático de dados para negócios não essenciais (você pode ajustar o ciclo de backup e o período de retenção no console. A frequência deve ser de pelo menos duas vezes por semana).
>?O [recurso de reversão](https://intl.cloud.tencent.com/document/product/236/7276) depende do ciclo de backup e dos dias de retenção de backups de dados e backups de log (binlog). A reversão será afetada se você reduzir a frequência de backup automático e o período de retenção. Selecione os parâmetros conforme necessário.
>
- Reduza o período de retenção de dados e backups de log para negócios não essenciais (um período de retenção de 7 dias pode atender aos requisitos da maioria dos cenários).

| Cenário de negócios             | Período de retenção de backup recomendado Período                                                 |
| -------------------- | ------------------------------------------------------------ |
| Negócios principais             | 7 a 1830 dias |
| Negócios não essenciais e não relacionados a dados | 7 dias |
| Negócios de arquivo | 7 dias. Recomendamos que você faça backup manual dos dados com base em suas necessidades de negócios e exclua os backups imediatamente após o uso |
| Negócios de teste | 7 dias. Recomendamos que você faça backup manual dos dados com base em suas necessidades reais de negócios e exclua os backups imediatamente após o uso |

