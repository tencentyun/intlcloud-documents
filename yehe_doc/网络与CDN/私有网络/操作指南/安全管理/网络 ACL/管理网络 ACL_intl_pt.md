## Criação de ACLs de rede
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** -> **Network ACL (ACL de rede)** no diretório à esquerda para acessar a página de gerenciamento.
3. Selecione a região e o VPC na parte superior da lista e clique em **+New (+Novo)**.
4. Digite o nome na janela pop-up, selecione o VPC ao qual ela pertence e clique em **OK**.
![](https://main.qcloudimg.com/raw/3e5444cc57b2da457c2cd9db221dd1d3.png)
5. Na página da lista, clique no ID da ACL correspondente para acessar sua página de detalhes, na qual você pode adicionar regras de ACL e associá-las a sub-redes.

## Adição de regras de ACL de rede
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** -> **Network ACL (ACL de rede)** no diretório à esquerda para acessar a página de gerenciamento.
3. Localize na lista a ACL de rede a ser modificada e clique em seu ID para acessar a página de detalhes.
4. Para adicionar uma regra de saída/entrada, clique em **Outbound Rules (Regras de saída)** ou **Inbound Rules (Regras de entrada)** -> **Edit (Editar)** -> **New Line (Nova linha)**, selecione o tipo de protocolo, insira a porta e o endereço IP de origem e selecione a política.
 - Protocol type (Tipo de protocolo): indica os tipos de protocolo que uma regra de ACL permite ou rejeita, por exemplo, TCP e UDP.
 - Port (Porta): indica a porta de origem do tráfego, que pode ser uma única porta ou um segmento de portas, por exemplo, porta 80 ou portas 90 a 100.
 - Source IP address (Endereço IP de origem): indica o endereço IP de origem ou intervalo de IP de tráfego que aceita o intervalo de IP ou bloco CIDR, por exemplo, `10.20.3.0` ou `10.0.0.2/24`.
 - Policy (Política): permite ou rejeita a solicitação de acesso.
![](https://main.qcloudimg.com/raw/d6d87cc117b15f5125d7f7fbb327f845.png)
5. Clique em **Save (Salvar)**.

## Exclusão de regras de ACL de rede
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** -> **Network ACL (ACL de rede)** no diretório à esquerda para acessar a página de gerenciamento.
3. Localize na lista a ACL de rede a ser excluída e clique em seu ID para acessar a página **Basic Information (Informações básicas)**.
4. Clique na guia **Inbound Rules (Regras de entrada)** ou na guia **Outbound Rules (Regras de saída)** para acessar a página **Rules List (Lista de regras)**.
5. Clique em **Edit (Editar)**. O processo de exclusão de regras de entrada é igual ao de exclusão de regras de saída. A exclusão de regras de entrada é usada conforme o exemplo aqui.
![](https://main.qcloudimg.com/raw/2d3a16b59a2566a2bfd6226086b3528b.png)
6. Na lista, selecione a linha da regra a ser excluída e clique em **Delete (Excluir)** na coluna de operação.
>? Esta regra de ACL ficará marcada em cinza. Se você a excluiu acidentalmente, clique em ***Recover the deleted rule (Recuperar a regra excluída)** na coluna de operação para restaurar a regra.
>
![](https://main.qcloudimg.com/raw/57389cf8420513b893c5f55747826247.png)
7. Clique em **Save (Salvar)** para salvar a operação anterior.
>! A exclusão ou restauração da regra de ACL só entrará em vigor depois que você salvar a operação.

## Associação de ACLs de rede a sub-redes
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** -> **Network ACL (ACL de rede)** no diretório à esquerda para acessar a página de gerenciamento.
3. Localize na lista a ACL de rede a ser associada e clique em seu ID para acessar a página de detalhes.
4. Na página **Basic Information (Informações básicas)**, clique em **Add Association (Adicionar associação)** no módulo **Associated Subnets (Sub-redes associadas)**.
![](https://main.qcloudimg.com/raw/60374f034ac84bc088b42f1b2811af93.png)
5. Selecione a sub-rede a ser associada na janela pop-up e clique em **OK**.
![2](https://main.qcloudimg.com/raw/dd1c974c4938aa5bfd13ebbba2fa3274.png)

## Desassociação de ACLs de rede de sub-redes
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** -> **Network ACL (ACL de rede)** no diretório à esquerda para acessar a página de gerenciamento.
3. Localize na lista a ACL de rede a ser desassociada e clique em seu ID para acessar a página de detalhes.
4. Existem diferentes métodos para desassociar ACLs de sub-redes:
 - Método 1: localize a sub-rede que deve ser desassociada no módulo **Associated Subnets (Sub-redes associadas)** na página **Basic Information (Informações básicas)** e clique em **Disassociate (Desassociar)**.
![1](https://main.qcloudimg.com/raw/f5049453bb9838e03e093461232e5c82.png)
 - Método 2: marque as sub-redes que devem ser desassociadas no módulo **Associated Subnets (Sub-redes associadas)** na página **Basic Information (Informações básicas)** e clique em **Batch Disassociate (Desassociar em lote)**.
![2](https://main.qcloudimg.com/raw/e2953af15a89f4476e033e08e67009e5.png)
5. Clique em **OK** na janela pop-up.
![3](https://main.qcloudimg.com/raw/e44731b65300f164200946b10b2d8be6.png)

## Exclusão de ACLs de rede
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** -> **Network ACL (ACL de rede)** no diretório à esquerda para acessar a página de gerenciamento.
3. Selecione a região e o VPC.
4. Na lista, localize a ACL de rede a ser excluída, clique em **Delete (Excluir)** e confirme a exclusão. A ACL de rede e todas as suas regras serão excluídas.
>? Se a opção **Delete (Excluir)** ficar marcada em cinza, como para a ACL de rede `testEg` na figura abaixo, isso indica que a ACL de rede está atualmente associada a uma sub-rede. Você precisará desassociá-la da sub-rede antes de excluí-la.

![](https://main.qcloudimg.com/raw/3d6113a44321ce73e35f99efc246bfb4.png)

