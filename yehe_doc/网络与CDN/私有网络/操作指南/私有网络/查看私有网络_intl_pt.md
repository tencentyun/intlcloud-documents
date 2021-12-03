É possível consultar todos os recursos do VPC por meio do console do VPC, como os recursos de nuvem e as conexões em um VPC.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região do VPC na parte superior da página **VPC**. É possível verificar as informações de todos os VPC nesta região na lista.

<table>
<tr>
<th width="15%">Coluna</th>
<th width="85%">Descrição</th>
</tr>
<tr>
<td>ID/Name (ID/Nome)</td>
<td>O ID e o nome do VPC. O nome pode ser modificado.</td>
</tr>
<tr>
<td>IPv4 CIDR Block (Bloco CIDR IPv4)</td>
<td>O bloco CIDR IPv4 do VPC. Ele não pode ser modificado.</td>
</tr>
<tr>
<td>IPv6 CIDR Block (Bloco CIDR IPv6)</td>
<td>O bloco CIDR IPv6 do VPC. Atualmente, essa funcionalidade está em beta. Para usá-la, <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1">envie um tíquete</a>.</td>
</tr>
<tr>
<td>Subnet (Sub-rede)</td>
<td>O número das sub-redes no VPC. Clique no número para acessar a página <b>Sub-rede</b>.</td>
</tr>
<tr>
<td>Tabela de rotas</td>
<td>O número das tabelas de rotas no VPC. Clique no número para acessar a página <b>Tabela de rotas</b>.</td>
</tr>
<tr>
<td>NAT Gateway</td>
<td>O número dos NAT Gateways no VPC. Clique no número para acessar a página <b>NAT Gateway</b>.</td>
</tr>
<tr>
<td>VPN Gateway</td>
<td>O número dos VPN Gateways no VPC. Clique no número para acessar a página <b>VPN Gateway</b>.</td>
</tr>
<tr>
<td>CVM</td>
<td>O número dos CVMs no VPC. Clique no número para acessar a página do CVM. Clique no ícone do CVM para redirecionar para a página de aquisição do CVM.</td>
</tr>
<tr>
<td>Classiclink</td>
<td>O número das instâncias do CVM baseadas na rede clássica associadas a este VPC. Um CVM baseado na rede clássica só pode ser associado a um VPC.</td>
</tr>
<tr>
<td>Gateway do Direct Connect</td>
<td>O número dos gateways do Direct Connect no VPC. Clique no número para acessar a página Gateway do Direct Connect.</td>
</tr>
<tr>
<td>VPC padrão</td>
<td>Indica se o VPC é o VPC padrão da região. Só pode haver um VPC padrão em uma região. O VPC padrão é criado automaticamente quando você adquire recursos como o CVM. Ele funciona da mesma forma que os criados manualmente.</td>
</tr>
<tr>
<td>Hora de criação</td>
<td>A hora em que o VPC foi criado.</td>
</tr>
<tr>
<td>Operação</td>
<td>As operações compatíveis do VPC. Apenas um VPC sem nenhum recurso pode ser excluído. Você pode clicar em <b>More (Mais)</b> para editar o bloco CIDR IPv4 e o bloco CIDR IPv6, se aplicável.</td>
</tr>
</table>

3. Clique no ID do VPC para exibir os detalhes, incluindo as informações básicas, a associação do CCN e os recursos associados. Clique no número ao lado de um recurso para acessar a página de gerenciamento do recurso.

4. Retorne à lista do VPC e clique na caixa de pesquisa do canto superior direito para filtrar o VPC por diferentes atributos de recursos.

5. Clique no ícone de configuração no canto superior direito para personalizar as colunas de exibição.
