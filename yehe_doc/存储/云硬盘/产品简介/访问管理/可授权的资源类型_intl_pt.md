As permissões no nível do recurso referem-se à capacidade de especificar em quais recursos os usuários podem realizar operações. O CBS é compatível com permissões no nível dos recursos. Ou seja, é possível especificar quando os usuários têm permissão para executar algumas operações do CBS que são compatíveis com permissões no nível dos recursos ou quais recursos os usuários têm permissão para usar.
Os tipos de recursos que podem ser autorizados no Cloud Access Management (CAM) são os seguintes:

| Tipo de recurso | Método de descrição de recursos na política de autorização |
| :-------- | -------------- |
| [APIs do CBS](#CBSCorrelation) |  ` qcs::cvm:$region::volume/* `|

As [APIs do CBS](#CBSCorrelation) descrevem as operações das APIs do CBS que atualmente são compatíveis com as permissões no nível dos recursos, assim como recursos e chaves de condição compatíveis com cada operação. **Ao configurar o caminho do recurso**, é necessário substituir os parâmetros variáveis como `$region` e `$account` pelos seus parâmetros reais. Você também pode usar o asterisco `*` no caminho. Para obter mais informações, consulte [Exemplo do console](https://intl.cloud.tencent.com/document/product/213/10312).

<dx-alert infotype="notice" title="">
As operações de APIs do CBS não listadas na tabela não são compatíveis com permissões no nível dos recursos. Você ainda pode autorizar os usuários a realizar essas operações, mas o elemento de recurso da instrução da política deve ser especificado como `*`.
</dx-alert>

[](id:CBSCorrelation)
### APIs do CBS
<table>
<thead>
<tr>
<th align="left">Operação da API</th>
<th align="left">Caminho do recurso</th>
<th align="left">Chave de condição</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16313" target="_blank">Montar um disco em nuvem<br>AttachDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16312" target="_blank">Criar um disco em nuvem<br>CreateDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/32170" target="_blank">Consultar a lista de logs de operação do disco em nuvem<br>DescribeDiskOperationLogs</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16315" target="_blank">Consultar a lista de discos em nuvem<br>DescribeDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16316" target="_blank">Desmontar um disco em nuvem<br>DetachDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/15659" target="_blank">Modificar os atributos de discos em nuvem<br>ModifyDiskAttributes</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Modificar o modo de faturamento de um disco em nuvem<br>ModifyDisksChargeType</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Modificar o sinalizador de renovação de um disco em nuvem<br>ModifyDisksRenewFlag</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Renovar um disco em nuvem<br>RenewDisk</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16310" target="_blank">Expandir a capacidade de um disco em nuvem<br>ResizeDisk</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16321" target="_blank">Retornar um disco em nuvem<br>TerminateDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
</tbody></table>






