Este documento descreve como migrar uma instância da rede clássica para a VPC e configurar a solução de acesso híbrido durante a migração.

## Migração de uma única instância
Você pode migrar com facilidade uma instância da rede clássica para uma VPC. Consulte os detalhes abaixo.
<table >
<th>Tipo de instância</th>
<th>Descrição</th>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/213/20278>CVM</a></td>
<td> <li>A instância será reiniciada.<li>O IP da rede clássica será convertido imediatamente em um IP da VPC.</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/236/31915>TencentDB for MySQL</a></td>
<td rowspan=5>Tanto o IP da rede clássica quanto o IP da VPC ficam disponíveis por um período. O IP da rede clássica original permanece válido da seguinte forma: <ul><li>MySQL:  período padrão: 24 horas (1 dia); período máximo: 168 horas (7 dias)<li>MariaDB:  válido por 24 horas (1 dia)<li>TDSQL:  válido por 24 horas (1 dia)<li>Redis:  opções disponíveis: liberar agora, liberar após 1 dia, liberar após 2 dias, liberar após 3 dias e liberar após 7 dias<li>MongoDB:  o endereço IP original se tornará inválido imediatamente para a versão 4.0 ou posterior. As outras versões apresentam as opções: liberar agora, liberar após 1 dia, liberar após 2 dias, liberar após 3 dias e liberar após 7 dias</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/237/40160>TencentDB for MariaDB</a></td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/1042/33340>TDSQL for MySQL</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/239/31944>TencentDB for Redis</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/240/40126>TencentDB for MongoDB</a></td>
</tr>
</table>

>? Se você quiser manter os endereços IP do recurso inalterados após a alternância de rede, tente criar uma VPC que tenha IPs da rede clássica. Se isso for impossível, consulte a seguinte solução:
>+ Crie um serviço Private DNS e resolva seu nome de domínio. Após migrar os recursos para uma VPC, use o [Private DNS](https://intl.cloud.tencent.com/document/product/1097/40551) da Tencent Cloud.
>+ Use um IP público. 
>

## Solução de acesso híbrido durante a migração
O acesso híbrido significa que os serviços que estão sendo migrados podem acessar a rede clássica e uma VPC. A Tencent Cloud fornece a seguinte solução de acesso híbrido:
+ A acessibilidade do IP da rede clássica e do IP da VPC do serviço TencentDB garante o acesso híbrido no nível da instância do TencentDB.
    ![]()
+ O acesso ao Cloud Object Storage (COS) por meio de nome de domínio fornece a capacidade de acesso híbrido.
+ Para implementar a interconexão durante a migração, use junto com:
  + Classiclink:  permite que as CVMs baseadas na rede clássica se interconectem com os recursos da VPC, como as instâncias da CVM, do TencentDB e do CLB.
  + Conexão de terminal:  permite que as instâncias em uma VPC se comuniquem com os recursos na rede clássica (exceto as CVMs).
  ![]()
   >? 
   >+ Se você deseja estabelecer uma conexão de terminal, [envie um tíquete](https://console.cloud.tencent.com/workorder/category). Essa funcionalidade apenas possibilita o acesso a CVMs baseadas na rede clássica. Recomendamos migrar os seus recursos para uma VPC.
   >+ Para saber mais sobre as soluções VPC e Classiclink, consulte [Comunicação com a rede clássica](https://intl.cloud.tencent.com/document/product/215/35505). Para mais informações sobre como configurar um Classiclink, consulte [Classiclink](https://intl.cloud.tencent.com/document/product/215/41418).

