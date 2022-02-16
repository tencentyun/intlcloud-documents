## Cenários de operação
Este documento descreve como alterar a senha de conexão de um cluster no console do TcaplusDB e atualizar o tempo de expiração da senha antiga.

## Pré-requisitos
Você criou um cluster e um grupo de tabelas. Para obter mais informações, consulte [Criação de cluster](https://intl.cloud.tencent.com/document/product/1016/32714) e [Criação de grupo de tabelas](https://intl.cloud.tencent.com/document/product/1016/32716).

## Instruções
### Alteração da senha de conexão
1. Acesse a página [Lista de clusters](https://console.cloud.tencent.com/tcaplusdb/app), clique em **Change Password (Alterar senha)** em "Connection Password (Senha de conexão)" do cluster, insira a senha antiga e a nova senha, confirme a nova senha na caixa de diálogo pop-up e clique em **Confirm (Confirmar)**.
>Para "Defer Change (Adiar alteração)", você precisa selecionar **Update password (Atualizar senha)** e o tempo de expiração da senha antiga.
>
![](https://main.qcloudimg.com/raw/7aab39aa33e2e461e0a2e87b07abeeb6.png)
2. Assim que a solicitação for enviada, o tempo de expiração da senha antiga será exibido na página de detalhes do cluster, antes do qual a senha antiga permanecerá válida e você não poderá enviar outra solicitação para atualizar a senha.

### Atualização do tempo de expiração da senha antiga
>Antes da senha antiga expirar, você pode atualizar o tempo de expiração para reduzir ou estender o período antes de substituí-la.

1. Acesse a página [Lista de clusters](https://console.cloud.tencent.com/tcaplusdb/app), clique em **Change Password (Alterar senha)** em "Connection Password (Senha de conexão)" do cluster, modifique o tempo de expiração na caixa de diálogo pop-up e clique em **Confirm (Confirmar)**.
 - **Old Password (Senha antiga)**: a senha antiga que vai expirar, ou seja, a senha antiga que você digitou quando alterou a senha de conexão.
 - **New Password (Nova senha)**: a nova senha que ainda não entrou em vigor, ou seja, a nova senha que você inseriu quando alterou a senha de conexão.
 - **Defer Change (Adiar alteração)**: selecione **Update old password expiration time (Atualizar tempo de expiração da senha antiga)**.
 - **Old Password Expiration Time (Tempo de expiração da senha antiga)**: selecione um novo tempo de expiração.
![](https://main.qcloudimg.com/raw/f603e4184231af909e48129d6cce56d4.png)
2. Volte para a página de detalhes do cluster e você verá que o tempo de expiração da senha antiga foi atualizado.
>Após o tempo de expiração, a senha antiga expirará e você poderá enviar uma nova solicitação para atualizá-la.
