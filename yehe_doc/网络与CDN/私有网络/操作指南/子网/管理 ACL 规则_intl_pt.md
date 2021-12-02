A [Regra de ACL](https://intl.cloud.tencent.com/document/product/215/31850) é uma camada de segurança opcional que opera no nível das sub-redes. Ela é usada para controlar os fluxos de dados de entrada e saída das sub-redes, que podem ser conforme o protocolo e a granularidade da porta, para obter um controle preciso do tráfego das sub-redes. É possível associar a mesma ACL de rede a sub-redes que requerem o mesmo nível de controle de tráfego de rede.
Esta seção descreve como vincular, desvincular e alterar as regras de ACL por meio do console do VPC.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Subnet (Sub-rede)** na barra lateral esquerda para acessar a página de gerenciamento de sub-rede.
3. Clique em um ID de sub-rede para acessar a sua página de detalhes. É possível realizar a vinculação, a desvinculação ou a alteração da ACL nas seguintes páginas.
    + No campo **Associate ACL (Associar ACL)** na guia **Basic Information (Informações básicas)**
    + Na guia **ACL Rules (Regras de ACL)**
4. Execute as seguintes operações com base nas necessidades empresariais. As capturas de tela a seguir consideram as operações em **ACL Rules (Regras de ACL)** como exemplo.
  + Se a sub-rede atual não estiver vinculada à regra de ACL, você pode clicar em **Bind (Vincular)** para selecionar uma regra de ACL apropriada e clicar em **OK** para concluir a vinculação. A vinculação entrará em vigor imediatamente. No momento, apenas o tráfego de entrada e saída da sub-rede a qual a regra é **Allow (Permitir)** pode avançar.
 + Se a regra de ACL vinculada à sub-rede atual não atender aos requisitos de fluxo de rede, clique em **Change (Alterar)** para alterar a regra de ACL, que entrará em vigor imediatamente.
 + Se a sub-rede atual estiver vinculada a uma regra de ACL, mas você não precisar mais controlar o tráfego de entrada e saída da sub-rede, clique em **Unbind (Desvincular)** para desvincular a regra de ACL. A desvinculação será feita de imediato e isso causará o levantamento da restrição da regra de ACL no tráfego de entrada e saída da sub-rede.
    	 
