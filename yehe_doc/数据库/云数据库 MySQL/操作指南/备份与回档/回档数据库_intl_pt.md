
## Visão geral
O TencentDB for MySQL não alterará nenhum dos seus dados. Os dados corrompidos por motivos pessoais podem ser recuperados, pelo próprio usuário, por meio de reversão. Um recurso de reversão é fornecido para reverter bancos de dados ou tabelas na Tencent Cloud com base em backup de dados e de binlog. É possível efetuar a reversão de dados em tempo real.

Ao reconstruir imagens periódicas e transações em tempo real, o recurso de reversão do TencentDB for MySQL pode reverter um banco de dados ou tabela para o ponto especificado no tempo e as fatias de tempo de todos os dados são, garantidamente, idênticas. Um novo banco de dados ou tabela será gerado na instância original e, durante o processo, o banco de dados ou tabela original poderá ser acessado normalmente. Após a conclusão da reversão, você pode ver os bancos de dados ou tabelas novos e originais.

## Como funciona a reversão
O recurso de reversão pode reverter bancos de dados ou tabelas para um ponto específico no tempo com base em `backup de dados frios e backup de binlog correspondente`.
![](https://main.qcloudimg.com/raw/89ab32296ba576cf8e087d760b5a8109.png)
1. Os dados são exportados da réplica do MySQL e importados diariamente para o sistema de backup frio.
2. Para reverter bancos de dados ou tabelas, solicite uma instância de reversão temporária do sistema de reversão. Exporte os dados frios do sistema de backup frio e importe-os para a instância de reversão temporária (os tipos de dados importados variam de acordo com os métodos de reversão).
3. Estabeleça uma relação de réplica de origem entre a instância de reversão e a instância de origem do MySQL, defina o tempo de reversão e especifique os bancos de dados ou tabelas a serem revertidos.
4. Replique os bancos de dados ou tabelas de reversão para a instância de origem do MySQL.

## Limites de recursos
- Somente instâncias de origem podem ser revertidas. Réplicas somente leitura ou instâncias de recuperação de desastres não podem ser revertidas.
- Apenas bancos de dados ou tabelas especificados podem ser revertidos. Os bancos de dados ou tabelas após a reversão serão renomeados e replicados para a instância de origem.

## Observações
- O recurso de reversão está sujeito ao ciclo de backup e aos dias de retenção definidos para backup automático. Ele permite a reversão de dados com base em backup de dados e backup de binlog, de acordo com os dias de retenção configurados e o ciclo de backup. Para as configurações do ciclo de backup, consulte [Backup automático de dados MySQL](https://intl.cloud.tencent.com/document/product/236/37796). Para garantir a segurança dos dados do MySQL, defina o ciclo de backup automático para pelo menos duas vezes por semana.
- Se o banco de dados ou a tabela a ser revertida não existir ou tiver sido descartada, você precisará fazer login na instância do TencentDB e criar uma antes de executar a reversão no console.
- Se o backup a frio antes da reversão não contiver a tabela, a reversão falhará.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instância, selecione uma ou mais instâncias e clique em **More (Mais)** > **Rollback (Reverter)**.
>?
>- Se a reversão for realizada em apenas uma instância, você também poderá acessar a página de gerenciamento de instâncias e clicar em **Rollback (Reverter)** no canto superior direito.
>- Até 5 tarefas de reversão podem ser iniciadas ao mesmo tempo sob o mesmo APPID.
>
![](https://main.qcloudimg.com/raw/abd517cf8b6db3db57b622f13d365893.png)
2. Na página de reversão, defina o método de reversão (descrito abaixo), selecione os bancos de dados ou tabelas a serem revertidos e clique em **Next step: set the rollback time and database table name (Próxima etapa: defina o tempo de reversão e o nome da tabela de banco de dados)**.
   - Fast (Rápido): o backup completo da instância é importado e os bancos de dados ou tabelas selecionados são revertidos. Este modo de reversão é lento, mas não tem limite.
   - Mais rápido: backup completo e binlogs em nível de banco de dados são importados. Para operação entre bancos de dados, se o banco de dados associado não for selecionado ao mesmo tempo, a reversão poderá falhar.
   - Ultrafast (Ultrarrápido): backup completo e binlogs em nível de tabela são importados. Para operação entre tabelas, se a tabela associada não for selecionada ao mesmo tempo, a reversão poderá falhar.
>?
>- Somente bancos de dados/tabelas cujo nome contém dígitos, letras, sublinhados ou suas combinações podem ser revertidos. Bancos de dados/tabelas com nomes contendo caracteres especiais não são compatíveis.
>- No modo em que apenas os bancos de dados/tabelas especificados podem ser revertidos, um máximo de 500 bancos de dados/tabelas na mesma instância podem ser revertidos por vez.
>- Se a reversão envolver operações compostas em outros bancos de dados ou tabelas durante a execução de binlogs, as instruções SQL podem falhar.
>- Se a reversão envolver chaves estrangeiras e outras restrições da tabela durante a execução dos binlogs, as instruções SQL podem falhar.
>
![](https://main.qcloudimg.com/raw/6cb2fa4d3e8b0d795bd5bf19f8d69d86.png)
3. Defina o banco de dados pós-reversão ou o nome da tabela e o tempo de reversão e clique em **Rollback (Reverter)**.
>?
>- Apenas um tempo de reversão pode ser definido para cada instância.
>- Se você optar por definir um tempo de reversão em lote, todos os bancos de dados ou tabelas serão revertidos no horário especificado.
>- Se você optar por definir um tempo de reversão de tabela única, as tabelas serão revertidas em seu respectivo tempo de reversão.
>- O nome do banco de dados ou da tabela após a reversão pode conter até 64 letras, dígitos ou símbolos (.-\_$).
>
![](https://main.qcloudimg.com/raw/62377981b147bdb453d79631b3557d12.png)
4. Após o envio, vá para **Operation Log (Log de operação)** > **Rollback Log (Log de reversão)** para ver o progresso da reversão. Clique em **View details (Ver detalhes)** para ver o log de reversão em tempo real.
![](https://main.qcloudimg.com/raw/b5206b3c23d532553fb54dfc4fe7bfd0.png)
5. Quando a reversão for concluída, vá para **Database Management (Gerenciamento de banco de dados)** > **Database List* (Lista de banco de dados)** para visualizar o novo banco de dados ou tabela após a reversão na instância original.
![](https://main.qcloudimg.com/raw/9b939d9a6a7da59092df0051f452b5cd.png)

