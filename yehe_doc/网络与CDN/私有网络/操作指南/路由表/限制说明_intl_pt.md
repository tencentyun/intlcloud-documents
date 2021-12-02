- A tabela de rotas padrão de um VPC não pode ser excluída. 
- Depois que um VPC for criado, sua tabela de rotas será fornecida automaticamente com uma rota padrão, indicando que todos os recursos neste VPC estão interconectados por meio da rede privada. Esta política de roteamento não pode ser modificada nem excluída.

<table>
<tbody>
<tr>
<th>Destino</th>
<th>Tipo de próximo salto</th>
<th>Próximo salto</th>
</tr>
<tr>
<td>Local</td>
<td>Local</td>
<td>Local</td>
</tr>
</tbody>
</table>

- Os protocolos de roteamento dinâmico, como BGP e OSPF, não são compatíveis.
- A compatibilidade com o ECMP varia com as rotas, conforme mostrado na tabela a seguir.

<table><tbody>
<tr><th>Tipo de próximo salto</th><th>Formação do ECMP com o mesmo tipo</th><th>Formação do ECMP com outro tipo</th><th>Máxima quantidade de ECMPs</th</tr>
<tr><td>NAT Gateway</td><td>Compatível</td><td>Não compatível</td><td>Mesmo tipo: até 8; tipos diferentes: 1</td></tr>
<tr><td>Peering Connection inter-região</td><td>Não compatível</td><td>Não compatível</td><td>N/A</td></tr>
<tr><td>Peering Connection entre regiões</td><td>Não compatível</td><td>Compatível, com o CCN</td><td>Tipos diferentes: 1</td></tr>
<tr><td>Gateway do Direct Connect</td><td>Não compatível</td><td>Compatível, com o CCN</td><td>Tipos diferentes: 1</td></tr>
<tr><td>HAVIP</td><td>Não compatível</td><td>Não compatível</td><td>N/A</td></tr>
<tr><td>VPN Gateway</td><td>Não compatível</td><td>Não compatível</td><td>N/A</td></tr>
<tr><td>CVM</td><td>Compatível</td><td>Não compatível</td><td>Mesmo tipo: até 8; tipos diferentes: 1</td></tr>
<tr><td>CCN</td><td>Não compatível</td><td>Compatível, com o gateway do Direct Connect ou Peering Connection entre regiões</td><td>Tipos diferentes: 1</td></tr>
</tbody> </table>

>?
>- O roteamento de vários caminhos de custo igual (ECMP) significa que há várias rotas de custo igual para um único destino.
>- Esse IP público do CVM tem prioridade maior que o do NAT Gateway ao rotear para o mesmo destino.
>- Devido às prioridades diferentes, o EIP e outros tipos de rotas não são considerados para o ECMP.
>- O gateway do Direct Connect e o CCN podem formar o ECMP. No entanto, ele não verificará o status de integridade da rota, ou excluirá automaticamente as rotas não íntegras. Para formar o ECMP com o CCN, primeiro [envie um tíquete](https://console.cloud.tencent.com/workorder/category).
>- Várias rotas do NAT Gateway podem formar o ECMP. No entanto, ele não verificará o status de integridade da rota, ou excluirá automaticamente as rotas não íntegras.
>- Várias rotas do CVM podem formar o ECMP. No entanto, ele não verificará o status de integridade da rota, ou excluirá automaticamente as rotas não íntegras.

- As rotas podem ser publicadas no CCN.
As seguintes rotas podem ser publicadas no CCN.

<table>
<tr>
<th>Tipo de próximo salto</th>
<th>Publicação no CCN por padrão</th>
<th>Publicar ou retirar manualmente</th>
<th>Descrição</th>
</tr>
<tr>
<td>Local</td>
<td>Compatível</td>
<td>Não compatível</td>
<td>Atribuído pelo sistema. O intervalo de IP do VPC conectado ao CCN será publicado automaticamente no CCN, incluindo os blocos CIDR principal e secundário (exceto para intervalos de IP do TKE).</td>
</tr>
<tr>
<td>VPN Gateway</td>
<td>Não compatível</td>
<td>Compatível</td>
<td>Uma rota personalizada para o VPN Gateway. Quando o intervalo de IP for todo 0 ou a política de roteamento estiver desabilitada, a rota não poderá ser publicada no CCN.</td>
</tr>
<tr>
<td>CVM</td>
<td>Não compatível</td>
<td>Compatível</td>
<td>Uma rota personalizada para o CVM. Quando o intervalo de IP for todo 0 ou a política de roteamento estiver desabilitada, a rota não poderá ser publicada no CCN.</td>
</tr>
<tr>
<td>HAVIP</td>
<td>Não compatível</td>
<td>Compatível</td>
<td>Rota personalizada para o HAVIP. Quando o intervalo de IP for todo 0 ou a política de roteamento estiver desabilitada, as rotas não poderão ser publicadas no CCN.</td>
</tr>
</table>

>?
> - Uma rota personalizada desabilitada não pode ser publicada no CCN.
> - Uma rota personalizada deve ser retirada primeiro antes de poder ser desabilitada, se tiver sido publicada em um CCN.

### Limites de cota

<table>
<tr>
<th>Recurso</th>
<th>Limite</th>
</tr>
<tr>
<td>Quantidade de tabelas de rotas por VPC</td>
<td>10</td>
</tr>
<tr>
<td>Quantidade de tabelas de rotas associadas a cada sub-rede</td>
<td>1</td>
</tr>
<tr>
<td>Quantidade de políticas de roteamento por tabela de rotas</td>
<td>50</td>
</tr>
</table>
