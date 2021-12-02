Os grupos de segurança são usados para gerenciar se um Cloud Virtual Machine (CVM) fica acessível. É possível configurar regras de entrada e de saída para grupos de segurança para especificar se o seu servidor pode ser acessado ou pode acessar outros recursos de rede.
As regras padrão de entrada e de saída para grupos de segurança são as seguintes:
- **Para garantir a segurança dos dados, a regra de entrada para um grupo de segurança é uma política de rejeição que nega o acesso remoto de redes externas.** Para tornar seu CVM acessível a recursos externos, é necessário permitir a regra de entrada para a porta correspondente.
- A regra de saída para um grupo de segurança especifica se o CVM pode acessar recursos de redes externas. Se você selecionar **Open all Ports (Abrir todas as portas)** ou **Open Ports 22, 80, 443, 3389 and ICMP protocol (Abrir as portas 22, 80, 443, 3389 e o protocolo ICMP)**, a regra de saída para o grupo de segurança abre as portas para a internet. Se você selecionar uma regra de grupo de segurança personalizada, a regra de saída bloqueia todas as portas por padrão e é necessário configurar a regra de saída para permitir que a porta correspondente acesse recursos de redes externas.

## Casos de uso comuns
Este documento descreve vários casos de uso comuns de grupos de segurança. Se algum dos casos abaixo atender aos seus requisitos, é possível definir seus grupos de segurança de acordo com a configuração recomendada para o caso de uso correspondente.

### Cenário 1: conexão remota a um CVM do Linux por SSH
**Caso**: você criou um CVM do Linux e deseja se conectar a ele remotamente por SSH.
**Solução**: ao [adicionar uma regra de entrada](https://intl.cloud.tencent.com/document/product/215/35513), defina **Type (Tipo)** como **Linux Login (Login no Linux)** e abra a porta TCP 22 para a internet, a fim de permitir o login do Linux por SSH.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de endereços IP) para a internet, conforme necessário. Isso permite que você configure os endereços IP de origem que podem acessar os CVMs por SSH de forma remota.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Login no Linux</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: um endereço IP ou intervalo de endereços IP especificado</li></ul></td><td>TCP: 22</td><td>Permitir</td></tr>
</table>

### Cenário 2: conexão remota a um CVM do Windows por RDP
**Caso**: você criou um CVM do Windows e deseja conectar-se a ele remotamente por meio da Conexão de área de trabalho remota (RDP).
**Solução**: ao [adicionar uma regra de entrada](https://intl.cloud.tencent.com/document/product/215/35513), defina **Type (Tipo)** como **Windows Login (Login no Windows)** e abra a porta TCP 3389 para a internet, a fim de habilitar o login remoto no Windows.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de endereços IP) para a internet, conforme necessário. Isso habilita que você configure os endereços IP de origem que podem acessar remotamente os CVMs por RDP.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Login no Windows</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: um endereço IP ou intervalo de endereços IP especificado</li></ul></td><td>TCP: 3389</td><td>Permitir</td></tr>
</table>

### Cenário 3: execução de ping de um CVM a partir da internet
**Caso**: você criou um CVM e deseja verificar se a comunicação o CVM e outros CVMs está normal.
**Solução**: teste a conexão usando o programa de ping. Especificamente, ao [adicionar uma regra de entrada](https://intl.cloud.tencent.com/document/product/215/35513), defina o **Type (Tipo)** como **Ping** e abra as portas do protocolo ICMP para a internet, a fim de permitir que outros CVMs acessem esse CVM por meio do ICMP.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de endereços IP) para a internet, conforme necessário. Isso permite que você configure os endereços IP de origem que podem acessar esse CVM por meio do ICMP.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Ping</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: um endereço IP ou intervalo de endereços IP especificado</li></ul></td><td>ICMP</td><td>Permitir</td></tr>
</table>

### Cenário 4: login remoto em um CVM por meio do Telnet
**Caso**: você deseja fazer login remotamente em um CVM por meio do Telnet.
**Solução**: ao [adicionar uma regra de entrada](https://intl.cloud.tencent.com/document/product/215/35513), configure a seguinte regra de grupo de segurança:
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: um endereço IP ou intervalo de endereços IP especificado</li></ul></td><td>TCP: 23</td><td>Permitir</td></tr>
</table>

### Cenário 5: autorização de acesso a um serviço Web por meio de HTTP ou HTTPS
**Caso**: você criou um site e deseja permitir que os usuários o acessem por meio de HTTP ou HTTPS.
**Solução**: ao [adicionar uma regra de entrada](https://intl.cloud.tencent.com/document/product/215/35513), configure as regras de grupo de segurança, conforme necessário:
- Permitir que todos os endereços IP na internet acessem este site
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Permitir</td></tr>
<tr><td>Entrada</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Permitir</td></tr>
</table>
- Permitir que alguns endereços IP na internet acessem este site
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>HTTP (80)</td><td>Endereço IP ou intervalo de endereços IP que tem permissão para acessar seu site</td><td>TCP: 80</td><td>Permitir</td></tr>
<tr><td>Entrada</td><td>HTTPS (443)</td><td>Endereço IP ou intervalo de endereços IP que tem permissão para acessar seu site</td><td>TCP: 443</td><td>Permitir</td></tr>
</table>

### Cenário 6: permissão para um endereço IP externo acessar uma porta especificada
**Caso**: você implantou um serviço e deseja que a porta de serviços especificada (como a porta 1101) seja acessível externamente.
**Solução**: ao [adicionar uma regra de entrada](https://intl.cloud.tencent.com/document/product/215/35513), defina o **Type (Tipo)** como **Custom (Personalizado)** e abra a porta TCP 1101 para a internet, a fim de que recursos externos acessem a porta de serviços especificada.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de endereços IP) para a internet, conforme necessário. Isso permite que o endereço IP de origem acesse a porta de serviços especificada.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: um endereço IP ou intervalo de endereços IP especificado</li></ul></td><td>TCP: 1101</td><td>Permitir</td></tr>
</table>

### Cenário 7: negação do acesso a uma porta especificada por endereços IP externos
**Caso**: você implantou um serviço e deseja bloquear o acesso externo a uma porta de serviços especificada (como a porta 1102).
**Solução**: ao [adicionar uma regra de entrada](https://intl.cloud.tencent.com/document/product/215/35513), defina o **Type (Tipo)** como **Custom (Personalizado)**, configure a porta TCP 1102 e defina a **Policy (Política)** como **Reject (Rejeitar)**, a fim de negar o acesso externo à porta de serviços especificada.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: um endereço IP ou intervalo de endereços IP especificado</li></ul></td><td>TCP: 1102</td><td>Rejeitar</td></tr>
</table>

### Cenário 8: permissão para um CVM acessar apenas um endereço IP externo especificado
**Caso**: você deseja que seu CVM acesse apenas um endereço IP externo especificado.
**Solução**: adicione duas regras de saída de grupo de segurança, referindo-se às seguintes configurações:
- Permitir que a instância do CVM acesse um endereço IP público especificado
- Não permitir que a instância do CVM acesse endereços IP públicos por meio de nenhum protocolo

> A regra que permite o acesso deve ter uma prioridade mais alta do que a regra que nega o acesso.
>
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Saída</td><td>Personalizado</td><td>O endereço IP público especificado que pode ser acessado pelo CVM</td><td>O protocolo e a porta necessários</td><td>Permitir</td></tr>
<tr><td>Saída</td><td>Personalizado</td><td>0.0.0.0/0</td><td>Todos</td><td>Rejeitar</td></tr>
</table>

### Cenário 9: negação para um CVM acessar apenas um endereço IP externo especificado
**Caso**: você não deseja que seu CVM acesse um endereço IP externo especificado.
**Solução**: adicione uma regra de grupo de segurança referindo-se à seguinte configuração:
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Saída</td><td>Personalizado</td><td>O endereço IP público especificado que você não deseja que seja acessado pelo CVM</td><td>Todos</td><td>Rejeitar</td></tr>
</table>

### Cenário 10: upload ou download de um arquivo de um CVM por FTP
**Caso**: você deseja fazer upload ou download de um arquivo de um CVM usando um programa FTP.
**Solução**: adicione uma regra de grupo de segurança referindo-se à seguinte configuração:
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td>0.0.0.0/0</td><td>TCP: 20-21</td><td>Permitir</td></tr>
</table>

## Combinação de vários cenários
Em um cenário real, pode ser útil configurar várias regras de grupo de segurança com base nos requisitos de serviço, por exemplo, configurar regras de entrada ou saída ao mesmo tempo. Um CVM pode estar vinculado a um ou mais grupos de segurança. Quando um CVM está vinculado a vários grupos de segurança, eles são combinados e executados em ordem decrescente de prioridade. É possível ajustar as prioridades dos grupos de segurança a qualquer momento. 

