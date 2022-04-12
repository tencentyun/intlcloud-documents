- Não é possível excluir a tabela de rotas padrão de uma VPC. 
- Após criar uma VPC, sua tabela de rotas será fornecida automaticamente com uma rota padrão, indicando que todos os recursos nessa VPC estão interconectados por meio da rede privada. Não é possível modificar nem excluir essa política de roteamento.
<table>
<tbody>
<tr>
<th>Destino</th>
<th>Tipo do próximo salto</th>
<th>Próximo salto</th>
</tr>
<tr>
<td>Local</td>
<td>Local</td>
<td>Local</td>
</tr>
</tbody>
</table>

- Os protocolos de roteamento dinâmico, como o BGP e o OSPF, não são aceitos.
- As rotas podem ser publicadas no CCN. As seguintes rotas podem ser publicadas no CCN.
<table>
<tr>
<th>Tipo do próximo salto</th>
<th>Publicação no CCN por padrão</th>
<th>Publicar ou retirar manualmente</th>
<th>Descrição</th>
</tr>
<tr>
<td>Local</td>
<td>Compatível</td>
<td>Não compatível</td>
<td>Atribuído pelo sistema. O intervalo de IP da VPC conectada ao CCN será publicado automaticamente no CCN, incluindo os blocos CIDR principal e secundário (exceto para intervalos de IP do TKE).</td>
</tr>
<tr>

<td>CVM</td>
<td>Não compatível</td>
<td>Compatível</td>
<td>Uma rota personalizada para a CVM. Quando o intervalo de IP for todo 0 ou a política de roteamento estiver desativada, a rota não poderá ser publicada no CCN.</td>
</tr>
<tr>
<td>HAVIP</td>
<td>Não compatível</td>
<td>Compatível</td>
<td>Rota personalizada para o HAVIP. Quando o intervalo de IP for todo 0 ou a política de roteamento estiver desativada, as rotas não poderão ser publicadas no CCN.</td>
</tr>
</table>

>?
> - Uma rota personalizada desativada não pode ser publicada no CCN.
> - Primeiro, uma rota personalizada deve ser retirada antes de poder ser desativada, se tiver sido publicada em um CCN.

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
