Após a criação de uma instância do CLB, é necessário configurar um listener para ela. O listener capta as solicitações na instância e roteia o tráfego para servidores de back-end, com base na política de balanceamento de carga.

É necessário configurar um listener do CLB com os seguintes itens:
1. Protocolo e porta de escuta. A porta de escuta, ou porta de front-end, é usada para receber e encaminhar solicitações para servidores de back-end.
2. Políticas de escuta, como política de balanceamento de carga e [persistência de sessão](https://intl.cloud.tencent.com/document/product/214/6154).
3. Políticas de [verificação de integridade](https://intl.cloud.tencent.com/document/product/214/6097).
4. servidor de back-end. Vincule um servidor de back-end selecionando seu IP e porta. Uma porta de serviço, ou porta de back-end, é usada pelo servidor de back-end para receber solicitações.

## Tipos de protocolo aceitos
Um listener do CLB pode ouvir as solicitações da camada 4 e da camada 7 em uma instância do CLB e encaminhá-las a servidores de back-end, para processamento. A principal diferença entre a camada 4 e a camada 7 do CLB é se o protocolo da camada 4 ou 7 é usado para encaminhar o tráfego para o balanceamento de carga das solicitações do usuário.
- Protocolos da camada 4: protocolos da camada de transporte que recebem solicitações e encaminham o tráfego para o servidor de back-end, principalmente via VIP e porta.
- Protocolos da camada 7: protocolos da camada de aplicativos que distribuem o tráfego com base nas informações dessa camada, como URL e cabeçalho HTTP.

Se você usar um listener da camada 4 (ou seja, encaminhamento de protocolo da camada 4), a instância do CLB estabelecerá uma conexão TCP com o servidor de back-end na porta de escuta e encaminhará solicitações para o servidor de back-end diretamente. Esse processo não modifica nenhum pacote de dados (no modo de passagem) e tem alta eficiência de encaminhamento.

O CLB do Tencent Cloud aceita o encaminhamento de solicitações nos seguintes protocolos:
- TCP (camada de transporte)
- UDP (camada de transporte)
- TCP SSL (camada de transporte)
- HTTP (camada de aplicativos)
- HTTPS (camada de aplicativos)

>? Atualmente, os listeners TCP SSL aceitam instâncias do CLB de rede pública, mas não de rede privada ou da rede clássica.

<table>
<thead>
<tr>
<th width="12%">Tipo de protocolo</th>
<th width="12%">Protocolo</th>
<th width="40%">Descrição</th>
<th width="36%">Casos de uso</th>
</tr>
<tr>
<td rowspan="3">Protocolo da camada 4</td>
<td>TCP</td>
<td>Protocolo da camada de transporte confiável e orientado para conexões:<li>As extremidades de origem e destino devem executar um handshake de três vias para estabelecer uma conexão antes da transferência de dados.</li><li>A persistência de sessão baseada em IP de cliente (IP de origem) é aceita.</li><li>O IP do cliente pode ser encontrado na camada de rede.</li><li>O servidor pode obter o IP do cliente diretamente.</li></td>
<td>Ele é adequado para cenários com altos requisitos de confiabilidade e precisão de dados, mas requisitos relativamente baixos de velocidade de transferência, como transferência de arquivos, recebimento e envio de e-mails e login remoto. <br>Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/214/32517">Configuração de um listener TCP</a>.</td>
</tr>
<tr>
<td>UDP</td>
<td>Protocolo da camada de transporte sem conexão:<li>As extremidades de origem e destino não estabelecem uma conexão, nem mantêm o status da conexão. </li><li>Cada conexão UDP é ponto a ponto. </li><li>As comunicações um para um, um para muitos, muitos para um e muitos para muitos são aceitas.</li><li>A persistência de sessão baseada em IP de cliente (IP de origem) é aceita.</li><li>O servidor pode obter o IP do cliente diretamente.</li></td>
<td>Ele é adequado para cenários que têm altos requisitos de eficiência de transferência, mas requisitos relativamente baixos de precisão, como sistema de mensagens instantâneas e vídeos online. <br>Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/214/32518">Configuração de um listener UDP</a>.</td>
</tr>
<tr>
<td>TCP SSL</td>
<td>TCP seguro: <li>Os listeners TCP SSL aceitam a configuração de certificados para evitar solicitações de acesso não autorizadas.</li><li>O gerenciamento de certificado unificado é fornecido para o CLB, a fim de implementar a descriptografia.</li><li>São aceitas autenticações unilaterais e mútuas.</li><li>O servidor pode obter o IP do cliente diretamente.</li></td>
<td>É adequado para cenários que têm altos requisitos de segurança quando o TCP é usado, e aceita protocolos personalizados baseados em TCP. <br>Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/214/32519">Configuração de um listener TCP SSL</a>.</td>
</tr>
<tr>
<td rowspan="2">Protocolo da camada 7</td>
<td>HTTP</td>
<td>Protocolo da camada de aplicativos: <li>O encaminhamento com base no nome de domínio e URL solicitados é aceito. </li><li>A persistência de sessão baseada em cookies é aceita.</li></td>
<td>Ele é adequado para aplicações em que o conteúdo da solicitação precisa ser identificado, como aplicativos web e móveis, etc. <br>Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/214/32515">Configuração de um listener HTTP</a>.</td>
</tr>
<tr>
<td>HTTPS</td>
<td>Protocolo da camada de aplicativos criptografada:<li>O encaminhamento com base no nome de domínio e URL solicitados é aceito.</li><li>A persistência de sessão baseada em cookies é aceita.</li><li>O gerenciamento de certificados unificado é fornecido para o CLB, a fim de implementar a descriptografia.</li><li>São aceitas autenticações unilaterais e mútuas.</li></td>
<td>Ele é adequado para aplicativos HTTP que requerem transmissão criptografada.<br>Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/214/32516">Configuração de um listener HTTPS</a>.</td>
</tr>
</tbody></table>

## Configuração de portas
<table>
<thead>
<tr>
<th width="16%">Tipo de porta</th>
<th>Observações</th>
<th width="50%">Restrições</th>
</tr>
</thead>
<tbody><tr>
<td>Porta de escuta (porta de front-end)</td>
<td>As portas de escuta são usadas por instâncias do CLB para receber e encaminhar solicitações a servidores de back-end<br/>Você pode configurar as instâncias do CLB para as portas 1 a 65535, como as portas 21 (FTP), 25 (SMTP), 80 (HTTP) e 443 (HTTPS), etc.</td>
<td><ul>Em uma instância do CLB:<li>As portas de escuta do UDP podem ser usadas para TCP; por exemplo, um listener `TCP:80` e um listener `UDP:80` podem coexistir.</li><li>As portas de escuta devem ser exclusivas para o mesmo tipo de protocolo. Como o TCP, o TCP SSL, o HTTP e o HTTPS são de TCP, um listener `TCP:80` e um listener `HTTP:80` não podem coexistir, por exemplo.</li></ul></td>
</tr>
<tr>
<td>Porta de serviço (porta de back-end)</td>
<td>As portas de serviço são usadas por instâncias do CVM para fornecer serviços, receber e processar o tráfego de instâncias do CLB.<br/>Em uma instância do CLB, uma porta de escuta pode encaminhar o tráfego para portas de várias instâncias do CVM.</td>
<td><ul>Em uma instância do CLB:<li>As portas de serviço de protocolos de escuta diferentes não precisam ser exclusivas; por exemplo, os listener `HTTP:80` e `HTTPS:443` podem ser vinculados à mesma porta de uma instância do CVM.</li><li>Ao usar o mesmo protocolo de escuta, cada porta de serviço de back-end pode ser vinculada a apenas um listener, ou seja, o quádruplo (VIP, protocolo de escuta, IP privado do servidor de back-end e porta de serviço de back-end) deve ser exclusivo.</li></ul></td>
</tr>
</tbody></table>
