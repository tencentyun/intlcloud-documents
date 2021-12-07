## Cenários de operação
A partir de 23 de março de 2020, todas as operações de certificado do CLB foram conectadas ao Cloud Access Management (CAM) para autenticação. Portanto, quando uma conta de subusuário executa operações de certificado CLB, se a mensagem "Você não está autorizado para esta operação. Entre em contato com seu desenvolvedor." for exibida, é possível conceder permissões de certificado à conta de subusuário conforme as instruções abaixo.

## Pré-requisitos
A conta logada precisa ser a conta de raiz ou uma conta de subusuário com permissões CAM (ou seja, associada à política `QcloudCamFullAccess`).
>?
>- Para verificar se a conta de subusuário tem permissões CAM, vá para [Lista de usuários](https://console.cloud.tencent.com/cam) no Console CAM, entre na página de detalhes do subusuário e verifique se a política `QcloudCamFullAccess` foi associada.
> - Se a política `QcloudCamFullAccess` estiver associada, mas a mensagem "Sem permissões de API (message:GetReceiversOnAllType). Entre em contato com seu desenvolvedor." for exibida quando o subusuário realizar operações de certificado, basta ignorar e continuar. 

## Instruções
Conceda permissões de certificado através dos seguintes métodos:

### Método 1. Associar uma política personalizada
1. Faça login no [Console do CAM](https://console.cloud.tencent.com/cam/overview).
2. Na barra lateral esquerda, clique em **Policies (Políticas)**.
3. Clique em **Create Custom Policy (Criar política personalizada)** e selecione **Create by Policy Syntax (Criar por sintaxe da política)** na caixa pop-up.
4. Na página "Select Template Policy (Selecionar política de modelo)", selecione **Blank Template (Modelo em branco)** e clique em **Next (Avançar)**.
5. Na página "Edit Policy (Editar política)", digite o nome da política e o seguinte conteúdo da política na caixa de entrada "Edit Policy Content (Editar conteúdo da política)":
```
   {
    "version": "2.0",
    "statement": [
        {
            "action": "name/ssl:*",
            "resource": "qcs::ssl:::*",
            "effect": "allow",
        }
    ]
}  
```
6. Em seguida, clique em **Done (Concluído)** para retornar à página da lista "Policy (Política)".
7. No topo da página da lista "Policy (Política)", selecione **Custom Policy (Política personalizada)**, encontre a linha da política que você acabou de criar na lista e clique em **Associate User/Group (Associar usuário/grupo)** na coluna "Operation (Operação)".
![](https://main.qcloudimg.com/raw/2a0cf97e6de81cbbc3fcc6af9164bb5a.png)
8. Na caixa pop-up, selecione o usuário a ser autorizado e clique em **OK**.
![](https://main.qcloudimg.com/raw/2105e8b1ebf79f0d6b1d063aa0bcd158.png)

### Método 2. Associar uma política predefinida
1. Faça login no [Console do CAM](https://console.cloud.tencent.com/cam/overview).
2. Na barra lateral esquerda, selecione **User (Usuário)** > **User List (Lista de usuários)** para entrar na página "User List (Lista de usuários)".
3. Na linha do subusuário a ser autorizado, clique em **Authorize (Autorizar)** na barra "Operation (Operação)".
4. Na caixa pop-up, selecione `QcloudSSLFullAccess` ou `QcloudSSLReadOnlyAccess` e clique em **OK**.
![](https://main.qcloudimg.com/raw/a18245f729467395f801002f6defcb8d.png)
