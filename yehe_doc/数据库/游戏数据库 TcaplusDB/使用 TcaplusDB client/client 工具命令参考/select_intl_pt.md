## Visão geral
Este comando é usado para consultar todo o registro ou vários campos incluídos no registro. Se nenhum registro for correspondido, um erro será retornado.

## Sintaxe
```
select key1, key2, key3, value1, value2 [into result.csv] from table where key1 = 1 and key2 = "abc" [and -index = 1] [\P] [\G] [using tdr]
select * [into result.xml] from table where key1 = 1 and key2 = "abc" [and -index = 1] using tdr [\P];
```

## Parâmetros

|  Parâmetro          | Protobuf                                      | TDR                             | Obrigatório       |
| --------- | ---------------------------------------- | -------------------------------------------- | ------------ |
| table     | Nome da tabela                                                  | Nome da tabela                             | Sim           |
| key       | Nome do campo de chave primária. A consulta de índice global é aceita. Você pode inserir alguns valores de chave.      | Nome do campo de chave primária. Todos os valores de chave são obrigatórios.        | Sim     |
| value     | Nome do campo de chave não primária                  | Nome do campo de chave não primária                                 | Sim, pelo menos um |
| \-index   | Tabela LIST: se `\-index` for especificado, o registro de índice sob a mesma chave será retornado; se `\-index` não for especificado, todos os registros serão retornados.<br>Tabela GENERIC: não aceita | Tabela LIST: se `\-index` for especificado, o registro de índice sob a mesma chave será retornado; se `\-index` não for especificado, todos os registros serão retornados.<br>Tabela GENERIC: não aceita | Não           |
| \\P       | Latência de impressão                              | Latência de impressão                           | Não           |
| \\G       | Impressão vertical                                   | Impressão vertical                                    | Não           |
| using tdr | Não aceito                 | Quando os dados são emitidos no formato XML, a estrutura do arquivo deve obedecer estritamente à sintaxe XML. Um arquivo TDR deve ser fornecido quando o cliente for iniciado. | Não           |
| into      | Saída de dados para o arquivo                           | Saída de dados para o arquivo                           | Não           |


## Erros
Para obter mais informações, consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).

## Exemplo

```
tcaplus> select * from test_table where gameid=1234 and itemid=12323 and name='testname';
+------+------+----------+------+----+-----+
|gameid|itemid|name      |typeid|Data|uname|
+------+------+----------+------+----+-----+
|1234  |12323 |"testname"|0     |9   |"ab" |
+------+------+----------+------+----+-----+
1 records selectd, select time: 9802 us
 
tcaplus> select uname from test_table where gameid=1234 and itemid=12323 and name='testname';
+------+------+----------+-----+
|gameid|itemid|name      |uname|
+------+------+----------+-----+
|1234  |12323 |"testname"|"ab" |
+------+------+----------+-----+
1 records selectd, select time: 9457 us
 
tcaplus> select * into test.txt from test_table where gameid=1234 and itemid=12323 and name='testname';
1 records are stored to test.csv, select time: 10198 us
 
tcaplus> select * from test_table where gameid=1234 and itemid=12323 and name='testname' \P \G;
gameid: 1234
itemid: 12323
name: "testname"
typeid: 0
Data: 9
uname: "ab"
 
API ----      -1us    --->ProxyFront----      10us    --->ProxyEnd---     364us    --->SvrMainStart
|                              |                             |                           |381us
|11380us                       |4138us                       |4104us                   SvrWorkerStart
|                              |                             |                           |61us
API <---   34197us    ----ProxyFront<---      24us    ----ProxyEnd<--    3298us    ----SvrWorkerEnd
1 records selectd, select time: 11380 us
 
 
tcaplus> select * into table_list.xml from table_list where uin=99 and name = "99" and key1=99 using tdr;
11 records are stored to table_list.xml, select time: 135299 us
 
tcaplus> select c_string from table_list where uin=99 and name = "99" and key1=99;
+---+----+----+--------+
|uin|name|key1|c_string|
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
11 records selectd, select time: 102572 us
 
tcaplus> select c_string from table_list where uin=99 and name = "99" and key1=99 and -index=9;
+---+----+----+--------+
|uin|name|key1|c_string|
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
1 records selectd, select time: 9886 us
```

