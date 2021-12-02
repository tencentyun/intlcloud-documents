Semelhante a um IP privado, a vinculação do HAVIP também pode ser configurada no console. Vincular um HAVIP refere-se a operações de EIP. Você pode pular esta seção se nenhuma conexão de rede pública for necessária.

## Vinculação de um EIP
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/) e selecione **IP and Interface (IP e interface)** > **HAVIP** na barra lateral esquerda. 
2. Selecione a região em questão na página de gerenciamento do HAVIP.
3. Selecione o HAVIP a ser vinculado ao EIP e clique em **Bind (Vincular)** na coluna **Operation (Operação)**.
4. Na caixa de diálogo pop-up, selecione um EIP a ser vinculado.
    >!
    >+ Um HAVIP só pode ser vinculado a um EIP. Se nenhum EIP estiver disponível, primeiro você deve criar um EIP no console.
    >+ Se o HAVIP não estiver vinculado a uma instância do CVM, o EIP correspondente ficará inativo e incorrerá em uma taxa de inatividade. Configure o HAVIP corretamente e vincule-o a uma instância, referindo-se aos seguintes casos: 
    >  + [Criação de cluster principal/secundário de alta disponibilidade usando HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) em Práticas recomendadas
    >  + [Criação de um banco de dados de alta disponibilidade usando HAVIP + cluster de failover do Windows Server](https://intl.cloud.tencent.com/document/product/215/31878) em Práticas recomendadas 
5. Clique em **OK**.

## Desvinculação de um EIP
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/) e selecione **IP and Interface (IP e interface)** > **HAVIP** na barra lateral esquerda. 
2. Selecione a região em questão na página de gerenciamento do HAVIP.
3. Selecione o HAVIP do qual o EIP será desvinculado e clique em **Unbind (Desvincular)** na coluna **Operation (Operação)**.
4. No pop-up, leia as observações e clique em **OK** para desvincular o EIP.
   >!
   >+ Seu negócio de rede pública pode ser afetado após a desvinculação do EIP. Prepare-se com antecedência.
   >+ Depois de ser desvinculado, o EIP ficará inativo e incorrerá em uma taxa de inatividade. Você pode liberar os EIPs não utilizados diretamente para evitar custos.
   >
