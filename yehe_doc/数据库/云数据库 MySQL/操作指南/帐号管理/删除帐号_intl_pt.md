## Cenários de operação
Para desativar uma conta de banco de dados existente, ela deve ser excluída no console do TencentDB for MySQL.
>!
>- Uma conta de banco de dados não pode ser recuperada após excluída.
>- Para evitar que a exclusão acidental interrompa a operação normal das atividades, você precisa se certificar de que a conta do banco de dados a ser excluída não esteja mais em uso por nenhuma aplicação.

## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna “Operation (Operação)” para acessar a sua página de gerenciamento.
2. Selecione a guia **Database Management (Gerenciamento de banco de dados)** > **Manage Account (Gerenciar conta)**, localize a conta a ser excluída e selecione **More (Mais)** > **Delete Account (Excluir conta)**.
![](https://main.qcloudimg.com/raw/8925fb7e9e11aa87466a5c9134773689.png)
3. Na caixa de diálogo pop-up, clique em **OK** para excluir a conta.
![](https://main.qcloudimg.com/raw/c1680eda4e1abd7fb7b16d061475ada7.png)

## APIs relacionadas
| Nome da API                                                      | Descrição     |
| -------------------------------------------------------- | -------- |
| [DeleteAccounts](https://intl.cloud.tencent.com/document/product/236/17501) | Exclui uma conta do TencentDB |

