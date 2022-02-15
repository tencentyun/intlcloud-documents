## Visão geral
Este comando é usado para exportar todos os dados de uma tabela para o console ou para um arquivo.

## Sintaxe
```
## Exportação de campos parciais
dump key1, key2, value1, value2 [into result.csv] from table limit 10;
 
## Exportação como um arquivo XML
dump * [into filename] from table limit 10 using tdr;
 
## Exportação como um arquivo CSV
dump * [into filename] from table limit 10;
```

## Parâmetros

|  Parâmetro          | Protobuf                                      | TDR                             | Obrigatório       |
| ----- | --------------------------------------------------- | ------------------------------------------------------- | ------ |
| table | Nome da tabela                                                   | Nome da tabela                                                   | Sim     |
| key   | Nome do campo de chave primária. Todos os valores de chave são obrigatórios.                                | Nome do campo de chave primária. Todos os valores de chave são obrigatórios.         | Sim     |
| value | Nome do campo de chave não primária                                                 | Nome do campo de chave não primária                                                 | Não     |
| limit | Tabela LIST: a quantidade de chaves exportadas. Uma chave para vários registros.<br>Tabela GENERIC: a quantidade de registros exportados. Uma chave para um registro. | Tabela LIST: a quantidade de chaves exportadas. Uma chave para vários registros.<br>Tabela GENERIC: a quantidade de registros exportados. Uma chave para um registro. | Não     |
| using | Não aceito                                                       | Quando os dados são emitidos no formato XML, a estrutura do arquivo deve obedecer estritamente à sintaxe XML. Um arquivo TDR deve ser fornecido quando o cliente for iniciado.  | Não     |
| into  | Exportar como arquivo.                                               | Exportar como arquivo.                                               | Não     |


## Erros
Para obter mais informações, consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).

## Exemplo

```
tcaplus> dump * from table_list limit 0;
uin,name,key1,level,count,array_count,items,c_int8,c_uint8,c_int16,c_uint16,c_int32,c_uint32,c_int64,c_uint64,c_float,c_double,c_string,c_string_128K,c_string_256K,c_binary,binary,selector,single_struct,simple_struct,single_union_selector,single_union,array,c_union,union_array,c_struct,struct_array
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
 
dump 4 records successful
 
dump time: 121671 us
 
tcaplus> dump * into table_list.txt from table_list limit 0;
 
dumped 4 records successful
 
tcaplus> dump * into table_list.xml from table_list limit 0 using tdr;
 
dumped 4 records successful
```
