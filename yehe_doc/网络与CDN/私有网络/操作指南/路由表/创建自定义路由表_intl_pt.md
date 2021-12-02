Uma tabela de rotas é usada para controlar o tráfego de saída da sub-rede. Ela pode conter várias políticas de roteamento. Existem tabelas de rotas padrão e personalizadas. A tabela de rotas padrão (rota local) permite a interconexão da rede privada no VPC, que não pode ser excluída, mas pode ser configurada com políticas de roteamento da mesma forma que você configura uma tabela de rotas personalizada. Este documento descreve como criar e configurar uma tabela de rotas personalizada.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Route Tables (Tabelas de rotas)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Clique em **+ New (+ Novo)**.
4. Na caixa de diálogo pop-up, insira o nome da tabela de rotas, selecione o VPC ao qual ela pertence e configure as políticas de roteamento.
    ![](https://main.qcloudimg.com/raw/8d001c82ce2c4ada7fba9a723a2b4e0c.png)
    
	>? É possível configurar as políticas de roteamento ao criar uma tabela de rotas. Como alternativa, depois que uma tabela de rotas for criada, você poderá clicar na ID dela para acessar a página **Basic Information (Informações básicas)** e clicar em **+ New routing policies (+ Novas políticas de roteamento)**, para configurar as políticas de roteamento.
	>

	Configuração de uma política de roteamento [](id:routeParam):

<table><tbody>
<tr><th>Parâmetro</th><th>Descrição</th></tr>
<tr><td>Destino</td><td>O intervalo de IP de destino para o qual o tráfego será encaminhado. A configuração deve atender aos seguintes requisitos:
  <ul><li>Insira um intervalo de IP. Se você quiser inserir um único IP, defina a máscara para 32 (por exemplo, `172.16.1.1/32`).</li>
	<li>O destino não pode ser um intervalo de IP do VPC onde a tabela de rotas está localizada, porque a rota local já permite a interconexão de rede privada neste VPC.</li></ul>
	<p><b>Observação:</b> se você tiver implantado um <a href="https://intl.cloud.tencent.com/document/product/457/6759">serviço TKE</a> no VPC, o destino que você configurar na política da tabela de rotas da sub-rede do VPC não poderá estar dentro do bloco CIDR do VPC ou conter o intervalo de IP do TKE. Por exemplo, se o bloco CIDR do VPC for `172.168.0.0/16` e o bloco CIDR do TKE for `192.168.0.0/16`, o intervalo de IP de destino não deve estar dentro de `172.168.0.0/16`, ou conter `192.168.0.0/16`, quando você configurar a política de roteamento para uma sub-rede do VPC.</note></td></tr>
<tr><td>Next hop type (Tipo de próximo salto)</td><td>A saída dos pacotes de dados do VPC. Os seguintes tipos são compatíveis:
 <ul>
<li> NAT Gateway: o tráfego direcionado para um intervalo de IP de destino é encaminhado para um NAT Gateway.</li>
<li>Peering Connections: o tráfego direcionado para um intervalo de IP de destino é encaminhado para um VPC na outra extremidade de um Peering Connection.</li>
<li>Gateway do Direct Connect: o tráfego direcionado para um intervalo de IP de destino é encaminhado para um gateway do Direct Connect.</li>
<li>IP virtual de alta disponibilidade: o tráfego direcionado para um intervalo de IP de destino é encaminhado para um HAVIP.</li>
<li>VPN Gateway: o tráfego direcionado para um intervalo de IP de destino é encaminhado para um VPN Gateway.</li>
<li>IP público do CVM: o tráfego direcionado para um intervalo de IP de destino é encaminhado para o IP público (incluindo EIPs) de uma instância do CVM em um VPC.</li>
<li>CVM: o tráfego direcionado para um intervalo de IP de destino é encaminhado para uma instância do CVM em um VPC.</li>
</ul>
</td></tr>
<tr><td>Próximo salto</td><td>Especifica a instância do próximo salto para a qual o tráfego é redirecionado, como o gateway ou IP do CVM.</td></tr>
<tr><td>Observações</td><td>Descreve o propósito da rota para gerenciamento de recursos. Esse parâmetro é opcional.</td></tr>
<tr><td>Adicionar uma linha</td><td>Configura várias políticas de roteamento, se necessário. Você pode clicar no ícone de exclusão na coluna **Operation (Operação)** para excluir as políticas de roteamento desnecessárias. Uma tabela de rotas personalizada deve conter pelo menos uma política de roteamento.</td></tr>
</tbody> 
</table>

5. Ao concluir a configuração, clique em **Create (Criar)**. Em seguida, a tabela de rotas será exibida na lista.
![](https://main.qcloudimg.com/raw/c0e5611a3c21733e454ea0e7b8eb4430.png)

## Configuração do HAVIP
Atualmente, apenas as políticas de roteamento cujo **Next hop type (Tipo de próximo salto)** é **High Availability Virtual IP (IP virtual de alta disponibilidade)**, **VPN Gateway** ou **CVM** nas tabelas de rotas padrão ou personalizadas podem ser publicadas manualmente ou retiradas do CCN.
1. Clique na ID da tabela de rotas para acessar a página de detalhes.
    ![](https://main.qcloudimg.com/raw/7f74257af9225a09dbbf3d2f2366c779.png)
2. Você pode realizar as seguintes operações, conforme necessário:
    + Clique em **Publish to CCN (Publicar no CCN)** para publicar uma política de roteamento habilitada para o CCN.
    + Clique em **Withdraw from CCN (Retirar do CCN)** para retirar uma política de roteamento personalizada que foi publicada no CCN.
    + Clique em **Edit (Editar)** para modificar a política de roteamento.
    + Clique em **Delete (Excluir)** para excluir uma política de roteamento desativada.
