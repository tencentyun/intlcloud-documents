## Visão geral
Este comando é usado para importar dados em formato CSV ou XML para atualizar ou adicionar registros.

## Sintaxe
```
## Importação de um arquivo XML
load table infile filename using tdr;
 
## Importação de um arquivo CSV
load table infile filename;
```

## Parâmetros

|  Parâmetro          | Protobuf                                      | TDR                             | Obrigatório       |
| --------- | -------------- | ------------------------------------------------------------ | ------ |
| table     | Nome da tabela         | Nome da tabela                                                      | Sim     |
| using tdr | Não aceito                 | Quando os dados no formato XML são importados, a estrutura do arquivo deve obedecer estritamente à sintaxe XML. Um arquivo TDR deve ser fornecido quando o cliente for iniciado. | Não           |
| infile    | Ler os dados do arquivo.                          | Ler os dados do arquivo.                          | Sim           |

## Erros
Para obter mais informações, consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).

## Exemplo
```
tcaplus> load table_list infile table_list_dump.xml using tdr;
loaded 49 records successful
 
tcaplus> load table_list infile table_list-dump.txt;
loaded 98 records successful
```
