
## Visão geral
O TencentDB for MySQL oferece suporte à importação de arquivos SQL no console. Este recurso permite executar instruções SQL no banco de dados selecionado. Você também pode usar esse recurso para criar bancos de dados/tabelas e alterar a estrutura da tabela para inicializar ou modificar a instância.
>?Apenas instâncias do TencentDB for MySQL de dois e três nós permitem a importação de arquivos SQL.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID de instância ou em **Manage (Gerenciar)**, na coluna **Operation (Operação)** para acessar a página de gerenciamento da instância.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Database List (Lista de banco de dados)** e clique em **Import Data (Importar dados)**.
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
3. Na página pop-up, clique em **Add File (Adicionar arquivo)** para importar o arquivo. Depois que o upload for concluído, clique em **Next (Avançar)**.
>?
>- Para evitar a indisponibilidade do banco de dados causada pela corrupção das tabelas do sistema, não importe dados das tabelas do sistema, como a tabela `mysql.user`. 
>- Somente importação incremental é compatível. Se houver dados obsoletos no banco de dados, limpe os dados antes da operação de importação.
>- Um único arquivo SQL a ser importado não pode exceder 2 GB. O nome do arquivo pode conter apenas letras, dígitos e sublinhados.
>- Os arquivos enviados são válidos por 14 dias e serão excluídos automaticamente após a expiração.
>
<img src="https://main.qcloudimg.com/raw/fd6c70707a8722ca64a87f71978e2a2a.png">
4. Na página de seleção de banco de dados, selecione o banco de dados de destino e clique em **Next (Avançar)**.
5. Na página de confirmação, após assegurar que os dados importados estão corretos, insira a conta, a senha e clique em **Import (Importar)**.
>!
>- A importação não pode ser revertida. Confirme as informações de importação.
>- Se você esqueceu a senha, redefina-a conforme instruído em [Redefinir senha](https://intl.cloud.tencent.com/document/product/236/31901).
> 
![](https://main.qcloudimg.com/raw/e21ccbe6c1f0a95cd46b4387fea1fab1.png)

