Para ativar o registro em tempo real como uma subconta ou colaborador, você precisa solicitar à conta raiz, ou subconta que tenha permissões de administrador, para conceder acesso ao seguinte:

1. Política predefinida: `QcloudCamSubaccountsAuthorizeRoleFullAccess`
2. Política personalizada: `cdn_PassRole`

## Instruções

1. Associe a política predefinida `QcloudCamSubaccountsAuthorizeRoleFullAccess` à subconta ou colaborador.
   A conta raiz/subconta com permissões de administrador precisa fazer login no console do CAM e selecionar **Policy (Política)** na barra lateral esquerda. Pesquise a política predefinida `QcloudCamSubaccountsAuthorizeRoleFullAccess` e clique em **Associate Users/Groups (Associar usuários/grupos)** à direita da política. Na caixa de diálogo pop-up, selecione uma subconta/colaborador a ser associado.

2. Crie uma política personalizada `cdn_PassRole` e associe a política à subconta ou colaborador.
   1. A conta raiz/subconta com permissões de administrador precisa fazer login no console do CAM e selecionar **Policy (Política)** na barra lateral esquerda, e então clicar em **Create Custom Policy (Criar política personalizada)**: Na caixa de diálogo pop-up, selecione **Create by Policy Syntax (Criar por sintaxe de política)**. 

   2. Na página **Create by Policy Syntax (Criar por sintaxe de política)**, selecione **Blank Template (Modelo em branco)** e clique em **Next (Avançar)**. Na página **Edit Policy (Editar política)**, insira o nome e o conteúdo da política conforme mostrado abaixo antes de clicar em **Done (Concluído)**.

      A sintaxe da política é a seguinte:
```
{
 "version": "2.0",
 "statement": [
     {
         "effect": "allow",
         "action": [
                 "cam:PassRole"
         ],
            "resource": [
                "qcs::cam::uin/${OwnerUin}:roleName/CDN_QCSRole"
            ]
     }
 ]
}
```
${OwnerUin}` deve ser substituído pelo ID da conta raiz, que pode ser obtido no console do CAM.
 3. Associe a política personalizada `cdn_PassRole` à subconta ou colaborador.
Na página **Policy (Política)**, a política personalizada `cdn_PassRole` criada é exibida, ou então é possível pesquisar a política pelo respectivo nome. Clique em **Associate Users/Groups (Associar usuários/grupos)** à direita da política. Na caixa de diálogo pop-up, selecione uma subconta/colaborador a ser associado.

3. Depois que todas as associações de política forem concluídas, a subconta/colaborador poderá ativar o registro em tempo real conforme solicitado no console.

