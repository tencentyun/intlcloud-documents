## Cenário de operação
Um grupo de segurança é usado como um importante método de isolamento de segurança de rede para configurar o controle de acesso à rede para um ou mais CVMs. Você pode associar instâncias do CVM a um ou mais grupos de segurança com base nas suas necessidades empresariais. Este documento descreve como associar uma instância do CVM a um grupo de segurança no console.

## Pré-requisitos
Uma instância do CVM foi criada.

## Etapas
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, clique em **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)** para ter acesso à pagina de gerenciamento de grupos de segurança.
3. Na página de gerenciamento de grupos de segurança, selecione **Region (Região)** e localize a linha do grupo para o qual deseja definir regras.
4. Na coluna de operação, clique em **Manage instance (Gerenciar instância)** para acessar a página **Associate with Instance (Associar à instância)**.
5. Nessa página, clique em **Add Association (Adicionar associação)**.
6. Na janela "Add Instance Association (Adicionar associação da instância)" exibida, selecione a instância a ser vinculada ao grupo de segurança e clique em **OK**.

## Operações subsequentes
- Para exibir todos os grupos de segurança que você criou em uma região, consulte a lista de grupos de segurança.
Para obter informações detalhadas sobre a operação, consulte [Exibição de um grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35507).
- Se você não deseja que uma instância do CVM pertença a um ou vários grupos de segurança, remova-a deles.
Para obter informações detalhadas sobre a operação, consulte [Remoção de um grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35508).
- Se sua empresa não precisar mais de um ou vários grupos de segurança, é possível excluí-los. Depois de excluir um grupo de segurança, todas as regras nele também serão excluídas.
Para obter informações detalhadas sobre a operação, consulte [Exclusão de um grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35510).

