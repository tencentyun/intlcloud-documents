## Visão geral
Este documento descreve como criar um cluster do TcaplusDB no console.

## Pré-requisitos
Você [criou](https://intl.cloud.tencent.com/document/product/378/17985) uma conta do Tencent Cloud e completou a [verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629).

## Instruções
1. Faça login no [console do TencentDB for TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/app), selecione **Cluster List (Lista de clusters)** na barra lateral esquerda e clique em **Create Cluster (Criar cluster)**.
2. Na página de aquisição exibida, especifique as seguintes configurações e clique em **Buy Now (Comprar agora)**.
 - **Network (Rede)**: selecione um VPC e uma sub-rede. Você pode selecionar apenas um VPC e uma sub-rede ao criar um cluster, e esse não pode ser modificado após criado.
 - **Connection Protocol (Protocolo de conexão)**: selecione um protocolo de conexão (protocolo de descrição de dados).
 - **Cluster Name (Nome do cluster)**: defina o nome do cluster, que deve ser exclusivo na conta e pode conter de 1 a 32 caracteres. Você pode renomear o cluster a qualquer momento.
 - **Access Password (Senha de acesso)**: defina a senha de acesso ao cluster, que deve atender aos seguintes requisitos:
	 - 8 a 64 caracteres de comprimento. É recomendável uma senha de 12 ou mais caracteres.
	 - Não pode começar com uma barra (/).
	 - Deve conter pelo menos três tipos:
	  - Letras minúsculas (a-z)
	  - Letras maiúsculas (A-Z)
	  - Números (0-9)
	  - Símbolos especiais `\~!@#$%^&*_-+=\|(){}[]:;'<>,.?/`.
 - **Table Group Name (Nome do grupo de tabelas)** e **Table Group ID (ID do grupo de tabelas)**: crie um grupo de tabelas padrão para o cluster e nomeie-o. O ID do grupo de tabelas pode ser gerado automaticamente ou personalizado.
![](https://qcloudimg.tencent-cloud.cn/raw/eebfcf5a907d248b8352b54865ccf235.png)
3. Volte para a lista de clusters para verificar o cluster criado e o grupo de tabelas. Cada cluster receberá um ID exclusivo.
![](https://qcloudimg.tencent-cloud.cn/raw/0706ef01fd5983fdcfb7dcb67ab9e018.png)

