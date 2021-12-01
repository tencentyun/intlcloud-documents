## Cenário
É possível vincular um ou vários grupos de segurança a uma instância do CVM. Se uma instância do CVM estiver vinculada a vários grupos de segurança, eles serão executados com base no nível de prioridade (como 1 e 2). É possível ajustar as prioridades dos grupos de segurança, conforme descrito abaixo.

## Pré-requisitos
A instância do CVM está associada a dois ou mais grupos de segurança.

## Instruções
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, clique no ID da instância do CVM para acessar a página de detalhes.
3. Selecione a guia **Security Groups (Grupos de segurança)** para acessar a pagina de gerenciamento de grupos de segurança.
4. Na seção "Bound Security Groups (Vincular grupos de segurança)" à direita, clique em **Order (Classificar)**. Selecione <img src="https://main.qcloudimg.com/raw/15a91d68b0396cb89bfd75a578b42130.png" style="margin:-3px 0px;width:20px"> à direita do grupo de segurança, e arraste para cima e para baixo para ajustar a prioridade dele. Quanto mais alta a posição, mais alto é o nível de prioridade.
5. Quando concluir o ajuste, clique em **Save (Salvar)**.

