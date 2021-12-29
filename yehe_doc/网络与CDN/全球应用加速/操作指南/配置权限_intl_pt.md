Uma conta raiz ou outras contas com permissões de AdministratorAccess (acesso de administrador) podem atribuir permissão de leitura/gravação ou somente leitura do GAAP a contas de colaboradores, configurando permissões de gerenciamento de acesso.

Existem duas maneiras de o usuário autorizar a conta de colaborador: associando uma política a um usuário ou associando um usuário a uma política. Para obter mais informações, consulte [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583).

## Preparações
1. Faça login na conta raiz ou em outra conta com permissões de AdministratorAccess (acesso de administrador) no [Console do Tencent Cloud](https://console.cloud.tencent.com/).
2. Na navegação superior, selecione **Cloud Products (Produtos de nuvem)** > **Manage and Audit (Gerenciar e auditar)** > ** [Cloud Access Management](https://console.cloud.tencent.com/cam/policy)**, para acessar o console do CAM.
>Você também pode acessar o console do gerenciamento de acesso selecionando **Your Account Name (Nome da sua conta)** > **Access Management (Gerenciamento de acesso)** no canto superior direito do console.

## Instruções
### Associação de um usuário a uma política
1. Na barra lateral esquerda, clique em **Policy (Política)** para acessar a página de gerenciamento.
2. Na barra de pesquisa, digite **GAAP**. Dois resultados foram encontrados. Selecione Policy Permissions (Permissões da política) e clique em **Associate user/group (Associar usuário/grupo)**.
![1](https://main.qcloudimg.com/raw/06fc88f33dbc935ca2b65948fb3343e3.png)
3. Selecione o usuário a ser autorizado e clique em **OK**. O usuário foi autorizado.
![](https://main.qcloudimg.com/raw/61df6a1fd920c302c0f2b2f68c79f4a2.png)

### Associação de uma política a um usuário
1. Na barra lateral esquerda, clique em **User (Usuário)** > **User List (Lista de usuários)** para acessar a página de gerenciamento.
2. Encontre a linha na lista que contém o usuário a ser autorizado. Na coluna de operação, clique em **Authorize (Autorizar)**.
![](https://main.qcloudimg.com/raw/740bfd484b9df92eb13bb9517c6238e1.png)
3. Pesquise por **GAAP** na lista de associações. Selecione a política a ser autorizada e clique em **OK**. O usuário foi autorizado.
![](https://main.qcloudimg.com/raw/7a602d2eefa9ed3ba69ca72df39616a7.png)

### Verificação e remoção de permissões
Os usuários autorizados podem verificar e remover as permissões clicando nos nomes de usuários na [Lista de usuários](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/da41405cfc21806881e2c86d9bc2823e.png)
