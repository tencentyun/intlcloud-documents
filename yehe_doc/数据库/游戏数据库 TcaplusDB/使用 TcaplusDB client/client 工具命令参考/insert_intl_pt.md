## Visão geral
Este comando é usado para inserir uma entrada de dados em uma tabela declarando explicitamente os parâmetros ou importando arquivos.

## Sintaxe
```
## Declaração explícita de parâmetros para inserir dados
insert into table (key1, key2, value1, vlaue2) values (1, "abc", 2, "def") [after -1] [shift none/head/tail];

## Importação de um arquivo CSV para inserir dados
insert into table infile result.csv [after -1] [shift none/head/tail];

## Importação de um arquivo XML para inserir dados desde que o arquivo TDR seja fornecido na inicialização do cliente
insert into table infile result.xml [after -1] [shift none/head/tail] using tdr;
```

## Parâmetros

|  Parâmetro          | Protobuf e TDR                                    | Obrigatório       |
| --------- | ------------------------------------------------------------ | ------------ |
| table     | Nome da tabela                                                  | Sim           |
| key       | Nome do campo de chave primária                                                   | Sim           |
| value     | Nome do campo de chave não primária                                                 | Sim, pelo menos um |
| after     | Tabela LIST: <br> n>0 indica que os dados serão inseridos após os primeiros n dados<br>n=-2 indica que os dados serão inseridos no início da fila<br>n=-1 indica que os dados serão inseridos no final da fila<br>n<-2: não aceito <br>Tabela GENERIC: esse campo não é aceito. | Não          |
| shift     | Se o tamanho da tabela exceder o valor máximo, você poderá especificar como limpar os dados de forma automática. Valores válidos: <br>`none`: nenhum dado será limpo<br>`head`: os dados no início da fila serão limpos<br>tail: os dados no final da fila serão limpos. | Não |
| using tdr | A tabela do Protobuf não aceita esse parâmetro. Para inserir dados na tabela do TDR, importe um arquivo XML cuja estrutura deve obedecer estritamente à sintaxe XML. Além disso, um arquivo TDR deve ser fornecido quando o cliente for iniciado. | Não           |
| infile    | Ler os dados do arquivo                                             | Não           |


## Erros
Para obter mais informações, consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).

## Exemplo
Baixe os arquivos de exemplo [result.xml](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/result.xml) e [result.csv](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/result.csv).

```
tcaplus>insert into game_players (player_id,player_name,player_email,game_server_id) values (2,name,email,2);
insert success
 
insert time: 45322 us
 
tcaplus> Insert into table_list (uin, name, key1) values (99,99,99) after -1 shift tail;
 
insert success
 
insert time: 22464 us
 
tcaplus> Insert into table_list infile result.xml  using tdr;
 
 
insert success
 
insert time: 9493 us
 
tcaplus> Insert into table_list infile result.csv;
 
 
insert success
 
insert time: 22368 us
```

