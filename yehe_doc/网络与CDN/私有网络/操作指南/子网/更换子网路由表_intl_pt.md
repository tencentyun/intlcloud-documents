Cada sub-rede deve ser associada a uma [tabela de rotas](https://intl.cloud.tencent.com/document/product/215/31810), que é usada para controlar a direção do tráfego de saída da sub-rede. Você pode alterar a tabela de rotas associada da sub-rede na página **VPC -> Subnet (Sub-rede)** de acordo com as necessidades de roteamento da sub-rede. Se você precisar criar uma tabela de rotas, consulte [Criação de uma tabela de rotas personalizada](https://intl.cloud.tencent.com/document/product/215/35236).

## Impacto nos sistemas
Considerando que a tabela de rotas impacta diretamente o fluxo de tráfego na sub-rede, quaisquer alterações como a associação da tabela de rotas ou as entradas de rotas devem ser cuidadosamente consideradas de acordo com as necessidades empresariais dos fluxos de rede.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Subnet (Sub-rede)** na barra lateral esquerda para acessar a página de gerenciamento de sub-rede.
3. O sistema fornece dois métodos para alterar a tabela de rotas associada à sub-rede.
    + Clique em **More (Mais)** > **Change Route Table (Alterar tabela de rotas)** na coluna **Operation (Operação)** no lado direito da sub-rede que precisa alterar a tabela de rotas.
       ![](https://main.qcloudimg.com/raw/154c5a6ff6b746a1a593fc4ac6a5ece9.png)
	+ Clique no ID da sub-rede que precisa alterar a tabela de rotas para acessar a página de detalhes, mude para a guia **Routing Rules (Regras de roteamento)** e clique em **Change Route Table (Alterar a tabela de rotas)**.
	   ![](https://main.qcloudimg.com/raw/572762da3d2163b3c30ed07c8a167130.png)
4. Na janela pop-up, selecione uma nova tabela de rotas na lista suspensa, confirme o impacto na sua empresa e clique em **Confirm (Confirmar)**.
![](https://main.qcloudimg.com/raw/c51606ba642517ffc01bcbf666abab49.png)
