
## Visão geral
Este documento descreve como atualizar o mecanismo do TencentDB for MySQL no console.
O TencentDB for MySQL oferece suporte à atualização do mecanismo de banco de dados:
- De MySQL 5.5 para MySQL 5.6
- De MySQL 5.6 para MySQL 5.7

>?
>- Não há suporte para downgrade do mecanismo de banco de dados.
>- Não há suporte para atualização em versões principais. Por exemplo, para atualizar uma instância do TencentDB for MySQL 5.5 para o MySQL 5.7 ou posterior, primeiro você precisa atualizá-la para o MySQL 5.6.
>- Atualmente, o MySQL 5.7 não pode ser atualizado para o MySQL 8.0. 
<span id ="shengjiguize"></span>
## Regras de atualização
- A sintaxe `create table … as select …` não é suportada.
- A sincronização de réplica de origem no TencentDB for MySQL 5.6 e 5.7 é implementada com base no GTID. Apenas InnoDB é suportado por padrão.
- As tabelas MyISAM serão convertidas em tabelas InnoDB durante o processo de atualização do MySQL 5.5 para 5.6. **Recomendamos que você conclua a conversão antes de fazer upgrade.**
- Durante a atualização, o TencentDB for MySQL limpará a tabela `slow_log`. Salve os logs antes de atualizar, se necessário.
- Se uma instância a ser atualizada estiver associada a outras instâncias (por exemplo, instância de origem e réplicas somente leitura), essas instâncias serão atualizadas juntas para garantir a consistência dos dados.**
- A atualização do TencentDB for MySQL envolve migração de dados e geralmente leva um tempo relativamente longo. Tenha paciência e aguarde. Durante o processo de upgrade, sua empresa não será afetada e a instância poderá ser acessada normalmente.
- A alternância de instância pode ser necessária após a conclusão da atualização da versão (ou seja, a instância do MySQL pode ser desconectada por alguns segundos). Recomendamos que os aplicativos sejam configurados com o recurso de reconexão automática e que a alternância seja realizada durante a janela de manutenção da instância. Para obter mais informações, consulte [Configuração da janela de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
- Se o número de tabelas em uma única instância exceder um milhão, a atualização pode falhar e o monitoramento do banco de dados pode ser afetado. Certifique-se de que o número de tabelas em uma única instância não seja superior a um milhão.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/), localize a instância desejada na lista e selecione **More (Mais)** > **Upgrade Version (Atualizar versão)** na coluna **Operation (Operação)**.
>?O MySQL 8.0 não pode ser atualizado para uma versão posterior.
>
2. Na janela pop-up, selecione a versão do banco de dados a ser atualizada e clique em **Upgrade (Atualizar)**.
Como a atualização do banco de dados envolve a migração de dados, após a conclusão da atualização, pode ocorrer uma desconexão muito curta do banco de dados MySQL, com duração de apenas alguns segundos. Quando o upgrade é iniciado, o **Switch Time (Horário de alternância)** pode ser selecionado como **During maintenance time (Durante o horário de manutenção)**, para que a alternância seja iniciada na próxima **janela de manutenção**, após a conclusão do upgrade da instância. 
>!Se você selecionar **During maintenance time (Durante o horário de manutenção)**, a alternância não ocorrerá imediatamente após a conclusão da atualização da especificação do banco de dados; em vez disso, a sincronização continuará até que a instância vá para a próxima **janela de manutenção**, quando a alternância será executada. Dessa forma, o tempo total necessário para atualizar a instância pode ser estendido.
>
![](https://qcloudimg.tencent-cloud.cn/raw/5fd7b83457ffb0cab80112ad32e8e0be.png)

## Perguntas frequentes
#### O TencentDB for MySQL fará backup dos dados automaticamente antes da atualização?
O TencentDB for MySQL adota o mecanismo de backup dinâmico, diário, de servidor duplo em tempo real que oferece suporte à restauração sem perdas de dados dos últimos 7 a 732 dias em backup de dados e backup de log (binlog).

#### É possível efetuar o downgrade do TencentDB for MySQL de MySQL 5.7 para o MySQL 5.6?
Não é possível efetuar o downgrade do mecanismo de banco de dados. Para usar uma instância MySQL 5.6, é preciso encerrar ou retornar a instância MySQL 5.7 existente e, em seguida, adquirir uma instância MySQL 5.6.

#### Haverá um atraso na réplica de origem durante a atualização?
A atualização da instância de origem requer comparação de dados e pode causar um atraso na réplica de origem.

#### A alternância de instância após a atualização da versão do mecanismo de banco de dados afetará minha instância do TencentDB for MySQL?
A atualização não afetará seus negócios, mas a instância do TencentDB for MySQL pode ser desconectada por alguns segundos. Recomendamos que os aplicativos sejam configurados com o recurso de reconexão automática e que a alternância de instância seja realizada durante a janela de manutenção da instância.

#### Quanto tempo levará para atualizar a versão do mecanismo de banco de dados de uma instância do TencentDB for MySQL? Como verifico o progresso da atualização?
A duração da atualização depende da quantidade de dados na instância, da velocidade de replicação de dados etc.
A atualização do TencentDB for MySQL envolve migração de dados e geralmente leva um tempo relativamente longo. Tenha paciência e aguarde. Sua empresa não será afetada durante o processo de atualização e poderá ser acessada normalmente.

#### Por que a instância está sempre no status "Waiting for switch (Aguardando alternância)"?
Talvez você tenha selecionado **During maintenance time (Durante o horário de manutenção)** como **Switch Time (Horário de alternância)** e a alternância será iniciada na próxima janela de manutenção após a conclusão da atualização da instância.
Para alternar a instância imediatamente, clique em **Switch Now (Alternar agora)** na coluna **Operation (Operação)** na lista de instâncias. A conexão pode ser interrompida durante a troca. Certifique-se de que o banco de dados tenha um mecanismo de reconexão.
