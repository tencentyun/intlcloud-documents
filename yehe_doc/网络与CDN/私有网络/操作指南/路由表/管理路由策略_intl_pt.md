
Este documento descreve as operações relacionadas com as políticas de roteamento.

## Adição de uma política de roteamento
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e acesse a página **Route Table (Tabela de rotas)**.
2. Clique no **ID/Name (ID/Nome)** da tabela de rotas a ser modificada para acessar sua página de detalhes.
3. Clique em **+New routing policies (+Novas políticas de roteamento)**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/38e0ec6462b9305afc0d3f7f0897fcde.png" width="80%">
4. Na janela pop-up, <span id="routeParam" />configure a política de roteamento.
>? Se você implantou um [serviço TKE](https://intl.cloud.tencent.com/document/product/457/6759) na VPC, o destino que você configura na política de roteamento da sub-rede da VPC não pode se sobrepor ao bloco CIDR da VPC ou ao intervalo de IP do TKE. Por exemplo, se o bloco CIDR da VPC for `172.168.0.0/16` e o bloco CIDR do TKE for `192.168.0.0/16`, o intervalo de IP de destino não pode estar dentro de `172.168.0.0/16` nem conter `192.168.0.0/16`.
>

<table><tbody>
<tr><th>Item de configuração</th><th>Descrição</th></tr>
<tr><td>Destination (Destino)</td><td>Especifica o intervalo de IP de destino para o qual você deseja encaminhar o tráfego de saída da sub-rede. Os requisitos para um destino são os seguintes:
<ul><li>Insira um intervalo de IP. Se você quiser inserir um único IP, defina a máscara para `32` (por exemplo, `172.16.1.1/32`).</li>
<li>O destino não pode ser um intervalo de IP da VPC onde reside a tabela de rotas, pois a rota local já permite interconexão de rede privada neste VPC.</li></ul>
	</td></tr>
<tr><td>Next hop type (Tipo do próximo salto)</td><td>Indica a saída de pacotes de dados para a VPC. Tipos aceitos:
  <ul>
     <li> NAT Gateway: o tráfego direcionado para um intervalo de IP de destino é encaminhado para um NAT Gateway.</li>
     <li>Peering Connections: o tráfego direcionado para um intervalo de IP de destino é encaminhado para o par da VPC de um Peering Connection.</li>
     <li>Direct Connect Gateway (Gateway do Direct Connect): o tráfego direcionado para um intervalo de IP de destino é encaminhado para um gateway do Direct Connect.</li>
    <li>High Availability Virtual IP (IP virtual de alta disponibilidade): o tráfego direcionado para um intervalo de IP de destino é encaminhado para um HAVIP.</li>
    <li>VPN Gateway (Gateway do VPN): o tráfego direcionado para um intervalo de IP de destino é encaminhado para um gateway do VPN.</li>
    <li>Public IP of CVM (IP público da CVM): o tráfego direcionado para um intervalo de IP de destino é encaminhado para o IP público (incluindo EIPs) de uma instância da CVM na VPC.</li>
    <li>CVM: o tráfego direcionado para um intervalo de IP de destino é encaminhado para uma instância da CVM na VPC.</li>
    </ul>
 </td></tr>
<tr><td>Next hop (Próximo salto)</td><td>Especifica a instância do próximo salto para a qual o tráfego é redirecionado, como o gateway ou o IP da CVM.</td></tr>
<tr><td>Notes (Observações)</td><td>(Opcional) Você pode inserir a descrição da rota para gerenciamento de recursos.</td></tr>
<tr><td>Add a line (Adicionar uma linha)</td><td>Você pode clicar em <b>+Add a line (+Adicionar uma linha)</b> para configurar várias políticas de roteamento ou clicar no ícone de exclusão na coluna <b>Operation (Operação)</b> para excluir as políticas de roteamento desnecessárias.</td></tr>
</tbody> </table>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/5d4e0dcde1c1a257298ea7fbdf15270a.png">

5. Clique em **Create (Criar)**.

## Edição de uma política de roteamento
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e acesse a página **Route Table (Tabela de rotas)**.
2. Na lista, clique no **ID/Name (ID/Nome)** da tabela de rotas em questão para acessar sua página de detalhes.
3. Clique em **Edit (Editar)** na coluna **Operation (Operação)** da política de roteamento para modificá-la.
![](https://main.qcloudimg.com/raw/6f817db7223a5f5f2ae146fc6a39d28b.png)
4. Após a modificação, clique em **OK** para salvar ou em **Cancel (Cancelar)** para descartar a modificação.

## Publicação/Retirada de uma política de roteamento do/para o CCN
As rotas de uma VPC associada a um CCN são publicadas no CCN por padrão. Para as novas políticas de roteamento personalizadas que não são publicadas, você precisa publicá-las manualmente. Você também pode retirar uma política de roteamento do CCN.
Atualmente, apenas as políticas de roteamento cujo **Next hop type (Tipo de próximo salto)** é **High Availability Virtual IP (IP virtual de alta disponibilidade)** ou **CVM** nas tabelas de rotas padrão ou personalizadas podem ser publicadas manualmente ou retiradas do CCN.

### Pré-requisitos
A VPC onde reside o HAVIP ou CVM está associada a uma instância do CCN.

### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e acesse a página **Route Table (Tabela de rotas)**.
2. Clique no **ID/Name (ID/Nome)** da tabela de rotas a ser modificada para acessar sua página de detalhes.
3. Execute as seguintes operações conforme necessário:
   + Clique em **Publish to CCN (Publicar no CCN)** para publicar manualmente uma política de roteamento personalizada no CCN.
   + Clique em **Withdraw from CCN (Retirar do CCN)** para retirar uma política de roteamento personalizada que foi publicada no CCN.
>!
>+ Uma política de roteamento desativada não pode ser publicada no CCN.
>+ Uma política de roteamento não pode ser desativada depois de publicada no CCN.


## Consulta e exportação de uma política de roteamento
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e acesse a página **Route Table (Tabela de rotas)**.
2. Clique no **ID/Name (ID/Nome)** da tabela de rotas em questão para acessar sua página de detalhes. Nessa página, você pode exibir as políticas de roteamento nesta tabela de rotas.
3. Na caixa de pesquisa superior direita, consulte as políticas de roteamento inserindo um endereço de destino.
![](https://qcloudimg.tencent-cloud.cn/raw/9be2e0939c90f89622a8e799e4b11ce6.png)
4. Clique em **Export (Exportar)** para salvar o resultado da pesquisa no formato .csv.

## Ativação/Desativação de uma política de roteamento
Uma política de roteamento personalizada pode ser ativada ou desativada.
### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc/route?rid=4) e acesse a página **Route Table (Tabela de rotas)**.
2. Clique no **ID/Name (ID/Nome)** da tabela de rotas em questão para acessar sua página de detalhes. Verifique o status da política de roteamento:
  + <img src="https://main.qcloudimg.com/raw/a142df25497e2ad5828a231dc17f5130.png" width="3%" />: ativada
 + <img src="https://main.qcloudimg.com/raw/7c04cc17a33bd833f66627628aba31b7.png" width="3%" />: desativada
3. Para desativar uma política de roteamento: clique no ícone <img src="https://main.qcloudimg.com/raw/a142df25497e2ad5828a231dc17f5130.png" width="3%" /> ao lado de uma política de roteamento para desativá-la.
>!Desativar uma rota pode resultar na interrupção dos negócios. Confirme antes de continuar.
>
   <img src="https://qcloudimg.tencent-cloud.cn/raw/278ad06cfcdad1de0eb0aabd9b08bab8.png" width="50%" />
4. Para ativar uma política de roteamento: clique no ícone <img src="https://main.qcloudimg.com/raw/7c04cc17a33bd833f66627628aba31b7.png" width="3%" /> ao lado de uma política de roteamento para ativá-la.
>! Quando ativada, será utilizada a rota com a máscara mais longa. Isso pode afetar seus negócios atuais. Confirme antes de continuar.
>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/c0fca3b5ddb0c6ba7e61e07470cd604a.png" width="50%" />
5. Para ativar ou desativar várias políticas de roteamento: selecione as políticas de roteamento em questão e clique em **Enable (Ativar)** ou **Disable (Desativar)** acima da lista.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1ea2f28cc53ed463f26edf7fdfd93640.png)

## Exclusão de uma política de roteamento
Você pode excluir as políticas de roteamento não utilizadas. Só é possível excluir as políticas de roteamento personalizadas.
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc/route?rid=1) e acesse a página **Route Table (Tabela de rotas)**.
2. Clique no **ID/Name (ID/Nome)** da tabela de rotas a ser modificada para acessar sua página de detalhes.
3. Selecione a política de roteamento a ser excluída e clique em **Delete (Excluir)** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/9ab1d9bcca75ba9f4cfdd4abfbddd58e.png)
4. Leia as observações e clique em **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/57035cab86a2e31d78477792548a7640.png" width="70%" />

