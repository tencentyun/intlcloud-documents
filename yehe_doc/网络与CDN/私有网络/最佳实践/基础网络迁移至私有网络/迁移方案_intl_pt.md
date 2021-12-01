Este documento descreve como migrar instâncias do CVM, do TencentDB for MySQL e do TencentDB for Redis da rede clássica para um VPC.

## Informações gerais
- A rede clássica é um pool de recursos de rede pública para todos os usuários do Tencent Cloud. Os IPs privados de todos os CVMs são atribuídos pelo Tencent Cloud. Não é possível personalizar os intervalos de IP ou os endereços de IP.
- Um VPC é um espaço de rede isolado logicamente no Tencent Cloud. Em um VPC, é possível personalizar os intervalos de IP, os endereços IP e as políticas de roteamento, tornando-o mais adequado para os casos de uso que exigem configurações personalizadas.

Como os recursos da rede clássica se tornam cada vez mais escassos e não podem ser expandidos, a partir de 13 de junho de 2017, todas as novas contas do Tencent Cloud só podem criar instâncias (incluindo instâncias do CVM e do TencentDB) em um VPC em vez da rede clássica. Cada vez mais usuários estão migrando suas instâncias da rede clássica para o VPC.


## Instruções
Verifique as instruções abaixo de acordo com seu tipo de recurso.
<table>
<thead>
<tr>
<th width="20%">Tipo de recurso</th>
<th width="25%">Características</th>
<th width="35%">Limitação</th>
<th width="20%">Instruções</th>
</tr>
</thead>
<tbody><tr>
<td>CVM</td>
<td>As instâncias migradas do CVM são as mesmas que estão sendo criadas no VPC.</td>
<td><li>A migração da rede clássica para o VPC NÃO PODE ser revertida. Após a migração, a instância do CVM não poderá se comunicar com os serviços do Tencent Cloud na rede clássica</li>
<li>A instância do CVM precisa ser reiniciada</li>
<li>O IP privado muda do IP da rede clássica para IP do VPC</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/20278" target="_blank">Alteração para VPC</a></td>
</tr>
<tr>
<td>TencentDB for MySQL</td>
<td><li>O acesso do VPC entra em vigor logo após a migração.</li><li>A rede clássica original permanece acessível por até 7 dias após a migração.</li><li>A conexão do banco de dados não é afetada durante a migração.</li></td>
<td><li>A migração da rede clássica para o VPC NÃO PODE ser revertida. Após a migração, a instância do TencentDB for MySQL não poderá se comunicar com os serviços do Tencent Cloud na rede clássica</li>
<li>O IP privado muda do IP da rede clássica para IP do VPC.</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">Alteração de rede</a></td>
</tr>
<tr>
<td>TencentDB for Redis</td>
<td><li>O acesso do VPC entra em vigor logo após a migração.</li><li>A rede clássica original permanece acessível por até 7 dias após a migração.</li><li>A conexão do banco de dados não é afetada durante a migração.</li></td>
<td><li>A migração da rede clássica para o VPC NÃO PODE ser revertida. Após a migração, a instância do TencentDB for Redis não poderá se comunicar com os serviços do Tencent Cloud na rede clássica</li>
<li>O IP privado muda do IP da rede clássica para IP do VPC.</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31944?from=10680#.E6.9B.B4.E6.8D.A2-redis-.E7.BD.91.E7.BB.9C" target="_blank">Alteração da rede do Redis</a></td>
</tr>
</tbody></table>

## Exemplo de migração
>?Este exemplo é apenas para referência. Antes de sua migração real, avalie o impacto em seu negócio e desenvolva um plano de migração detalhado.
### Descrição

Suponha que um serviço da rede clássica use quatro serviços do Tencent Cloud, incluindo o CLB, o CVM, o TencentDB for MySQL e o TencentDB for Redis. A relação desses serviços é descrita abaixo: 
- O CLB público está vinculado a dois CVMs como servidores de back-end.
- O TencentDB for MySQL e o TencentDB for Redis atuam como bancos de dados para aplicativos implantados nos dois CVMs.
![](https://main.qcloudimg.com/raw/bf54dd1832d0e16c756984e305772e06.png)

## Instruções para a migração
1. Migre as instâncias do TencentDB para um VPC. Após a migração, o acesso à rede clássica original permanece disponível por um determinado período, mantendo assim a conexão com o banco de dados e a disponibilidade do seu serviço. Durante esse período, você pode concluir a migração de outros serviços.
![](https://main.qcloudimg.com/raw/427fe3f0445056c94332df90d4cd9bb3.png)
2. Crie dois CVMs e implante os serviços conforme necessário no VPC para o qual os bancos de dados sejam migrados. Depois, teste se os CVMs conseguem acessar as instâncias do TencentDB.
![](https://main.qcloudimg.com/raw/4425f9af34e3df70a84f1a80e8a7ba40.png)
3. Crie um CLB público no VPC de bancos de dados e associe-o aos dois CVMs criados na etapa anterior. Execute uma verificação de integridade para evitar a interrupção do serviço devido a uma exceção.
![](https://main.qcloudimg.com/raw/8dab2d96a40f1df4eefa9ad04117cb2b.png)
4. Aguarde a conclusão da migração. Libere os recursos do CLB e do CVM da rede pública original na rede clássica.
![](https://main.qcloudimg.com/raw/cb567a4a3f88c4bc4c8d787d60f512f3.png)

