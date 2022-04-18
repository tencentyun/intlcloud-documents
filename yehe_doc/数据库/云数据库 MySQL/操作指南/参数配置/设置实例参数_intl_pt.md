
Você pode visualizar e modificar determinados parâmetros além de consultar os logs de modificação deles no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb).

## Observações
- Para garantir a estabilidade da instância, apenas alguns parâmetros podem ser modificados no console. Esses parâmetros são exibidos na página **Parameter Settings (Configurações de parâmetros)**.
- Se o parâmetro modificado exigir que a reinicialização da instância seja efetivada, o sistema perguntará se você deseja reiniciar. Recomendamos que você faça isso fora do horário de pico e garanta que seu aplicativo tenha um mecanismo de reconexão.
- Se você deseja retornar à fórmula padrão, limpe os parâmetros inseridos e aplique.

## Modificação de parâmetros na lista de parâmetros
### [Modificação de parâmetros em lotes](id:plxgcs)
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID de instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a página de gerenciamento de instâncias.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configuração de parâmetros)** e clique em **Batch Modify Parameters (Parâmetros de modificação do lote)**.
![](https://main.qcloudimg.com/raw/82c535bd50543645831988ca2e9b688e.png)
3. Localize os parâmetros desejados e modifique seus valores na coluna **Current value (Valor atual)**. Após confirmar que tudo está correto, clique em **Confirm Modification (Confirmar modificação)**.
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. Na janela pop-up, selecione o **execution mode (modo de execução)** e clique em **OK**.
>?
>- Se você selecionar **Immediate execution (Execução imediata)**, a tarefa de modificação de parâmetro será executada e entrará em vigor imediatamente.
>- Se você selecionar **During maintenance time (Durante o tempo de manutenção)**, a tarefa de modificação de parâmetro será executada e terá efeito durante o [tempo de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
>

### [Modificação de um parâmetro](id:xgdgcs)
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique em um ID de instância na lista de instâncias para entrar na página de gerenciamento da instância.
2. Na guia **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configurações de parâmetros)**, localize na lista de parâmetros aquele que deseja e clique em <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> na coluna **Current Value (Valor atual)**.
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. Modifique o valor dentro das restrições indicadas na coluna **Acceptable Values (Valores aceitáveis)** e clique em <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> para salvar a modificação. Você pode clicar em <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> para cancelar a operação.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. Na janela pop-up, selecione o **execution mode (modo de execução)** e clique em **OK**.
>?
>- Se você selecionar **Immediate execution (Execução imediata)**, a tarefa de modificação de parâmetro será executada e entrará em vigor imediatamente.
>- Se você selecionar **During maintenance time (Durante o tempo de manutenção)**, a tarefa de modificação de parâmetro será executada e terá efeito durante o [tempo de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Modificação dos parâmetros importando modelo de parâmetro
### Opção 1. Importação de um modelo de parâmetro na página "Parameter Settings (Configurações de parâmetros)"
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique em um ID na lista de instâncias para entrar na respectiva página de gerenciamento.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configurações de parâmetros)** e clique em **Custom Template (Modelo personalizado)**. (Se você ainda não configurou um modelo personalizado comumente usado, pode selecionar **Custom Template (Modelo personalizado)** na barra lateral esquerda no console do TencentDB for MySQL, clicar em **Create Template (Criar modelo)** para configurar um modelo de parâmetro e importá-lo a partir do modelo personalizado conforme descrito na etapa 2.)
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. Na janela pop-up, selecione um modelo de parâmetro e clique em **Import and Overwrite Original Parameters (Importar e substituir parâmetros originais)**.
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)
4. Depois de confirmar todas as informações, clique em **Confirm Modification (Confirmar modificação)**.
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. Na janela pop-up, selecione o **execution mode (modo de execução)** e clique em **OK**.
>?
>- Se você selecionar **Immediate execution (Execução imediata)**, a tarefa de modificação de parâmetro será executada e entrará em vigor imediatamente.
>- Se você selecionar **During maintenance time (Durante o tempo de manutenção)**, a tarefa de modificação de parâmetro será executada e terá efeito durante o [tempo de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
>

### Opção 2. Modificação dos parâmetros importando um arquivo de configuração de parâmetro
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID na lista de instâncias e entre na respectiva página de gerenciamento.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configuração de parâmetros)** e clique em **Import Parameters (Importar parâmetros)**.
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. Clique em **Select File (Selecionar arquivo)** para localizar o arquivo de parâmetro desejado e clique em **Import and Overwrite Original Parameters (Importar e substituir parâmetros originais)**.
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. Depois de confirmar todas as informações, clique em **Confirm Modification (Confirmar modificação)**.
5. Na janela pop-up, selecione o **execution mode (modo de execução)** e clique em **OK**.
>?
>- Se você selecionar **Immediate execution (Execução imediata)**, a tarefa de modificação de parâmetro será executada e entrará em vigor imediatamente.
>- Se você selecionar **During maintenance time (Durante o tempo de manutenção)**, a tarefa de modificação de parâmetro será executada e terá efeito durante o [tempo de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).


### Opção 3. Importação de um modelo de parâmetro na página "Parameter Template (Modelo de parâmetro)"
Para obter mais informações, consulte [Gerenciamento de modelo de parâmetro > Aplicação de um modelo de parâmetro a um banco de dados](https://intl.cloud.tencent.com/document/product/236/31906).

## Restauração do modelo padrão
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID na lista de instâncias e entre na respectiva página de gerenciamento.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configurações de parâmetros)**, clique em **Default Template (Modelo padrão)** e selecione **High-Stability Template (Modelo de alta estabilidade)** ou **High-Performance Template (Modelo de alto desempenho)** e clique em **Import and Overwrite Original Parameters (Importar e substituir os parâmetros originais)**.
![](https://qcloudimg.tencent-cloud.cn/raw/030f986ea488796d5c084cb97aec5d6b.png)
3. Clique em **Confirm Modification (Confirmar modificação)** para redirecionar para a janela de confirmação de modificação de parâmetro.
![](https://qcloudimg.tencent-cloud.cn/raw/5ba2e9ba71f33211db43637e0aed8f37.png)
4. Na janela pop-up, selecione o **execution mode (modo de execução)**, leia e indique seu consentimento com as **restart rules (regras de reinicialização)** e clique em **OK**.
>?
>- Se você selecionar **Immediate execution (Execução imediata)**, a tarefa de modificação de parâmetro será executada e entrará em vigor imediatamente.
>- Se você selecionar **During maintenance time (Durante o tempo de manutenção)**, a tarefa de modificação de parâmetro será executada e entrará em vigor durante o [tempo de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Fórmula do parâmetro
Você pode usar uma fórmula para definir os parâmetros de instância. Para fazer isso, defina os parâmetros relacionados à especificação da instância como uma fórmula e, quando a especificação da instância for alterada, os valores dos parâmetros na fórmula serão alterados adequando-se dinamicamente. Além disso, eles continuarão efetivos após a alteração da especificação. Dessa forma, a instância está sempre no estado ideal para executar os negócios sem problemas.

Tomando o valor `{DBinitMemory\*786432}` do parâmetro `innodb_buffer_pool_size` como exemplo, quando o `DBinitMemory` é alterado na especificação da instância, a configuração do parâmetro não precisa ser modificada e o valor de `innodb_buffer_pool_size` será alterado automaticamente.
![](https://qcloudimg.tencent-cloud.cn/raw/696a0d3be52c058124f7c678a18e6b27.png)

A sintaxe de expressão é suportada da seguinte forma:

| Tipo suportado | Descrição | Amostra |
| -------- | ------------------------------------------------------------ | --------------------- |
| Variável   | <li>DBinitMemory: tamanho da memória da especificação da instância, que é um inteiro. Por exemplo, se o tamanho da memória da especificação da instância for 4.000 MB, o valor de `DBinitMemory` será 4000<li>.DBInitCpu: número de núcleos de CPU da especificação da instância, que é um número inteiro. O valor do parâmetro `innodb_buffer_pool_size` no TencentDB for MySQL deve estar entre 50% e 90% do tamanho da memória. Se o valor configurado estiver acima de 90% ou abaixo de 50%, ele será automaticamente convertido para 90% ou 50% respectivamente. | {DBinitMemory*786432} |
| Operador | Sintaxe da fórmula: deve ser colocada entre chaves (`{}`).  <li>Operador de divisão (/): divide o dividendo pelo divisor e retorna um quociente inteiro. Se o resultado do cálculo for um número decimal, apenas a parte inteira será mantida. Números decimais não são compatíveis; por exemplo, `{MIN(DBInitMemory/4+500,1000000)}` em vez de `{MIN(DBInitMemory\*0.25+500,1000000)}` é compatível.<li>Operador de multiplicação (*): multiplica dois números e retorna um inteiro como produto. Se o resultado do cálculo for um número decimal, apenas a parte inteira será mantida. O cálculo do número decimal não é suportado. | - |
| Função   | <li>MAX(): | retorna o maior valor em uma lista de fórmulas de inteiros ou parâmetros. <li>MIN(): retorna o menor valor em uma lista de fórmulas de inteiros ou de parâmetros.</li> | {MAX(DBInitCpu/2,4)} |


## Exportação de configuração de parâmetro como arquivo
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID na lista de instâncias e entre na respectiva página de gerenciamento.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configuração de parâmetros)** e clique em **Export Parameters (Exportar parâmetros) para exportar o arquivo de configuração do parâmetro.
![](https://main.qcloudimg.com/raw/6885ffbc45f3154ed203551a309e1848.png)

## Exportação da configuração de parâmetro como modelo
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID na lista de instâncias e entre na respectiva página de gerenciamento.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configuração de parâmetros)** e clique em **Save as Template (Salvar como modelo)** para salvar a configuração de parâmetro existente como um modelo de parâmetro.
![](https://main.qcloudimg.com/raw/fca4ec16b316948af812db9988d0c92c.png)

## Personalizar a janela de tempo para aplicar modificações de parâmetro
Antes de confirmar a modificação do parâmetro, a caixa de diálogo "Modify Parameters (Modificar parâmetros)" será exibida para você selecionar uma janela de tempo personalizada para que a modificação seja efetivada.
>?Se você selecionar **During maintenance time (Durante o tempo de manutenção)**, a tarefa de modificação de parâmetro será executada e será efetivada durante o [tempo de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
>
![](https://main.qcloudimg.com/raw/00d4892fb614dd285cdec91a4a74cf2d.png)

## Cancelamento da tarefa de modificação de parâmetro
Se uma modificação de parâmetro ou tarefa de modificação em lote foi enviada, mas você deseja cancelá-la, selecione **[Lista de tarefas](https://console.cloud.tencent.com/mysql/task)** na barra lateral esquerda do console, localize a tarefa e clique em **Cancel (Cancelar)** na coluna **Operation (Operação)**. Você pode cancelar uma tarefa somente antes de ser executada. O estado da tarefa deve ser **Waiting for execution (Aguardando execução)**.
![](https://main.qcloudimg.com/raw/566fd9374d0d59b38ceb99d310b782a9.png)

## Como visualizar logs de modificação de parâmetros
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID na lista de instâncias e entre na respectiva página de gerenciamento.
2. Na guia **Database Management (Gerenciamento de banco de dados)** > **Parameter Setting (Configurações de parâmetros)**, clique em **Recent Modifications (Modificações recentes)** à direita.
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. Você pode visualizar os registros de modificação de parâmetros recentes aqui.

## Operações subsequentes
- Você pode usar modelos para gerenciar os parâmetros do banco de dados em lotes. Para obter mais informações, consulte [Gerenciamento de modelo de parâmetro](https://intl.cloud.tencent.com/document/product/236/31906).
- Para sugestões de configuração de parâmetros-chave, consulte [Sugestões sobre configurações de parâmetros](https://intl.cloud.tencent.com/document/product/236/38056).

