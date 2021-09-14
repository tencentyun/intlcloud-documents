## Cenários de operação
Quando não houver necessidade de usar o snapshot novamente, é possível excluí-lo para liberar recursos virtuais. 


## Descrições
- Quando você exclui um snapshot, apenas os dados exclusivos do snapshot são excluídos e o disco em nuvem para o qual o snapshot foi criado não será afetado.
- É possível usar um snapshot para recuperar um disco em nuvem para o status de dados quando o snapshot foi criado. Excluir um snapshot criado anteriormente para um disco em nuvem não afetará o uso contínuo dos snapshots criados posteriormente.
- **Quando um snapshot é excluído, todos os dados nele são excluídos simultaneamente e não é possível recuperá-los. Snapshots excluídos não podem ser restaurados, portanto, use com cuidado.**



## Instruções
### Exclusão de um snapshot no console
1. Faça login na página [Lista de snapshots](https://console.cloud.tencent.com/cvm/snapshot).
2. É possível excluir snapshots usando os seguintes métodos:
 a. Exclusão única: clique em **Delete (Excluir)** na linha do snapshot a ser excluído.
 b. Exclusão em lote: selecione todos os snapshots que deseja excluir (certifique-se de que os snapshots não estejam envolvidos em nenhuma tarefa) e clique em **Delete (Excluir)** no topo da lista.
3. Clique em **OK**.

### Exclusão de um snapshot com API
É possível usar a API DeleteSnapshots para excluir um snapshot. Para instruções detalhadas, consulte [Exclusão de snapshots](https://intl.cloud.tencent.com/document/product/362/15645).
