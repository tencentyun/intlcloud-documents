### VPCs e sub-redes
<table>
<thead>
<tr>
<th width="70%">Recurso</th>
<th width="30%">Limite de cota</th>
</tr>
</thead>
<tbody><tr>
<td>Quantidade de VPCs por conta por região</td>
<td align="center">20</td>
</tr>
<tr>
<td>Quantidade de sub-redes por VPC</td>
<td align="center">100</td>
</tr>
<tr>
<td>Quantidade de blocos CIDR secundários por VPC</td>
<td align="center">5</td>
</tr>
<tr>
<td>Quantidade de instâncias da CVM da rede clássica associadas a cada VPC</td>
<td align="center">100</td>
</tr>
</tbody></table>

### Tabelas de rotas
<table>
<thead>
<tr>
<th width="70%">Recurso</th>
<th width="30%">Limite de cota</th>
</tr>
</thead>
<tbody><tr>
<td>Quantidade de tabelas de rotas por VPC</td>
<td align="center">10</td>
</tr>
<tr>
<td>Quantidade de tabelas de rotas associadas a cada sub-rede</td>
<td align="center">1</td>
</tr>
<tr>
<td>Quantidade de políticas de roteamento por tabela de rotas</td>
<td align="center">50</td>
</tr>
</tbody></table>

### ENIs
<table>
<tr>
<th width="70%">Recurso</th>
<th width="30%">Limite de cota</th>
</tr>
<tr>
<td>Quantidade de ENIs secundários por VPC</td>
<td>1.000</td>
</tr>
</table>

### HAVIPs
<table >
<thead>
<tr>
<th width="70%">Recurso</th>
<th width="30%">Limite de cota</th>
</tr>
</thead>
<tbody><tr>
<td>Quantidade de HAVIPs padrão por VPC</td>
<td>10</td>
</tr>
</tbody></table>

### Grupos de segurança
<table>
<tr><th width="70%">Item</th><th width="30%">Descrição</th></tr>
<tr><td>Quantidade de grupos de segurança</td><td>50 por região</td></tr>
<tr><td>Quantidade de regras em um grupo de segurança</td><td>100 para regras de entrada e 100 para regras de saída</td></tr>
<tr><td>Quantidade de instâncias da CVM associadas a um grupo de segurança</td><td>2.000</td></tr>
<tr><td>Quantidade de grupos de segurança associados a uma instância do CVM</td><td>5</td></tr>
<tr><td>Quantidade de grupos de segurança que podem ser importados por um grupo de segurança</td><td>10</td></tr>
</table>

### ACLs de rede
<table >
<thead>
<tr>
<th width="70%">Recurso</th>
<th width="30%">Restrições</th>
</tr>
</thead>
<tbody><tr>
<td>Quantidade de ACLs de rede por VPC</td>
<td>50 partições</td>
</tr>
<tr>
<td>Quantidade de regras por ACL de rede</td>
<td>Entrada: 20<br>Saída: 20</td>
</tr>
<tr>
<td>Quantidade de ACLs de rede associadas a cada sub-rede</td>
<td>1 partição</td>
</tr>
</tbody></table>

### Modelos de parâmetros
<table>
<thead>
<tr>
<th width="70%">Tipo de recurso</th>
<th width="30%">Limite de cota</th>
</tr>
</thead>
<tbody><tr>
<td>Objetos de endereço IP (ipm)</td>
<td>Máx.: 1.000</td>
</tr>
<tr>
<td>Objetos de grupo de endereços IP (ipmg)</td>
<td>Máx.: 1.000</td>
</tr>
<tr>
<td>Objetos de porta de protocolo (ppm)</td>
<td>Máx.: 1.000</td>
</tr>
<tr>
<td>Objetos de grupo de portas de protocolo (ppmg)</td>
<td>Máx.: 1.000</td>
</tr>
<tr>
<td>Membros do endereço IP em um objeto de endereço IP (ipm)</td>
<td>Máx.: 20</td>
</tr>
<tr>
<td>Membros do objeto de endereço IP (ipm) em um objeto de grupo de endereços IP (ipmg)</td>
<td>Máx.: 20</td>
</tr>
<tr>
<td>Membros de porta de protocolo em um objeto de grupo de portas de protocolo (ppm) </td>
<td>Máx.: 20</td>
</tr>
<tr>
<td>Membros de objeto de porta de protocolo (ppm) em um objeto de grupo de portas de protocolo (ppmg)</td>
<td>Máx.: 20</td>
</tr>
<tr>
<td>Objetos de grupo de endereços IP (ipmg) que podem fazer referência ao mesmo objeto de endereço IP (ipm)</td>
<td>Máx.: 50</td>
</tr>
<tr>
<td>Objetos de grupo de portas de protocolo (ppmg) que podem fazer referência ao mesmo objeto de porta de protocolo (ppm)</td>
<td>Máx.: 50</td>
</tr>
</tbody></table>

### Sondas de rede 
<table >
<thead>
<tr>
<th width="70%">Recurso</th>
<th width="30%">Limite de cota</th>
</tr>
</thead>
<tbody><tr>
<td>Quantidade de sondas de rede criadas em cada VPC</td>
<td>50</td>
</tr>
</tbody></table>
