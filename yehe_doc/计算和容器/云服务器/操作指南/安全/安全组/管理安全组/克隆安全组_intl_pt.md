## Cenário
Pode ser necessário clonar um grupo de segurança se você:
- Criou um grupo de segurança sg-A na região A e deseja aplicar as mesmas regras a uma instância na região B. É possível clonar sg-A para a região B, em vez de criar um novo grupo de segurança do zero.
- Precisa de um novo grupo de segurança para o seu serviço, mas deseja clonar o grupo de segurança antigo como backup.



## Observações
- Por padrão, ao clonar um grupo de segurança, apenas as regras são clonadas, não a associação com as instâncias.
- É possível clonar um grupo de segurança entre projetos e regiões.

## Instruções

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, selecione **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)**. A página Security Group (Grupo de segurança) é exibida.
3. Selecione a região desejada. Uma lista de grupos de segurança da região é exibida.
4. Localize o grupo de segurança desejado e clique em **More (Mais)**. Em seguida, clique em **Clone (Clonar)**. A página **Clone security group (Clonar grupo de segurança)** é exibida.
5. Selecione uma **Target region (Região de destino)** e o **Target project (Projeto de destino)** e insira um **New name (Novo nome)** para o novo grupo de segurança. Clique em **OK**.






