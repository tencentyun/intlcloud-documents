## Cenário de operação
Pode ser necessário clonar um grupo de segurança nas seguintes situações:
- Você criou um grupo de segurança denominado sg-A na região A e deseja aplicar as regras de sg-A às instâncias da região B. Neste caso, você pode clonar sg-A para a região B em vez de criar outro grupo na região B.
- Sua empresa precisa executar uma nova regra de grupo de segurança. Nesse caso, você pode clonar o grupo de segurança original para backup.



## Observações
- Por padrão, apenas as regras de entrada e saída de um grupo de segurança são clonadas, mas não as instâncias associadas ao grupo.
- Os grupos de segurança podem ser clonados entre projetos ou regiões.

## Etapas

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, clique em **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)** para ter acesso à pagina de gerenciamento de grupos de segurança.
3. Na página de gerenciamento de grupos de segurança, selecione **Region (Região)** e localize a linha do grupo a ser clonado.
4. Na coluna de operação, clique em **More (Mais)** > **Clone (Clonar)**.
5. Na janela "Clone Security Group (Clonar grupo de segurança)" exibida, selecione **Target Project (Projeto de destino)** e **Target Region (Região de destino)** para a clonagem, insira um **New Name (Novo nome)** para o grupo e clique em **OK**.






