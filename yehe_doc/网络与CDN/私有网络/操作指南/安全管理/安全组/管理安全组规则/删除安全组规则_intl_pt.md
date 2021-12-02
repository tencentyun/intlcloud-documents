## Cenário de operação
Se uma regra de grupo de segurança não for mais necessária, é possível excluí-la.

## Pré-requisitos
- Você criou um grupo de segurança e adicionou regras de grupo de segurança ao grupo.
Para obter informações sobre como criar um grupo de segurança e adicionar regras a ele, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35513).
- Você confirmou que sua instância do CVM não precisa permitir ou proibir o acesso à internet ou à rede privada.

## Etapas
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, clique em **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)** para ter acesso à pagina de gerenciamento de grupos de segurança.
3. Na página de gerenciamento de grupos de segurança, selecione **Region (Região)** e localize a linha do grupo cujas regras devem ser excluídas.
4. Na coluna de operação, clique em **Modify Rules (Modificar regras)** para acessar a página de regras do grupo de segurança.
5. Na página de regras do grupo de segurança, clique na guia **Inbound Rules or Outbound Rules (Regras de entrada ou Regras de saída)** com base na direção (entrada ou saída) das regras a serem excluídas.
6. Localize a regra do grupo de segurança desejada e clique em **Delete (Excluir)**.
7. Na janela pop-up, clique em **OK**.



