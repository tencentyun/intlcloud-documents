## Visão geral
Este comando é usado para consultar a vida útil (TTL) em milissegundos de um registro. Após um registro for configurado com a TTL, você pode usar `getttl` para consultar a TTL de sua chave, ou seja, quanto tempo falta para a chave ser removida por expiração. Este comando pode consultar a TTL de apenas um registro.

## Sintaxe
```
getttl from [table]  where key1 = 1 and key2 = "abc";
```

## Parâmetros

| Parâmetro             | Obrigatório | Limites de uso                     | Descrição                            |
| ---------------- | -------- | ---------------------------- | ------------------------------- |
| table            | Sim       | Nenhum                           | Nome da tabela                            |
| key na cláusula WHERE | Sim       | Tabela do TDR: todos os valores de chave são obrigatórios | Especifique o valor de uma chave. Vários valores são separados por `and`. |

## Erros
Para obter mais informações, consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).

## Mensagens de retorno

| Situação                                 | Mensagem de retorno                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| A chave não existe ou expirou.                     | Record does not exist or has expired\.                       |
| A chave existe, mas sua TTL não foi especificada. | Record exists and no expiration time is set \(permanent\)\.  |
| Falha ao consultar a TTL.                                 | Failed to get time to live\. The error code is \[error code\] and the error message is \[Error message\]\. |
| TTL consultada com êxito.                                 | The time to live is \[TTL\] milliseconds\.                   |


## Exemplo
Consulte a TTL de um registro:
```
tcaplus> getttl from mails where key1 = 1 and key2 = "abc";
The time to live is 2000 milliseconds.
```
