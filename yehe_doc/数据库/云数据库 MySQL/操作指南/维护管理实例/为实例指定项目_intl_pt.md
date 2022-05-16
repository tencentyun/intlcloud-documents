O TencentDB for MySQL permite a atribuição de instâncias a projetos diferentes para gerenciamento. As observações para atribuição estão listadas abaixo:
- As réplicas somente leitura são as instâncias associadas da instância de origem (source) e devem estar no mesmo projeto que a instância de origem (source).
- Atribuir e reatribuir instâncias do TencentDB não afetará os serviços fornecidos pelas instâncias.
- Os usuários precisam especificar os projetos aos quais as instâncias pertencem ao adquiri-las. O projeto padrão é “Default Project (Projeto padrão)”.
- As instâncias atribuídas podem ser reatribuídas a outros projetos por meio da funcionalidade **Assign to Project (Atribuir ao projeto)**.

## Instruções
1. Faça login no [console do MySQL](https://console.cloud.tencent.com/cdb/), selecione uma instância e clique em **More (Mais)** > **Assign to Project (Atribuir ao projeto)** na parte superior da lista de instâncias.

   ![](https://main.qcloudimg.com/raw/d1fe0ad3b002172fbb6418cc8ba830d5.png)

2. Na caixa de diálogo pop-up, selecione um projeto e clique em **OK**.
  ![](https://main.qcloudimg.com/raw/f547428bb9ae2fc0d2d8105cff950b85.png)
