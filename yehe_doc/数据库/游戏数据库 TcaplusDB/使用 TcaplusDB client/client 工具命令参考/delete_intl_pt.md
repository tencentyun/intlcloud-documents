## Visão geral
Este comando é usado para excluir um registro de uma tabela pela chave especificada. Se o parâmetro `-index` não for especificado, todos os registros que atenderem à condição serão excluídos da tabela.

## Sintaxe
```
delete from table where key1 = 1 and key2 = "abc" [and -index = 1] [by partkey];
```

## Parâmetros

|  Parâmetro          | Protobuf                                      | TDR                             | Obrigatório       |
| ---------- | ------------------------------------- | -------------------------------- | ------------ |
| table      | Nome da tabela                                        | Nome da tabela                                  | Sim           |
| key       | Nome do campo de chave primária. Todos os valores de chave são obrigatórios.             | Nome do campo de chave primária. Todos os valores de chave são obrigatórios.               | Sim       |
| value     | Nome do campo de chave não primária                  | Nome do campo de chave não primária                                 | Sim, pelo menos um nome de campo é obrigatório. |
| \-index   | Tabela LIST: você deve especificar `\-index`. Apenas o registro especificado será substituído.<br>Tabela GENERIC: não aceita | Tabela LIST: se `\-index` for especificado, o registro index-th com a mesma chave será retornado; se `\-index` não for especificado, todos os registros serão retornados.<br>Tabela GENERIC: não aceita | Não           |
| by partkey | Não aceito         | Tabela LIST: não aceita <br> Tabela GENERIC: excluir registros por chaves parciais      | Não           |


## Erros
Para obter mais informações, consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).

## Exemplo
```
tcaplus> delete from table_list where  uin=99 and name = "99" and key1=99 and -index=0;
 
delete success
 
delete time: 10263 us
 
tcaplus> delete from table_generic_xiahuaxian  where _uin=99 and name = "danmi_test_1" and _key3=4 by partkey;
 
delete success
 
delete time: 14405 us
```
