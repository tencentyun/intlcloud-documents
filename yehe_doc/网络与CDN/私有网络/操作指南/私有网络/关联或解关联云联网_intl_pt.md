O Cloud Connect Network (CCN) faz a ponte dos VPCs do Tencent Cloud e entre VPCs e IDCs locais. Ele fornece interconexão de rede privada multiponto. Para usar essa funcionalidade do CCN, primeiro é necessário adicionar VPCs a um CCN. Este documento descreve como associar um VPC ou desassociá-lo de um CCN.

## Associação ao CCN
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região do VPC na parte superior da página **VPC**.
3. Clique no ID do VPC para acessar a página **Basic Information (Informações básicas)**.
4. Clique em **Associate Now (Associar agora)** em **Associate with CCN (Associar ao CCN)** para abrir a caixa de diálogo.

5. Configure os parâmetros da seguinte forma.

	+ **Account (Conta)**: a conta do proprietário da instância do CCN. A instância do VPC e do CCN pode estar na mesma conta ou em contas diferentes. Se você escolher **Other accounts (Outras contas)**, insira o **Account ID (ID da conta)**. O proprietário da conta precisa aceitar o aplicativo do CCN dentro de 7 dias, caso contrário, o aplicativo vai expirar. O proprietário do CCN assume a tarifa de interconexão de rede gerada pelas instâncias que se conectam ao CCN.
	+ **CCN ID (ID do CCN)**: selecione um ID do CCN na lista suspensa para **My Account (Minha conta)** ou insira um ID do CCN para **Other accounts (Outras contas)**. 
6. Clique em **OK**. Em seguida, o status estará como **Connected (Conectado)** conforme mostrado abaixo.

		
## Desassociação do CCN
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região do VPC na parte superior da página **VPC**.
3. Localize o VPC para desassociar do CCN e clique no ID do VPC para acessar a página **Basic Information (Informações básicas)**.
4. Clique em **Disassociate (Desassociar)** na seção **Associate with CCN (Associar ao CCN)**.

5. Verifique e confirme os riscos da operação e clique em **Disassociate (Desassociar)**.


## Operações relevantes
[Interconexão de instância de rede em uma conta](https://intl.cloud.tencent.com/document/product/1003/31986)
[Interconexão de instância de rede entre contas](https://intl.cloud.tencent.com/document/product/1003/31987)
