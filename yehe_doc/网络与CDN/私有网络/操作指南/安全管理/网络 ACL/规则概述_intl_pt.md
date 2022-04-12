A lista de controle de acesso (ACL) de rede é uma camada opcional de segurança que limita o tráfego de e para as sub-redes com precisão de protocolo e porta.

## Visão geral
Você pode associar uma ACL de rede a várias sub-redes para manter o tráfego e controlar com precisão sua entrada e saída, definindo regras de entrada e saída.
Por exemplo, quando você hospeda um aplicativo da web com várias camadas em uma instância da VPC da Tencent Cloud e cria sub-redes diferentes para serviços de camada da web, camada lógica e camada de dados, é possível usar uma ACL de rede para garantir que as sub-redes da camada da web e da camada de dados não podem acessar umas às outras, mas apenas a sub-rede da camada lógica pode acessar as sub-redes da camada da web e da camada de dados.
![](https://main.qcloudimg.com/raw/f8490b4c94db7cd50f2cbe29524d237d.jpg)


## Regras de ACL
Quando uma regra de ACL de rede for adicionada ou excluída, a alteração será aplicada automaticamente às sub-redes associadas.
Você pode configurar regras de ACL de rede de entrada e de saída. Cada regra consiste em:
+ IP de origem/IP de destino: insira o IP de origem para uma regra de entrada ou o IP de destino para uma regra de saída. Formatos aceitos:
  + IP único: como “192.168.0.1” ou “FF05::B5”
  + Bloco CIDR: como “192.168.1.0/24” ou “FF05:B5::/60”
  + Todos os endereços IPv4: “0.0.0.0/0”
- Protocol type (Tipo de protocolo): indica os tipos de protocolo que uma regra de ACL permite ou nega, por exemplo, TCP e UDP.
- Port (Porta): indica a porta de origem ou destino do tráfego. Formatos aceitos:
  + Porta única: como “22” ou “80”
  + Intervalo de portas: como “1-65535” ou “100-20000”
  + Todas as portas: todas
- Policy (Política): indica se deve permitir ou negar a solicitação de acesso.

### Regras padrão
Depois de criada, cada ACL de rede tem duas regras padrão que não podem ser modificadas ou excluídas, com a prioridade mais baixa.
- Regra de entrada padrão
<table>
<thead>
<tr>
<th>Tipo de protocolo</th>
<th>Porta</th>
<th>IP de origem</th>
<th>Política</th>
<th>Descrição</th>
</tr>
</thead>
<tbody><tr>
<td>Todas</td>
<td>Todas</td>
<td>0.0.0.0/0</td>
<td>Negar</td>
<td>Nega todo o tráfego de entrada.</td>
</tr>
</tbody></table>

- Regra de saída padrão
<table>
<thead>
<tr>
<th>Tipo de protocolo</th>
<th>Porta</th>
<th>IP de destino</th>
<th>Política</th>
<th>Descrição</th>
</tr>
</thead>
<tbody><tr>
<td>Todas</td>
<td>Todas</td>
<td>0.0.0.0/0</td>
<td>Negar</td>
<td>Nega todo o tráfego de saída.</td>
</tr>
</tbody></table>

### Prioridades das regras
- As regras de uma ACL de rede são priorizadas de cima para baixo. A regra no topo da lista tem a prioridade mais alta e entrará em vigor primeiro, já a regra na parte inferior tem a prioridade mais baixa e entrará em vigor por último.
- Se houver um conflito de regras, a regra com a prioridade mais alta prevalecerá por padrão.
- Quando o tráfego entrar ou sair de uma sub-rede vinculada a uma ACL de rede, as regras de ACL de rede serão correspondidas sequencialmente de cima para baixo. Se uma regra for correspondida com êxito e entrar em vigor, as regras posteriores não serão correspondidas.

#### Exemplo de aplicação
Para permitir que todos os endereços IP de origem acessem todas as portas de CVMs em uma sub-rede associada a uma ACL de rede, e negar que o endereço IP de origem HTTP de `192.168.200.11/24` acesse a porta 80, adicione as seguintes duas regras de ACL de rede para tráfego de entrada:

| Tipo de protocolo | Porta | IP de origem | Política | Descrição |
| --- | --- | --- | --- |---|
| HTTP | 80 | 192.168.200.11/24 | Negar | Nega que este endereço IP de serviços HTTP acesse a porta 80. |
| Todos | Todas | 0.0.0.0/0 | Permitir | Permite que todos os endereços IP de origem acessem todas as portas. |


## Grupos de segurança vs. ACLs de rede
<table>
<thead>
<tr>
<th width="12%">Item</th>
<th width="45%">Grupo de segurança</th>
<th width="43%">ACL de rede</th>
</tr>
</thead>
<tbody><tr>
<td>Limitação de tráfego</td>
<td>Limitação de tráfego no nível de instâncias, como CVM e banco de dados</td>
<td>Limitação de tráfego no nível de sub-redes</td>
</tr>
<tr>
<td>Regra</td>
<td>Regras permitir e negar</td>
<td>Regras permitir e negar</td>
</tr>
<tr>
<td>Com estado e sem estado</td>
<td>Com estado: o tráfego retornado é permitido automaticamente, sem estar sujeito a nenhuma regra.</td>
<td>Sem estado: o tráfego retornado deve ser explicitamente permitido pelas regras.</td>
</tr>
<tr>
<td>Tempo efetivo</td>
<td>As regras são aplicadas a uma instância, como da CVM ou TencentDB, apenas se você especificar um grupo de segurança ao criar a instância ou associar um grupo de segurança à instância após sua criação.</td>
<td>As regras de ACL são aplicadas automaticamente a todas as instâncias, como instâncias da CVM e do TencentDB na sub-rede associada.</td>
</tr>
<tr>
<td>Prioridade da regra</td>
<td>Se houver um conflito de regras, a regra com a prioridade mais alta prevalecerá por padrão.</td>
<td>Se houver um conflito de regras, a regra com a prioridade mais alta prevalecerá por padrão.</td>
</tr>
</tbody></table>
