Este documento descreve como usar a ferramenta de cliente `tcaplus_client` para acessar os dados do TcaplusDB.
Todas as instruções de operação de dados devem conter a cláusula `WHERE`, que deve conter pelo menos um campo de chave primária. Se houver várias chaves primárias, separe-as utilizando o `and`.

## Ferramenta de cliente
O `tcaplus_client` é uma ferramenta de cliente usada para acessar tabelas do TcaplusDB e pode ser obtida no endereço de download na tabela abaixo.

O pacote de lançamento do TcaplusServiceAPI para Linux x86_64 contém a ferramenta `tcaplus_client` para Linux de 64 bits.

| Versão | Sistema operacional | Nome do pacote de download |
| ------------- | -------- | ------------------------------------------------------------ |
| 3.36.0.192960 | Linux    | [TcaplusPbApi3.36.0.192960.x86_64](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz) |

>?As operações básicas precisam ser realizadas na instância do CVM no mesmo VPC e sub-rede em sua conta do Tencent Cloud assim como é feito na sua instância do TcaplusDB.

### Instalação do cliente
Após baixar o pacote de instalação TcaplusServiceAPI, você pode [usar a ferramenta de upload](https://intl.cloud.tencent.com/document/product/213/34821) para carregá-lo na instância do CVM no mesmo VPC e sub-rede do cluster do TcaplusDB.

1. Após o upload, execute o seguinte comando para descompactar o pacote de instalação:
```
tar -xf TcaplusServiceApi3.32.0.191008.x86_64_release_20190409.tar.gz -C tcaplus
```
2. Após a descompactação, entre no diretório `bin` em `tcaplus` e conceda a permissão executável da ferramenta:
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. Execute o comando `./tcaplus_client`, e o sistema solicitará que você insira as informações de parâmetro requeridas para a conexão do banco de dados. Você pode inseri-las com base nas informações do cluster.
>!No exemplo abaixo, `app_id` indica o ID de acesso do cluster, `App` indica o cluster e `zone` indica o grupo de tabelas.


```
# ./tcaplus_client
--------------------------------------------------------------------------------
 invalid parameters, please start the client as following:
    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]
    the params in [] are optional, and theire order is not important.
    -a(--ap_id)    App ID
    -z(--zone_id)    ZONE ID
	-s(--signature)    PASSWORD
    -d(--dir)    dir server addr
    -t(--table)    table to add
    -l(--log)    log file name that must be client_log.xml, and log class name be client
    -T(--tdr)    tdr filename 
    -e(--execute)    content following should be with qoutes.
    e.g. ./tcaplus_client -a 2 -z 3 -s "test@Password1" -d 172.xx.xx.181:9999 -T table_test.tdr 
--------------------------------------------------------------------------------
```

### Conexão ao TcaplusDB
Execute o comando correspondente para se conectar ao TcaplusDB. As informações do ponto de acesso estão descritas no exemplo abaixo, e a tabela `tb_online` foi criada no grupo de tabelas cujo ID é 1:
- ID de acesso ao cluster: 2
- Senha de conexão: test@Password1
- Endereço privado: porta privada: 10.125.32.21:9999
- ID do grupo de tabelas: 1

```
./tcaplus_client -a 2 -z 1 -s "test@Password1" -d 10.125.32.21:9999
+------------------------------------------------------------------------------+
|    tcaplus_client x86_64  build at Wed Jan 18 22:08:38 CST 2017              |
|                                                                              |
|    Welcome!                                                                  |
+------------------------------------------------------------------------------+

tcaplus>
```

Digite `help` após o prompt, e as informações de ajuda serão exibidas. Você pode executar o `> help specific command` para ter acesso ao uso detalhado do comando específico.
```
tcaplus>help
--------------------------------------------------------------------------------
    show                 get server status related information. executing help show for details.
    dir                  add dir server url. if no dir_server_url added ,
                         commands will fail when executing.
    desc                 output current table struction description
    count                output table row count
    select               query data
    update               update record. if record does not exist then add it or update it if exists.
    insert               insert a new record (not implemented)
    delete               delete record(s)
    bson                 execute bson query
    dump                 dump records from tcaplus to file with csv format
    load                 load records from csv file and import the records to tcplus
    clean                clean table
    quit                 exit the client
    help                 follow a command to get details.
                         e.g. help show, help dir etc.
    note: tdr mode means starting client with -T, and none tdr mode starting client without -T
--------------------------------------------------------------------------------
```


## Método de execução de instrução
<br>Os métodos de execução e funcionalidades das instruções acima são mostrados abaixo.

#### Execução da operação de desc
Este comando é usado para exibir as informações de definição da tabela. Para um campo aninhado, você só pode ver que seu atributo é do tipo aninhado, mas não pode ver a definição da estrutura aninhada.
Sintaxe: `desc table name;`
```
tcaplus>desc game_players;
TableName:game_players
TableType:PROTOBUF
-------------------------------------------------------------------------
| Field                         Type                          Key       |
-------------------------------------------------------------------------
| player_id                     int64                         key       |
| player_email                  string                        key       |
| player_name                   string                                  |
| game_server_id                int32                                   |
| login_timestamp               string                                  |
| logout_timestamp              string                                  |
| is_online                     int8                                    |
| pay                           message                                 |
-------------------------------------------------------------------------
```

#### Execução da operação de count
Este comando é usado para exibir a quantidade total de registros da tabela.
Sintaxe: `count table name;`
```
tcaplus>count t1;
-------------------------------------------
| TableName                     COUNT(*)  |
-------------------------------------------
| t1                            15        |
-------------------------------------------
```

#### Exportação de dados
Você pode executar o comando `dump` para exportar todos os registros de uma tabela especificada para um arquivo .json.
Sintaxe: `dump * from table name into filename;`
```
tcaplus>dump * from player into player.txt;
--------------------------------------------------------------------------------
      dump from table("player") success. total record number is 4
--------------------------------------------------------------------------------
```

#### Importação de dados
Você pode executar o comando `load` para importar os registros de uma tabela especificada de um arquivo .csv. Os arquivos exportados com o comando `dump` não podem ser importados diretamente.
Sintaxe: `load table name from file;`
```
tcaplus>load hehe from test1;
--------------------------------------------------------------------------------
      1 records loaded successfully.
--------------------------------------------------------------------------------
```

#### Limpeza de dados da tabela
Atualmente, por motivos de segurança, a ferramenta de cliente não permite que você limpe os dados da tabela diretamente. Caso deseje limpar todos os dados da tabela, use a funcionalidade [limpeza de tabela](https://console.cloud.tencent.com/tcaplusdb/table) no console.


### Inserção de dados
Atualmente, a instrução `INSERT` não pode ser usada; em vez disso, você pode executar a instrução `UPDATE` para inserir um registro.

### Modificação de dados
Você pode executar a instrução `UPDATE` para gravar um registro. Se não houver registros correspondentes ao valor do campo da chave primária na cláusula `WHERE`, o registro será adicionado como um novo.
Sintaxe: `update table set field=value[,field 2=value 2…] where primary key field=value [and primary key field 2=value 2…];`
```
tcaplus>update tb_online set gamesvrid=4099, logintime=101 where uin=1024 and name="tcaplus_user" and region=10;
--------------------------------------------------------------------------------
        success. 
--------------------------------------------------------------------------------
update time: 5593 us
```

### Leitura de dados
Você pode executar a instrução `SELECT` para ler os dados do campo especificado.
Sintaxe: `select field[,field 2…] from table where primary key field=value [and primary key field 2=value];`
The `recDataVersion` column in the input data indicates the version number of the current record.
```
tcaplus>select gamesvrid, logintime from tb_online where uin=1024 and name="tcaplus_user" and region=10;
+------+--------------+--------+------------------+--------------+-----------+
| uin  | name         | region | recDataVersion   | gamesvrid    | logintime |
+------+--------------+--------+------------------+--------------+-----------+
| 1024 | tcaplus_user | 10     | 2                | 4099         | 101       |
+------+--------------+--------+------------------+--------------+-----------+
totally 1 record(s) responded.
query time 8686 us
```

The syntax `select * from table where primary key field=value` is supported. Segue abaixo um exemplo:
```
tcaplus>select * from test where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 7537 us
```

Os modos de saída formatados em `\G` e `\P` são compatíveis. `\G` indica saída horizontal por campo, já `\P` indica que os dados serão produzidos como uma tabela. Por padrão, os campos que não são configurados com saída formatada serão retornados no modo `\P`.
```
tcaplus>select * from hehe where id=1 and name=1 \G;
----------------------------------------1.row----------------------------------------
id: 1
name: 1
recDataVersion: 1
em: 1
responding record total:1
query time 3285 us
```

Você pode executar a instrução `SELECT` para exportar dados para um arquivo.
Sintaxe: `select * into [outfile] filename from table name where primary key=value [and primary key 2=value];`

```
tcaplus>select * into outfile test2.xml from hehe where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 5399 us
```

### Exclusão de dados
Você pode executar a instrução `DELETE` para excluir um registro escrito.
Sintaxe: `delete from table name where primary key=value [and primary key 2=value];`
```
tcaplus>delete from hehe where id=4 and name=4;
--------------------------------------------------------------------------------
        success
--------------------------------------------------------------------------------
delete time 4280 us
```
