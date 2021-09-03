Ao configurar grupos de segurança, você consegue gerenciar o acesso a um Cloud Virtual Machine (CVM). É possível configurar regras de entrada e de saída para grupos de segurança para especificar se o seu servidor pode ser acessado ou pode acessar outros recursos de rede.
As regras padrão de entrada e de saída para grupos de segurança são as seguintes:
- **Para garantir a segurança dos dados, a regra de entrada para um grupo de segurança é uma política de rejeição que proíbe o acesso remoto de redes externas.** Para habilitar o acesso de redes externas ao seu CVM, é necessário permitir a regra de entrada da porta correspondente.
- A regra de saída para um grupo de segurança especifica se o CVM pode acessar recursos de redes externas. Se você selecionar "Open all Ports (Abrir todas as portas)" ou "Open Ports 22, 80, 443, 3389 and ICMP protocol (Abrir as portas 22, 80, 443, 3389 e o protocolo ICMP)", a regra de saída para o grupo de segurança abre todas as portas para a internet. Se você selecionar uma regra de grupo de segurança personalizada, a regra de saída bloqueia todas as portas por padrão e é necessário configurar a regra de saída para permitir que a porta correspondente acesse recursos de redes externas.

## Casos de uso comuns
Este documento descreve vários casos de uso comuns de grupos de segurança. Se os casos a seguir atenderem aos seus requisitos, será possível configurar os grupos de segurança de acordo com as configurações recomendadas para os casos de uso correspondentes.

### Cenário 1: Conexão remota a um CVM do Linux por SSH
**Caso**: você criou um CVM do Linux e deseja se conectar a ele remotamente por SSH.
**Solução**: ao [adicionar uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272), defina **Type (Tipo)** como **Login Linux CVMs(22)** e abra a porta TCP 22 para a internet, a fim de habilitar o login do Linux por SSH.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de IP) para a internet, conforme necessário. Isso permite que você configure os endereços IP de origem dos CVMs que podem ser conectados remotamente por SSH.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Login no Linux</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: insira seu endereço IP ou intervalo de IP especificado</li></ul></td><td>TCP: 22</td><td>Permitir</td></tr>
</table>

### Cenário 2: Conexão remota a um CVM do Windows por RDP
**Caso**: você criou um CVM do Windows e deseja se conectar a ele remotamente usando o desktop remoto (RDP).
**Solução**: ao [adicionar uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272), defina **Type (Tipo)** como **Login Windows CVMs(3389)** e abra a porta TCP 3389 para a internet, a fim de habilitar o login remoto no Windows.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de IP) para a internet, conforme necessário. Isso permite que você configure os endereços IP de origem dos CVMs que podem ser conectados remotamente por RDP.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Login no Windows</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: insira seu endereço IP ou intervalo de IP especificado</li></ul></td><td>TCP: 3389</td><td>Permitir</td></tr>
</table>

### Cenário 3: Execução de ping de um CVM na internet
**Caso**: você criou um CVM e deseja testar se a comunicação dele com outros CVMs está normal.
**Solução**: teste a conexão usando o comando ping. Especificamente, ao [adicionar uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272), defina o **Type (Tipo)** como **Ping** e abra as portas do protocolo ICMP para a internet, a fim de permitir que outros CVMs acessem esse CVM por meio do ICMP.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de IP) para a internet, conforme necessário. Isso permite que você configure os endereços IP de origem dos CVMs que podem acessar esse CVM por meio do ICMP.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Ping</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: insira seu endereço IP ou intervalo de IP especificado</li></ul></td><td>ICMP</td><td>Permitir</td></tr>
</table>

### Cenário 4: Login remoto em um CVM por meio do Telnet
**Caso**: você deseja fazer login remotamente em um CVM usando o Telnet.
**Solução**: ao [adicionar uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272), configure a seguinte regra:
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: insira seu endereço IP ou intervalo de IP especificado</li></ul></td><td>TCP: 23</td><td>Permitir</td></tr>
</table>

### Cenário 5: Permissão de acesso a um serviço Web por meio de HTTP ou HTTPS
**Caso**: você criou um site e deseja permitir que os usuários o acessem por meio de HTTP ou HTTPS.
**Solução**: ao [adicionar uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272), configure as seguintes regras, conforme necessário:
- Permitir que todos os endereços IP públicos acessem este site
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Permitir</td></tr>
<tr><td>Entrada</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Permitir</td></tr>
</table>
- Permitir que alguns dos endereços IP públicos acessem este site
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>HTTP (80)</td><td>Endereço IP ou intervalo de IP que tem permissão para acessar seu site</td><td>TCP: 80</td><td>Permitir</td></tr>
<tr><td>Entrada</td><td>HTTPS (443)</td><td>Endereço IP ou intervalo de IP que tem permissão para acessar seu site</td><td>TCP: 443</td><td>Permitir</td></tr>
</table>

### Cenário 6: Permissão para um endereço IP externo acessar uma porta especificada
**Caso**: você implantou um serviço e deseja que a porta de serviços especificada (como a porta 1101) seja acessível externamente.
**Solução**: ao [adicionar uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272), defina o **Type (Tipo)** como **Custom (Personalizado)** e abra a porta TCP 1101 para a internet, a fim de permitir o acesso externo à porta de serviços especificada.
É possível abrir todos os endereços IP ou um endereço IP especificado (ou intervalo de IP) para a internet, conforme necessário. Isso permite que o endereço IP de origem acesse a porta de serviços especificada.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: insira seu endereço IP ou intervalo de IP especificado</li></ul></td><td>TCP: 1101</td><td>Permitir</td></tr>
</table>

### Cenário 7: Rejeição do acesso a uma porta especificada por endereços IP externos
**Caso**: você implantou um serviço e deseja impedir o acesso externo a uma porta de serviços especificada (como a porta 1102).
**Solução**: ao [adicionar uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272), defina o **Type (Tipo)** como **Custom (Personalizado)**, configure a porta TCP 1102 e defina a **Policy (Política)** como **Reject (Rejeitar)**, a fim de rejeitar o acesso externo à porta de serviços especificada.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td><ul style="margin: 0;"><li>Todos os endereços IP: 0.0.0.0/0</li><li>Endereço IP especificado: insira seu endereço IP ou intervalo de IP especificado</li></ul></td><td>TCP: 1102</td><td>Rejeitar</td></tr>
</table>

### Cenário 8: Permissão para um CVM acessar apenas um endereço IP externo especificado
**Caso**: você deseja que seu CVM acesse apenas um endereço IP externo especificado.
**Solução**: adicione duas regras de saída de grupo de segurança, referindo-se à seguinte configuração.
- Permitir que a instância do CVM acesse um endereço IP externo especificado
- Proibir que a instância do CVM acesse quaisquer endereços IP públicos por meio de qualquer protocolo

> As regras que permitem o acesso têm prioridade sobre as que o proíbem.
>
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Saída</td><td>Personalizado</td><td>Endereço IP público especificado que pode ser acessado pelo CVM</td><td>Protocolo e porta necessários</td><td>Permitir</td></tr>
<tr><td>Saída</td><td>Personalizado</td><td>0.0.0.0/0</td><td>Todos</td><td>Rejeitar</td></tr>
</table>

### Cenário 9: Proibição de um CVM acessar um endereço IP externo especificado
**Caso**: você não deseja que seu CVM acesse um endereço IP externo especificado.
**Solução**: adicione uma regra de grupo de segurança referindo-se à seguinte configuração.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Saída</td><td>Personalizado</td><td>Endereço IP público especificado que você não deseja que sua instância do CVM acesse</td><td>Todos</td><td>Rejeitar</td></tr>
</table>

### Cenário 10: Upload ou download de um arquivo de um CVM por FTP
**Caso**: você deseja fazer upload ou download de um arquivo de um CVM usando um software FTP.
**Solução**: adicione uma regra de grupo de segurança referindo-se à seguinte configuração.
<table>
<tr><th>Direção</th><th>Tipo</th><th>Origem</th><th>Porta do protocolo</th><th>Política</th></tr>
<tr><td>Entrada</td><td>Personalizado</td><td>0.0.0.0/0</td><td>TCP: 20 ou 21</td><td>Permitir</td></tr>
</table>

## Combinação de vários cenários
Em um cenário real, pode ser necessário configurar várias regras de grupos de segurança com base nos requisitos da sua empresa, como configurar regras de entrada ou de saída ao mesmo tempo. Um CVM pode estar vinculado a um ou mais grupos de segurança. Quando um CVM está vinculado a vários grupos de segurança, eles são combinados e executados em ordem decrescente de prioridade. É possível ajustar a prioridade de um grupo de segurança a qualquer momento. Para obter informações acerca das prioridades das regras de grupos de segurança, consulte [Prioridades de grupos de segurança](http://intl.cloud.tencent.com/document/product/213/12452).

