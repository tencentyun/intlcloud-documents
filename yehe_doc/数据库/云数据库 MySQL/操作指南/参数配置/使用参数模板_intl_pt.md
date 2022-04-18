Além dos modelos de parâmetros do sistema fornecidos pelo TencentDB for MySQL, você pode criar modelos de parâmetros personalizados para configurar parâmetros em lotes.

É possível usar o modelo de parâmetro para configurar e gerenciar os parâmetros de um mecanismo de banco de dados. Um modelo é como um contêiner dos valores dos parâmetros do mecanismo de banco de dados que pode ser aplicado a uma ou mais instâncias do TencentDB.
Você pode fazer login no  [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clicar em **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda para criar, visualizar e gerenciar modelos de parâmetros compatíveis com os seguintes recursos:
- Compatibilidade com modelos de parâmetros padrão.
- Criação de modelos modificando os parâmetros padrão para gerar esquemas de otimização de parâmetros personalizados.
- Importação do arquivo de configuração do MySQL `my.conf` para gerar modelos.
- Possibilita que as configurações de parâmetros sejam salvas como modelos.
- Importação de parâmetros de modelos para aplicar a uma ou mais instâncias.
>!Se os parâmetros no modelo forem atualizados, os parâmetros da instância não serão atualizados, a menos que sejam reaplicados manualmente às instâncias. 
>Você pode aplicar as alterações de parâmetro a uma ou várias instâncias importando um modelo.


## Criação de um modelo de parâmetros
É possível criar um modelo de parâmetro, modificar os valores de parâmetro e aplicar o modelo às instâncias.
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda e clique em **Create Template (Criar modelo)**.
![](https://main.qcloudimg.com/raw/bd2e7b2373beade127ddafbe46a7ba68.png)
2. Na caixa de diálogo pop-up, especifique as configurações a seguir e clique em **Create and Set Parameters (Criar e definir parâmetros)**.
 - **Template Name (Nome do modelo)**: insira um nome exclusivo para o modelo.
 - **Database Version (Versão do banco de dados)**: selecione uma versão do banco de dados.
 - **Template Description (Descrição do modelo)**: insira uma breve descrição do modelo de parâmetro.
![](https://main.qcloudimg.com/raw/a93abb9d05b05c0018c46d5efa027221.png)
3. Após a conclusão da criação, você pode modificar, importar e exportar parâmetros na página de detalhes do modelo.

## Aplicação de um modelo de parâmetro a instâncias
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates) e selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda.
2. Na lista de modelos de parâmetros, localize o modelo desejado e clique em **Apply to Instances (Aplicar a instâncias)** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/4598668de63c22bcbef5f7a20b262f02.png)
3. Na página exibida, especifique o modo de execução e as instâncias, certifique-se de que todos os valores de parâmetro estejam corretos e clique em **Submit (Enviar)**.
 - **Execution Mode (Modo de execução)**: **Immediate execution (Execução imediata)** é selecionada por padrão. Se você selecionar **During maintenance window (Durante a janela de manutenção)**, a tarefa de modificação de parâmetro será executada e entrará em vigor durante o [período de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
 - **MySQL Instance (Instância MySQL)**: selecione uma ou mais instâncias que precisam aplicar o modelo de parâmetro na região especificada.
 - **Parameter Comparison (Comparação de parâmetros)**: visualize os valores dos parâmetros alterados da instância selecionada.
 >!Antes de aplicar um modelo de parâmetro a várias instâncias, verifique se os parâmetros podem ser aplicados a essas instâncias.
 >
![](https://main.qcloudimg.com/raw/cdb5878b84b497bbea7d981cb4e9749d.png)
4. (Opcional) Se uma modificação de parâmetro ou tarefa de modificação em lote foi enviada, mas você deseja cancelá-la, selecione **[Task List (Lista de tarefas)](https://console.cloud.tencent.com/mysql/task)** na barra lateral esquerda do console, localize a tarefa e clique em **Cancel (Cancelar)** na coluna **Operation (Operação)**. Você pode cancelar uma tarefa somente antes de ser executada. O estado da tarefa deve ser "Waiting for execution (Aguardando execução)".
![](https://main.qcloudimg.com/raw/98b1462f86e0b274ab8380726c5ddc52.png)


## Copiar um modelo de parâmetro
Para incluir a maioria dos parâmetros e valores personalizados de um modelo de parâmetro existente em um novo modelo, você pode copiar o modelo existente.

### Método 1. Copiar um modelo de parâmetro existente
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda, clique no nome do modelo de parâmetro ou em **View Details (Visualizar detalhes)**, na coluna **Operation (Operação)**, na lista de modelos, e entre na página de detalhes do modelo de parâmetro.
2. Selecione **More (Mais)** > **Save as Template (Salvar como modelo)** na parte superior.
3. Na caixa de diálogo pop-up, especifique as seguintes configurações: 
  - **Template Name (Nome do modelo)**: insira um nome exclusivo para o modelo.
  - **Template Description (Descrição do Modelo)**: insira uma breve descrição do modelo de parâmetro.
4. Depois de confirmar todas as informações, clique em **Save (Salvar)**.

### Método 2. Como salvar parâmetros de uma instância como um modelo de parâmetro
1. Faça login no [console TencentDB for MySQL](https://console.cloud.tencent.com/cdb), selecione **Instance List (Lista de instâncias)** na barra lateral esquerda e clique em um ID/nome na lista de instâncias para acessar a respectiva página de gerenciamento.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Parameter Settings (Configurações de parâmetros)** e clique em **Save as Template (Salvar como modelo)**.
3. Na caixa de diálogo pop-up, especifique as seguintes configurações:
  - **Template Name (Nome do modelo)**: insira um nome para o modelo.
  - **Template Description (Descrição do Modelo)**: insira uma breve descrição do modelo de parâmetro.
4. Depois de confirmar todas as informações, clique em **Create and Save (Criar e salvar)**.


## Modificação dos valores de parâmetro em um modelo de parâmetro
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda, clique no nome do modelo de parâmetro ou em **View Details (Visualizar detalhes)**, na coluna **Operation (Operação)**, na lista de modelos, e entre na página de detalhes do modelo de parâmetro.
2. Clique em **Batch Modify Parameters (Modificação de parâmetros em lote)** ou clique em <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> na coluna **Current Value (Valor atual)** para modificar o valor do parâmetro.
>!Se você clicar em **Import Parameters (Importar parâmetros)**, será necessário fazer upload de um arquivo de configuração de parâmetro local. Para evitar falhas na importação, o arquivo de configuração deve estar no mesmo formato do arquivo de configuração do servidor de banco de dados MySQL, ou você pode usar o modelo de arquivo dos parâmetros exportados.
>
![](https://main.qcloudimg.com/raw/d582cbb01aec5e7c6072fb2b04f74b45.png)

## Importação de um modelo de parâmetro
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda, clique no nome do modelo de parâmetro ou em **View Details (Visualizar detalhes)**, na coluna **Operation (Operação)**, na lista de modelos, e entre na página de detalhes do modelo de parâmetro.
2. Clique em **Import Parameters (Importar parâmetros)**.
>!Se você clicar em **Import Parameters (Importar parâmetros)**, será necessário fazer upload de um arquivo de configuração de parâmetro local. Para evitar falhas na importação, o arquivo de configuração deve estar no mesmo formato do arquivo de configuração do servidor de banco de dados MySQL, ou você pode usar o modelo de arquivo dos parâmetros exportados.
>
3. Na caixa de diálogo pop-up, selecione um arquivo para carregar e clique em **Import and Overwrite Original Parameters (Importar e substituir parâmetros originais)**.

## Exportação de um modelo de parâmetro
### Método 1
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates) e selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda.
2. Na lista de modelos de parâmetros, localize o modelo desejado e clique em **Export (Exportar)** na coluna **Operation (Operação)**.

### Método 2
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda, clique no nome do modelo de parâmetro ou em **View Details (Visualizar detalhes)**, na coluna **Operation (Operação)**, na lista de modelos, e entre na página de detalhes do modelo de parâmetro.
2. Selecione **More (Mais)** > **Export Parameters (Exportar parâmetros)** na parte superior.

## Exclusão de um modelo de parâmetro
Se um modelo de parâmetro for criado de forma redundante ou não for mais necessário, ele poderá ser facilmente excluído.
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates) e selecione **Parameter Templates (Modelos de parâmetros)** na barra lateral esquerda.
2. Na lista de modelos de parâmetros, localize o modelo desejado e clique em **Delete (Excluir)** na coluna **Operation (Operação)**.
3. Clique em **OK** na caixa de diálogo pop-up.


## Consulte também
Para sugestões de configuração de parâmetros-chave, consulte [Sugestões sobre configurações de parâmetros](https://intl.cloud.tencent.com/document/product/236/38056).
