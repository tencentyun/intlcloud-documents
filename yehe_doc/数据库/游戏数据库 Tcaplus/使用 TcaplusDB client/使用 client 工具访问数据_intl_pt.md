Este documento descreve como usar a ferramenta de cliente tcaplus_client para acessar dados.

Todas as instruções DML devem usar a cláusula `WHERE` que deve conter pelo menos um campo de chave primária. Se houver várias chaves primárias, separe-as utilizando o `and`.

## Acesso do TcaplusDB por meio da ferramenta de cliente
A tcaplus_client é uma ferramenta de cliente usada para acessar tabelas do TcaplusDB e pode ser obtida no endereço de download na tabela abaixo.

O pacote de lançamento da TcaplusServiceAPI para Linux x86_64 contém a ferramenta tcaplus_client para Linux de 64 bits.

| Versão          | Data de lançamento   | Sistema operacional     | Endereço de download do pacote                                                     |
| ------------- | ---------- | ------------ | ------------------------------------------------------------ |
| 3.46.0.199033 | 28/12/2020 | Linux x86_64 | [Download](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/release/3-46/TcaplusPbApi3.46.0.199033.x86_64_release_20201210.tar.gz) |

>?
>- As operações a seguir precisam ser realizadas na instância do CVM no mesmo VPC e sub-rede em sua conta do Tencent Cloud que seu cluster do TcaplusDB.
>- Você pode baixar a TcaplusServiceAPI v3.36.0.192960 [aqui](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz).

### Instalação do cliente
Após baixar o pacote de instalação TcaplusServiceAPI, você pode [usar a ferramenta de upload](https://intl.cloud.tencent.com/document/product/213/34821) para carregá-lo na instância do CVM no mesmo VPC e sub-rede do cluster do TcaplusDB.

1. Após o upload, execute o seguinte comando para descompactar o pacote de instalação:
```
tar -xf TcaplusPbApi3.46.0.199033.x86_64_release_20201210.tar.gz -C tcaplus
```
2. Após a descompactação, entre no diretório `bin` em `tcaplus` e conceda a permissão executável da ferramenta:
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. Execute o comando `./tcaplus_client`, e o sistema solicitará que você insira as informações de parâmetro requeridas para a conexão do banco de dados. Você pode inseri-las com base nas informações do cluster.
>!No exemplo abaixo, `app_id` indica o ID de acesso do cluster, `App` indica o cluster e `zone` indica o grupo de tabelas.


```
## ./tcaplus_client
--------------------------------------------------------------------------------
  invalid parameters, please start the client as following:

    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]

    the params in [] are optional, and their order is not important.

    -a(--ap_id)    APP ID

    -z(--zone_id)    ZONE ID

    -s(--signature)    PASSWORD

    -d(--dir)    dir server addr

    -t(--table)    table to add

    -l(--log)    log file name that must be client_log.xml, and log class name be client

    -T(--tdr)    tdr filename 

    -e(--execute)    SQL command need to execute, the content should be in quotes.

    e.g. ./tcaplus_client -a 2 -z 3 -s "FE6533875C8385C3" -d 172.25.40.181:9999 -T table_test.tdr -e "select a, b from table where key = 1;" 
--------------------------------------------------------------------------------
```

### Conexão ao TcaplusDB (cenário padrão)
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

Digite `help` após o prompt e você poderá ver informações detalhadas de ajuda. Digite `> help` para ver como usar os comandos relacionados.
```
tcaplus>help
--------------------------------------------------------------------------------
      help: show usage of commands, example: "help select;".
      show: get server status related information. executing "help show;" for details.
      exit/quit: exit the client.
     count: print record number in the database.
 
      desc: print table field name and type.
    select: query records from database.
    insert: insert a new record into database.
   replace: replace a record into the database.
    update: update a record in the database.
    delete: delete record(s) from database.
 
      dump: dump records from database.
      load: load records into the database.
--------------------------------------------------------------------------------
```

### Descrição do parâmetro
| Parâmetro | Descrição                                          | Obrigatório |
| ---- | --------------------------------------------- | -------- |
| -a   | ID de acesso                                       | Sim       |
| -z   | ID do grupo de tabelas                                     | Sim       |
| -s   | Senha do cluster                                      | Sim       |
| -d   | IP e porta do cluster                            | Sim       |
| -t   | Nome da tabela                                        | Não       |
| -l   | A configuração de saída dos arquivos de log. O nome do arquivo deve ser "client_log.xml". | Não       |
| -T   | Caminho do arquivo TDR                                  | Não       |
| -e   | As instruções SQL a serem executadas                           | Não       |
| -v   | A versão a ser consultada                                      | Não       |
| <    | Redirecione as instruções SQL ao cliente para executar.                 | Não       |

### Conexão ao TcaplusDB (usando o TDR)
Para se conectar ao TcaplusDB via TDR, você deve usar os parâmetros de ativação do cliente para especificar o caminho do arquivo TDR. Você pode usar a [ferramenta TDR](#tdrgj) para converter várias bases de metadados XML em formato binário. Se houver dependências entre vários arquivos XML, o arquivo XML dependente deve ser colocado na frente da lista de parâmetros.

Exemplo:
```
[root@test-PC0 /opt]# ./tcaplus_client -a 2 -z 3 -s C12901752D0D3347 -d 8.x.x.8:9999 -T /mnt/e/tdr/2.3.table_list.tdr
 
====== Welcome to use tcaplus_client, use "help" to show usage ======
tcaplus > exit

[root@test-PC0 /opt]# ./tcaplus_client -a 2 -z 3 -s C12901752D0D3347 -d 8.x.x.8:9999 -T /mnt/e/tdr/2.3.table_list.tdr -e "show tables;"
-------------------------------------------
| Table Name                    Type      |
-------------------------------------------
| MTownRoleInfo                 GENERIC   |
| table_generic                 GENERIC   |
| table_generic_xiahuaxian      GENERIC   |
| table_list                    LIST      |
| test_table                    GENERIC   |
-------------------------------------------
```

<span id = "tdrgj"></span>

#### Ferramenta TDR
Você precisa usar a ferramenta TDR para gerar um arquivo TDR, que é gerado principalmente pelo arquivo de definição de dados (estrutura TDR em formato XML). Baixe a ferramenta [aqui](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tdr).

Exemplo:
```
tdr -B -o ov_res.tdr ov_res.xml
        # Converta bases de metadados XML em bancos de dados binários TDR.
tdr -C -o ov_res.c --old_xml_tagset  ov_res.xml
        # Converta bases de metadados em formato XML antigo (usando o conjunto de tags antigo) em arquivos .c.
tdr -H -O "include" --add_custom_prefix="m_" --no_type_prefix
        # Converta bases de metadados XML para arquivos .h que são salvos no diretório "include".
        # Adicione o prefixo "m_" ao nome do membro de struct/union, mas não adicione um prefixo de tipo.
tdr -G -m Pkg -x ATTR -o Pkg.xml net_protocol.xml
        # Gere um arquivo de configuração em formato XML com pacote (um pacote de estrutura de dados customizado pelo usuário).
tdr -T -u prefixfile
        # Exporte a tabela de prefixos do membro de dados usado ao gerar o arquivo .h para o arquivo "prefixfile".
tdr -A --indent-size=8 net_protocol.xml
        # Gere arquivos de classe ActionScript3 de acordo com o protocolo descrito em "net_protocol.xml". Os arquivos de classe gerados são todos recuados com 8 espaços.
tdr -P --indent-size=8 net_protocol.xml
        # Gere arquivos de classe C++ de acordo com o protocolo descrito em "net_protocol.xml". Os arquivos de classe gerados são todos recuados com 8 espaços.
tdr -S --indent-size=8 net_protocol.xml
        # Gere arquivos de classe C# de acordo com o protocolo descrito em "net_protocol.xml". Os arquivos de classe gerados são todos recuados com 8 espaços.
tdr -E 0x83010404
        # Consulte as informações de erro do código de erro 0x83010404.
```

#### Ferramenta tdr2xml
A ferramenta tdr2xml pode descompilar o arquivo de metadados binários em um arquivo de metadados XML. Baixe a ferramenta [aqui](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tdr2xml).

Sintaxe:
```
tdr2xml   [-o --out_file=FILE] [-h --help] [-v --version] DRFILE
A descrição de cada parâmetro é como segue:
-o, --out_file=FILE: especifique o nome do arquivo de saída. Valor padrão: a.xml.
-h, --help: saída de ajuda.
-v, --version: saída das informações da versão.
```

Exemplo:
```
tdr2xml –o net_cs.xml  net_cs.tdr
```
Converta o arquivo de descrição de metadados em formato binário personalizado salvo no arquivo "net_cs.tdr" em um arquivo de descrição em formato XML.
