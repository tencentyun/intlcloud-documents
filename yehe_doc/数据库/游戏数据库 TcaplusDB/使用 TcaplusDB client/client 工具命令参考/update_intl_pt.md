## Visão geral
Este comando é usado para atualizar um registro em uma tabela declarando explicitamente os parâmetros ou importando arquivos.

## Sintaxe
```
## Declaração explícita de campos para atualizar registros
update table set value1 = 1, value2 = "abc", value3 = 0x123456 where key1 = 1 and key2 = "abc" and [-index = 1];
 
## Importação de arquivos CSV para substituir registros
update table infile file name [where -index = 0];
 
## Importação de arquivos XML para substituir registros
update table infile file name [where -index = 0] using tdr;
```

## Parâmetros

|  Parâmetro          | ProtoBuf                                      | TDR                             | Obrigatório       |
| --------- | ------------------------------------- | ------------------------------------------- | ------------ |
| table     | Nome da tabela                                   | Nome da tabela                                  | Sim           |
| key       | Nome do campo de chave primária. Todos os valores de chave são obrigatórios.             | Nome do campo de chave primária. Todos os valores de chave são obrigatórios.               | Sim       |
| value     | Nome do campo de chave não primária                  | Nome do campo de chave não primária                                 | Pelo menos um ou \* |
| \-index   | Tabela LIST: você deve especificar `\-index`. Apenas o registro especificado será substituído.<br>Tabela GENERIC: não aceita | Tabela LIST: se `\-index` for especificado, o registro index-th com a mesma chave será retornado; se `\-index` não for especificado, todos os registros serão retornados.<br>Tabela GENERIC: não aceita | Não           |
| using tdr | Não aceito                 | Quando os dados são emitidos no formato XML, a estrutura do arquivo deve obedecer estritamente à sintaxe XML. Um arquivo TDR deve ser fornecido quando o cliente for iniciado. | Não           |
| infile    | Ler os dados do arquivo.                          | Ler os dados do arquivo.                          | Não           |


## Erros
Consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).

## Exemplo
```
tcaplus> update table_list set level=99 and count= 88 where uin=99 and name = "99" and key1=99 and -index=0;
 
update success
 
update time: 117086 us
```
