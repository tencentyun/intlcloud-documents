### O que é a ENI?

A [Elastic Network Interface](https://intl.cloud.tencent.com/product/eni) (ENI) é uma interface de rede elástica vinculada a CVMs em um VPC, que pode ser migrado entre vários CVMs. A ENI é muito útil para configurar redes de gerenciamento e estabelecer soluções de rede altamente confiáveis.

A ENI tem atributos de VPC, zona de disponibilidade e sub-rede. Você só pode vinculá-lo a CVMs na mesma zona de disponibilidade. É possível vincular uma CVM a várias ENIs, e a quantidade máxima permitida varia de acordo com as especificações da CVM.

### Quais são as restrições para o uso de ENIs nos CVMs?

Para mais detalhes, consulte a seção de limites de uso em [Visão geral dos limites de uso](https://intl.cloud.tencent.com/document/product/213/15379).

### Quais são as informações básicas de uma ENI?

Consulte a seção **Conceitos** em [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/213/6514).

### Como faço para criar uma ENI?

Consulte [Criação de uma ENI](https://intl.cloud.tencent.com/document/product/576/18534).

### Como faço para exibir as informações da ENI?

Consulte [Exibição das informações da ENI](https://intl.cloud.tencent.com/document/product/576/18533).

### Como faço para vincular uma ENI a uma instância da CVM?

Consulte [Vinculação e configuração dos CVMs](http://intl.cloud.tencent.com/document/product/576/18535).

### Como faço para configurar uma ENI na instância da CVM?

Consulte [Vinculação e configuração dos CVMs](http://intl.cloud.tencent.com/document/product/576/18535).

### Como faço para modificar ou personalizar o IP privado de uma ENI?

Os CVMs no VPC permitem a modificação e a personalização do IP privado de uma ENI. Siga as etapas abaixo:

1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Na barra lateral esquerda, clique em **IP and Interface (IP e interface)** > **ENI** para acessar a página da lista de ENIs.
3. Clique no **ID/Name (ID/Nome)** de um ENI para acessar a página de detalhes e exibir as suas informações.
4. Selecione a guia **IPv4 address management (Gerenciamento de endereços IPv4)** e clique em **Assign Private IP (Atribuir IP privado)**.
5. Na janela pop-up, selecione o método de atribuição de IP como **Enter manually (Inserir manualmente)**, para inserir o endereço IP que deseja modificar.
6. Clique em **OK** para concluir a operação.

Após a modificação ser feita no console, você também precisa modificar o arquivo de configuração da ENI. Para mais informações, consulte [Vinculação e configuração dos CVMs](https://intl.cloud.tencent.com/document/product/576/18535).
