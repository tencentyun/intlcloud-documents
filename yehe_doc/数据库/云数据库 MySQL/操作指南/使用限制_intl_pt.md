
## Limites no volume de dados
O TencentDB for MySQL impõe restrições de volume de dados em todos os tipos de instâncias do MySQL para isolar problemas de desempenho devido a recursos limitados. Este documento descreve o impacto técnico de uma única instância ou tabela com um grande volume de dados no MySQL.

**Instância com grande volume de dados**: o mecanismo de armazenamento padrão do TencentDB é o InnoDB. Se o buffer de cache puder armazenar em cache todos os dados e páginas de índice na instância do MySQL, a instância poderá aceitar uma grande quantidade de solicitações de acesso simultâneas. Se a instância contiver muitos dados, o cache e o buffer trocarão dados de entrada/saída com frequência; nesse caso, o gargalo de desempenho do MySQL logo se espalhará para E/S, o que reduzirá a taxa de transferência. Por exemplo, uma instância do TencentDB criada para manter até 8 mil solicitações de acesso por segundo pode aceitar apenas 700 solicitações por segundo se o volume de dados for o dobro do tamanho do cache e do buffer.

**Tabela com grande volume de dados**: se uma tabela contiver muitos dados, o custo do MySQL para gerenciar os recursos da tabela (dados, índices etc.) mudará, o que afetará a eficiência do processamento da tabela. Por exemplo, se o tamanho de uma tabela de transações (InnoDB) exceder 10 GB, a latência nas operações de atualização aumentará, aumentando o tempo de resposta das transações. Nesse caso, o problema só pode ser resolvido por meio de fragmentação e migração.

>?Se a quantidade de tabelas em uma única instância exceder um milhão, o backup, o monitoramento e o upgrade podem falhar e o monitoramento do banco de dados pode ser afetado. Certifique-se de que a quantidade de tabelas em uma única instância seja inferior a um milhão.

## Limites no máximo de conexões
A quantidade máxima de conexões para uma instância do MySQL é especificada com a variável do sistema MySQL `max_connections`. Quando a quantidade real excede `max_connections`, nenhuma outra conexão pode ser estabelecida.
A quantidade padrão de conexões com o TencentDB pode ser exibida clicando no ID da instância para acessar a página **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configurações de parâmetros)** no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), que pode ser ajustada se necessário. No entanto, mais conexões significam que mais recursos do sistema serão consumidos; se a quantidade de conexões for além do que a capacidade real de carga do sistema permite, a qualidade do serviço do sistema será definitivamente prejudicada.
Para mais informações sobre `max_connections`, consulte a [documentação oficial do MySQL](https://dev.mysql.com/doc/).

## Limites na versão do cliente do MySQL
Recomendamos que você use o cliente e a biblioteca do MySQL que acompanham a CVM para se conectar às instâncias do TencentDB.

### Observações sobre consultas lentas
- Para instâncias da CVM do Linux, você pode usar a ferramenta de exportação do TencentDB para obter logs de consulta lenta. Para mais informações, consulte [Restauração do banco de dados do backup físico](https://intl.cloud.tencent.com/document/product/236/31910).
- Para instâncias da CVM do Windows, os logs de consulta lenta não podem ser obtidos diretamente no momento. Se precisar deles, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

### Observações sobre a duração da retenção do binlog do TencentDB
Os binlogs do TencentDB for MySQL podem ser retidos por 7 (valor padrão) a 1.830 dias (personalizável clicando no ID da instância para acessar a página **Backup and Restoration (Backup e restauração)** > **Auto-Backup Settings (Configurações de backup automático)**). 
Se os binlogs forem retidos por um longo período ou aumentarem muito rápido, será necessário espaço adicional para backup e taxas serão cobradas se o espaço exceder o nível gratuito de capacidade de backup.

### Observações sobre o conjunto de caracteres
Por padrão, o TencentDB for MySQL usa o conjunto de caracteres UTF8.
Embora o TencentDB permita a alteração do conjunto de caracteres padrão, recomendamos que você especifique explicitamente o formato de codificação da tabela ao criá-la e especifique a codificação da conexão durante o estabelecimento da conexão. Dessa forma, sua aplicação será mais portátil.
Para mais informações sobre os recursos do conjunto de caracteres do MySQL, consulte a [documentação oficial do MySQL](https://dev.mysql.com/doc/).

Você pode modificar o conjunto de caracteres por meio do SQL ou no console do TencentDB for MySQL.

#### Modificação do conjunto de caracteres por meio do SQL
1. Execute as seguintes instruções SQL para alterar o conjunto de caracteres padrão para instâncias do TencentDB:
```
SET @@global.character_set_client = utf8;
SET @@global.character_set_results = utf8;
SET @@global.character_set_connection = utf8;
SET @@global.character_set_server = utf8;
```
Depois que as instruções forem executadas, `@@global.character_set_server` será automaticamente sincronizado com um arquivo local para persistência em aproximadamente 10 minutos, já as outras três variáveis não. O valor configurado permanecerá inalterado mesmo após a migração ou reinicialização.
2. Execute as seguintes instruções para alterar a codificação do conjunto de caracteres para a conexão atual:
```
SET @@session.character_set_client = utf8;
SET @@session.character_set_results = utf8;
SET @@session.character_set_connection = utf8;
```
Ou
```
SET names utf8;
```
3. Para programas PHP, você pode configurar a codificação do conjunto de caracteres para a conexão atual usando a seguinte função:
```
bool mysqli::set_charset(string charset);
```
Ou
```
bool mysqli_set_charset(mysqli link, string charset);
```
4. Para programas Java, você pode configurar a codificação do conjunto de caracteres para a conexão atual, conforme mostrado abaixo:
```
jdbc:mysql://localhost:3306/dbname?useUnicode=true&characterEncoding=UTF-8
```

#### Modificação do conjunto de caracteres no console do TencentDB for MySQL
1. Faça login no [Console TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique no ID de uma instância na lista de instâncias para acessar a sua página de detalhes.
2. Localize o conjunto de caracteres em **Basic Info (Informações básicas)** e clique no ícone de modificação para modificá-lo.
![](https://qcloudimg.tencent-cloud.cn/raw/c970624cd5c1424b880719a2708c1e55.png)
3. Na janela pop-up, selecione um conjunto de caracteres e clique em **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/53466da07103fff22b41c6fa6f5ca4e7.png)

### Limites nas operações
1. Não modifique as informações e permissões das contas existentes para uma instância do MySQL; caso contrário, alguns serviços de cluster podem ficar indisponíveis.
2. O InnoDB é recomendado para criar bancos de dados e tabelas, para que as instâncias possam aceitar melhor uma grande quantidade de solicitações de acesso simultâneo.
3. Não modifique ou encerre a relação de origem-réplica; caso contrário, o backup dinâmico pode falhar.

### Limites no nome da tabela
Não são aceitos nomes de tabelas em chinês porque podem resultar em falhas de processos, como reversão e upgrade.

## Permissão de conta de banco de dados
O TencentDB for MySQL não fornece mais a permissão de superusuário. Para modificar os parâmetros que exigem essa permissão, faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique no ID da instância para acessar a página **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configurações de parâmetros)** e modifique-os.

## Escolha de rede
Recomendamos o uso de uma VPC. Na VPC, você pode definir livremente a segmentação de intervalo de IP, endereços IP e políticas de roteamento. Em comparação com a rede clássica, a VPC é mais adequado para cenários em que são necessárias configurações de rede personalizadas. Para obter uma comparação da VPC e da rede clássica, consulte [Gerenciamento de rede](https://intl.cloud.tencent.com/document/product/215/31807).

