## Cenário de operação

O grupo de segurança é um firewall virtual para filtrar pacotes e é usado para definir os controles de acesso à rede para um ou vários CVMs. É um método importante de isolamento de segurança de rede fornecido pelo Tencent Cloud. Ao criar uma instância do CVM, você deve configurar um grupo de segurança para ela. O Tencent Cloud permite que você configure um novo grupo de segurança para a instância do CVM após sua criação.
> Para configurar um novo grupo de segurança para a instância, crie primeiro um grupo de segurança. Para obter mais informações, consulte [Criação de um grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34271).

## Pré-requisitos

Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).

## Direções

### Alterar o grupo de segurança configurado

Para melhorar sua experiência no console do CVM, o grupo de segurança pode ser configurado na página de gerenciamento da instância ou na página de detalhes da instância.

#### Configuração de um grupo de segurança na página de gerenciamento da instância

1. Selecione um CVM a ser reatribuído a um novo grupo de segurança na página de gerenciamento da instância e clique em **More (Mais)** > **Security Groups (Grupos de segurança)** > **Configure Security Groups (Configurar grupos de segurança)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/68a30faac347446e57d87e8a1c30ef11.png)
2. Na janela pop-up “Configure Security Group (Configurar grupo de segurança)”, marque o nome do novo grupo de segurança (vários nomes podem ser selecionados) e clique em **Confirm (Confirmar)** para alterar o grupo de segurança.
 
#### Configuração de um grupo de segurança na página de detalhes da instância
 
1. Na página de gerenciamento da instância, clique no ID/nome da instância do CVM para o qual deseja alterar o grupo de segurança e entre na página de detalhes da instância.
2. Clique em **More Actions (Mais ações)** > **Security Groups (Grupos de segurança)** > **Configure Security Groups (Configurar grupos de segurança)** no canto superior direito da página de detalhes da instância, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/c7a1d76159feaa66f52eb16c7787432d.png)
3. Na janela pop-up “Configure Security Group (Configurar grupo de segurança)”, marque o nome do novo grupo de segurança (vários nomes podem ser selecionados) e clique em **Confirm (Confirmar)**.

### Alterar o grupo de segurança vinculado

1. Na página de gerenciamento da instância, clique no ID/nome da instância do CVM para o qual deseja vincular o grupo de segurança e entre na página de detalhes da instância.
2. Na página de detalhes da instância, selecione a guia **Security Groups (Grupos de segurança)** e clique em **Bind (Vincular)** na coluna “Bound to security group (Vincular a grupo de segurança)”, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/2ea553a1f2f589c6202245addfd62523.png)
3. Na janela pop-up “Security Groups (Grupos de segurança)”, marque o nome do grupo de segurança (vários nomes podem ser selecionados) a ser vinculado com base em suas necessidades reais e clique em **OK** para vincular o grupo de segurança.
![](https://main.qcloudimg.com/raw/ac58322e8b11db8497d79eb54ecc67f6.png)
