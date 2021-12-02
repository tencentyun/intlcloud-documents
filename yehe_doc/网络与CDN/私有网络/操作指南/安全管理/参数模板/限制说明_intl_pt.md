### Limites de uso
- Os formatos aceitos pelo modelo de endereço IP são os seguintes:
 - Endereço IP único: como `10.0.0.1`;
 - Endereços IP consecutivos: como `10.0.0.1`-`10.0.0.100`;
 - Intervalo de IP: como `10.0.1.0/24`.
- Os formatos aceitos pelo modelo de portas são os seguintes:
 - Porta única: como `TCP:80`;
 - Várias portas: como `TCP:80,443`;
 - Intervalo de portas: como `TCP:3306-20000;
 - Todas as portas: como `TCP:ALL`.

### Limites de cota 
<table>
<thead>
<tr>
<th>Instância</th>
<th>Limite superior</th>
</tr>
</thead>
<tbody><tr>
<td>Objetos de endereços IP (ipm)</td>
<td>1.000 por locatário</td>
</tr>
<tr>
<td>Objetos de grupos de endereços IP (ipmg)</td>
<td>1.000 por locatário</td>
</tr>
<tr>
<td>Objetos de portas de protocolo (ppm)</td>
<td>1.000 por locatário</td>
</tr>
<tr>
<td>Objetos de grupos de portas de protocolo (ppmg)</td>
<td>1.000 por locatário</td>
</tr>
<tr>
<td>Membros do endereço IP em um objeto de endereço IP (ipm)</td>
<td>20 por locatário</td>
</tr>
<tr>
<td>Membros do objeto de endereço IP (ipm) em um objeto de grupo de endereços IP (ipmg)</td>
<td>20 por locatário</td>
</tr>
<tr>
<td>Membros de porta de protocolo em um objeto de grupo de portas de protocolo (ppm) </td>
<td>20 por locatário</td>
</tr>
<tr>
<td>Membros de objeto de porta de protocolo (ppm) em um objeto de grupo de portas de protocolo (ppmg)</td>
<td>20 por locatário</td>
</tr>
<tr>
<td>Objetos de grupo de endereços IP (ipmg) que podem fazer referência ao mesmo objeto de endereço IP (ipm)</td>
<td>50 por locatário</td>
</tr>
<tr>
<td>Objetos de grupo de portas de protocolo (ppmg) que podem fazer referência ao mesmo objeto de porta de protocolo (ppm)</td>
<td>50 por locatário</td>
</tr>
</tbody></table>

>?Se o modelo de parâmetros for referenciado por um grupo de segurança, os IPs e portas no modelo serão convertidos em várias regras do grupo de segurança (até 2.000).

