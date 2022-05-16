## Visão geral
Você pode gerenciar as permissões de contas de banco de dados existentes no console do TencentDB for MySQL. Especificamente, você pode conceder ou remover contas de banco de dados globais, assim como permissões em nível de objetos.

## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique no ID da instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de gerenciamento.
2. Selecione a guia **Database Management (Gerenciamento de banco de dados)** > **Manage Account (Gerenciar conta)**, localize a conta para a qual deseja modificar as permissões e clique em **Modify Permissions (Modificar permissões)**.
![](https://main.qcloudimg.com/raw/144f93c6415892d0fe828f3cf267c94e.png)
3. Na caixa de diálogo pop-up, marque ou desmarque as permissões e clique em **OK** para concluir a modificação.
 - **Global Privileges (Privilégios globais)**: conceda permissões globais a todos os bancos de dados na instância.
 - **Object Level Privileges (Privilégios em nível de objetos)**: conceda permissões para determinados bancos de dados na instância.
![](https://main.qcloudimg.com/raw/19e5e35796516b6a3cd5a346ce4dcd74.png)

## APIs relacionadas
| Nome da API                                                      | Descrição     |
| ------------------------------------------------------------ | ------------ |
| [ModifyAccountPrivileges](https://intl.cloud.tencent.com/document/product/236/17496) | Modifica as permissões de contas de instância do TencentDB |

