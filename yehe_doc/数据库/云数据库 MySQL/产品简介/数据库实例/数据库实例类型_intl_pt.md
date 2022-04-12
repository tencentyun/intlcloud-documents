Uma instância do TencentDB for MySQL é um ambiente de banco de dados executado de forma independente na Tencent Cloud. É a unidade básica para você adquirir o serviço TencentDB for MySQL. Você pode criar, modificar e excluir instâncias no console.
Cada instância é independente uma da outra com recursos isolados. Não há problemas de preempção de CPU, memória e E/S entre instâncias. Cada instância possui características próprias, como tipo e versão do banco de dados, e o sistema possui parâmetros correspondentes para controlar os comportamentos das instâncias.

Existem três tipos de instâncias disponíveis no TencentDB for MySQL:

<table>
<thead><tr>
<th>Tipo de instância</th><th width="20%">Definição</th><th width="15%">Arquitetura</th><th>Visível na lista de instâncias</th><th>Funcionalidade</th></tr></thead>
<tbody><tr>
<td>Instância de origem</td><td>Uma instância que pode ser lida e gravada</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Nó único</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">Dois nós</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">Três nós</a></td>
<td>Sim</td><td>Uma instância de source pode montar instâncias somente leitura e instâncias de recuperação de desastres para separação de leitura/gravação e recuperação de desastres remota</td></tr>
<tr>
<td>Instância somente leitura</td><td>Uma instância que só pode ser lida</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Nó único</a></td><td>Sim</td>
<td>Uma instância somente leitura não pode existir por conta própria. Em vez disso, ela deve ser afiliada a uma instância de source. Os dados dela vêm exclusivamente da sincronização com a instância de source, e devem estar localizados na mesma região que a instância de source</td></tr>
<tr>
<td>Instância de recuperação de desastres</td><td>Uma instância que permite a recuperação de desastres em AZs e regiões diferentes</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">Dois nós</a><td>Sim</td>
<td>Uma instância de recuperação de desastres é somente leitura quando sincronizada com uma instância de source. Ela pode interromper ativamente a sincronização e ser promovida a uma instância de source para acesso de leitura/gravação. A instância de recuperação de desastres deve estar localizada em uma região diferente da instância de source</td></tr>
</tbody></table>

### Referência
- Para mais informações sobre a criação de instância somente leitura e observações sobre ela, consulte [Criação de instância somente leitura](https://intl.cloud.tencent.com/document/product/236/7270).
- Para mais informações sobre como criar e configurar grupos do RO para instâncias somente leitura, consulte [Grupo do RO de instâncias somente leitura](https://intl.cloud.tencent.com/document/product/236/11361).
- Para mais informações sobre a criação de instância de recuperação de desastres e observações sobre ela, consulte [Instância de recuperação de desastres](https://intl.cloud.tencent.com/document/product/236/7272).
