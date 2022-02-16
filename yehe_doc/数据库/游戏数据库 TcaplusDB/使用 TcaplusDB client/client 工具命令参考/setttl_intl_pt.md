## Visão geral
Este comando é usado para definir uma vida útil (TTL) em milissegundos para um registro. O valor definido será reduzido pelo tempo decorrido. Quando o valor da TTL de um registro for igual a 0, o TcaplusDB vai removê-lo. Este comando só tem efeito em um único registro.

## Sintaxe
```
setttl [table] ttl=[TTL] where key1 = 1 and key2 = "abc";
```

## Parâmetros

| Parâmetro             | Obrigatório | Limite                                                   | Descrição                            |
| ---------------- | -------- | ------------------------------------------------------------ |------------------------------- |
| table            | Sim       | Não                                                       | Nome da tabela                            |
| TTL              | Sim       | O valor não pode exceder a metade do valor máximo de `uint64\_t`. Em outras palavras, o valor máximo da TTL é ULONG\_MAX/2. Um valor excedido este limite será definido para o valor máximo.    | Vida útil (TTL) em milissegundos          |
| Key na cláusula WHERE | Sim       | Todos os valores de chave são obrigatórios para a tabela do TDR.      | Os valores de chave precisam ser declarados. Vários valores de chave são unidos com `and`.  |

## Erros
Para obter mais informações, consulte [Códigos de erro](https://intl.cloud.tencent.com/document/product/1016/38791).


## Mensagens de retorno

| Situação             | Mensagem de retorno                                                   |
| -------------------- | ------------------------------------------------------------ |
| O registro não existe ou expirou. | Record does not exist or has expired\.                       |
| Falha ao definir a vida útil.            | Failed to set time to live\. The error code is \[error code\] and the error message is \[Error message\]\. |
| Vida útil definida com êxito.            | Set time to live successfully\.                              |


## Exemplo
Defina a TTL para 2.000 milissegundos:
```
tcaplus> setttl mails ttl=2000 where key1 = 1 and key2 = "abc";
Set time to live successfully.
```
