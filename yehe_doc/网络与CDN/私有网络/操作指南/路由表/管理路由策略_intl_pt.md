As políticas de roteamento na tabela de rotas podem ser operadas em tempo real. Algumas das ações disponíveis de política de roteamento são adicionar, excluir, consultar, exportar ou publicar no CCN e retirar dele. Este documento descreve todas as operações acima mencionadas das políticas de roteamento.

## Adição de uma política de roteamento
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e selecione **[Route Tables (Tabelas de rotas)](https://console.cloud.tencent.com/vpc/route?rid=1)** na barra lateral esquerda para acessar a página **Route Table (Tabela de rotas)**.
2. Na lista, clique no ID da tabela de rotas a ser modificado para acessar a página de detalhes.
3. Clique em **+New routing policies (+Novas políticas de roteamento)**.
4. Na janela pop-up, <span id="routeParam" />configure a política de roteamento.
 >? Se você implantou um <a href="https://int/product/457/6759">serviço TKE</a> no VPC, ao configurar a política de roteamento da tabela de rotas para a sub-rede do VPC, o destino não pode estar dentro do intervalo dos blocos CIDR do VPC, nem conter o intervalo de IP do contêiner. Por exemplo, se um bloco CIDR do VPC for 172.168.0.0/16 e o bloco CIDR da rede do contêiner for 192.168.0.0/16, quando você configurar a política de roteamento para a sub-rede do VPC, o intervalo de IP de destino não pode estar no intervalo de 172.168.0.0/16, e não pode conter 192.168.0.0/16.
 >
  <table><tbody>
   <tr><th>Item de configuração</th><th>Descrição</th></tr>
   <tr><td>Destination (Destino)</td><td>O intervalo de IP de destino para o qual você deseja encaminhar o tráfego de saída da sub-rede. Os requisitos são os seguintes:
    <ul><li>O intervalo de IP de destino só pode estar no formato do intervalo de IP. Se você deseja que o destino seja um único IP, defina a máscara para 32 (por exemplo, 172.16.1.1/32).</li>
	  <li>O destino não pode ser um intervalo de IP no VPC em que a tabela de roteamento está localizada, porque o roteamento local indicou que a rede privada está conectada neste VPC por padrão.</li></ul>
    	</td></tr>
    <tr><td>Next hop type (Tipo de próximo salto)</td><td>A saída dos pacotes de dados do VPC. Os seguintes tipos são compatíveis:
        <ul>
           <li> NAT Gateway: o tráfego designado para um intervalo de IP de destino é encaminhado para um NAT Gateway.</li>
           <li>Peering Connections: o tráfego designado para um intervalo de IP de destino é encaminhado para um VPC na outra extremidade de um Peering Connection.</li>
           <li>Gateway do Direct Connect: o tráfego designado para um intervalo de IP de destino é encaminhado para um gateway do Direct Connect.</li>
          <li>IP virtual de alta disponibilidade: o tráfego designado para um intervalo de IP de destino é encaminhado para um IP virtual de alta disponibilidade.</li>
          <li>VPN Gateway: o tráfego designado para um intervalo de IP de destino é encaminhado para um VPN Gateway.</li>
          <li>IP público do CVM: o tráfego designado para um intervalo de IP de destino é encaminhado ao IP público de uma instância do CVM em um VPC (incluindo IPs públicos e elásticos).</li>
          <li>CVM: o tráfego designado para um intervalo de IP de destino é encaminhado para uma instância do CVM em um VPC.</li>
          </ul>
       </td></tr>
   <tr><td>Next hop (Próximo salto)</td><td>Especifique a instância do próximo salto para a qual redirecionar, como o gateway ou IP do CVM.</td></tr>
    <tr><td>Notes (Observações)</td><td>Você pode personalizar a descrição da rota para gerenciamento de recursos.</td></tr>
    <tr><td>Add a line (Adicionar uma linha)</td><td>Você pode clicar em <b>+Add a line (+Adicionar uma linha)</b>, para configurar várias políticas de roteamento, ou clicar no ícone de exclusão na coluna <b>Operation (Operação)</b>, para excluir as políticas de roteamento desnecessárias.</td></tr>
     </tbody> </table>
5. Clique em **Create (Criar)** para concluir a criação.

## Publicação de uma política de roteamento para o CCN/Retirada de uma política de roteamento do CCN
Para as instâncias do VPC ou do VPN associadas ao CCN, as rotas são publicadas no CCN por padrão. Para as novas políticas de roteamento personalizadas que não são publicadas no CCN por padrão, é necessário publicá-las manualmente. As políticas de roteamento que são publicadas manualmente ou publicadas por padrão podem ser retiradas do CCN.
Atualmente, apenas as políticas de roteamento cujo **Next hop type (Tipo de próximo salto)** é **High Availability Virtual IP (IP virtual de alta disponibilidade)**, **VPN Gateway** ou **CVM** nas tabelas de rotas (incluindo as tabelas de rotas padrão e personalizadas) podem ser publicadas manualmente no CCN/retiradas do CCN.

### Pré-requisitos
Os VPCs nos quais o IP virtual de alta disponibilidade, o VPN Gateway e o CVM estão localizados foram associados ao CCN.

### Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e selecione **[Route Tables (Tabelas de rotas)](https://console.cloud.tencent.com/vpc/route?rid=1)** na barra lateral esquerda para acessar a página **Route Table (Tabela de rotas)**.
2. Na lista, clique no ID da tabela de rotas a ser modificado para acessar a página de detalhes.
   ![](https://main.qcloudimg.com/raw/351e5dec96293642293015fcebdc3ba5.png)
3. Você pode realizar as seguintes operações, conforme necessário:
   + Para a política de roteamento personalizada, você pode clicar em **Publish to CCN (Publicar no CCN)** para publicar manualmente esta política de roteamento no CCN.
   + Para a política de roteamento personalizada que foi publicada no CCN, você pode clicar em **Withdrawn from CCN (Retirar do CCN)** para reivindicar a política.
   + Clique em **Edit (Editar)** para modificar a política de roteamento.
 >?
 >+ Quando uma política de roteamento é desabilitada, ela não pode ser publicada no CCN.
 >+ Uma política de roteamento não pode ser desabilitada depois de publicada no CCN.

## Edição de uma política de roteamento
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e selecione **[Route Tables (Tabelas de rotas)](https://console.cloud.tencent.com/vpc/route?rid=1)** na barra lateral esquerda para acessar a página **Route Table (Tabela de rotas)**.
2. Na lista, clique na ID da tabela de rotas para acessar a página de detalhes.
3. Clique em **Edit (Editar)** à direita da política de roteamento para modificá-la.
![](https://main.qcloudimg.com/raw/6f817db7223a5f5f2ae146fc6a39d28b.png)
4. Clique em **OK** para concluir a modificação ou clique em **Cancel (Cancelar)** para cancelar a modificação.

## Consulta e exportação de uma política de roteamento
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e selecione **[Route Tables (Tabelas de rotas)](https://console.cloud.tencent.com/vpc/route?rid=1)** na barra lateral esquerda para acessar a página **Route Table (Tabela de rotas)**.
2. Na lista, clique em um ID da tabela de rotas para acessar a página de detalhes. É possível encontrar as políticas de roteamento nesta tabela de rotas.
3. Na caixa de pesquisa no canto superior direito, é possível consultar a política de roteamento digitando o endereço de destino.
![](https://main.qcloudimg.com/raw/0fb54a38484b8525e5cdd9fdc904a183.png)
4. Clique em **Export (Exportar)** para exportar as políticas de roteamento na lista, e salve no formato .csv.

## Exclusão de uma política de roteamento
É possível excluir as políticas de roteamento desnecessárias. Apenas as políticas de roteamento personalizadas podem ser excluídas.
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e selecione **[Route Tables (Tabelas de rotas)](https://console.cloud.tencent.com/vpc/route?rid=1)** na barra lateral esquerda para acessar a página **Route Table (Tabela de rotas)**.
2. Na lista, clique no ID da tabela de rotas a ser modificado para acessar a página de detalhes.
3. Clique em **Delete (Excluir)** à direita da política de roteamento que deseja excluir.
![](https://main.qcloudimg.com/raw/9ab1d9bcca75ba9f4cfdd4abfbddd58e.png)
4. Certifique-se de estar ciente dos possíveis impactos da exclusão da política de roteamento e clique em **OK**.
