
Este documento descreve como usar a sintaxe de dica no proxy de banco de dados.

A sintaxe de dica pode ser usada para forçar a execução de solicitações de SQL na instância especificada. Uma dica tem a prioridade de roteamento mais alta. Por exemplo, não está sujeita a restrições de consistência e transação. Avalie cuidadosamente a necessidade em seu cenário de negócios antes de usar.

>!Ao usar a ferramenta de linha de comando do MySQL para conectar e usar a instrução `HINT`, você precisa adicionar a opção `-c` no comando; caso contrário, a dica será filtrada pela ferramenta.
>
Atualmente, três tipos de dicas são suportados:
- Atribuir à instância de origem para execução:
```
/* to master */
/*FORCE_MASTER*/   
```  
- Atribuir a uma instância somente leitura para execução:
```
/* to slave */
/*FORCE_SLAVE*/  
```  
- Especificar uma instância para execução:
```
/* to server server_name*/
```
`server_name` pode ser um ID curto, como `/* to server test_ro_1 */`.

