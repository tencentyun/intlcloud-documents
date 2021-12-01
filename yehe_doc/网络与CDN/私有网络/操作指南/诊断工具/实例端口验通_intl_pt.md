A funcionalidade de verificação de portas da instância pode ajudar a detectar a acessibilidade da porta de um grupo de segurança associado a instâncias do CVM, localizar falhas e melhorar a experiência do usuário.
Essa funcionalidade aceita detecção de acessibilidade de portas comuns e personalizadas. Confira abaixo as portas comuns.
 <table>
<thead>
<tr>
<th>Regra</th>
<th>Porta</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="7">Regras de entrada</td>
<td>Protocolo ICMP</td>
<td>Usado para passar mensagens de controle, como o comando ping. ICMP é um protocolo de controle e nenhuma porta está envolvida.</td>
</tr>
<tr>
<td>TCP:20</td>
<td rowspan="2">Usada para permitir uploads e downloads por FTP.</td>
</tr>
<tr>
<td>TCP:21</td>
</tr>
<tr>
<td>TCP:22</td>
<td>Usada para permitir login SSH no Linux.</td>
</tr>
<tr>
<td>TCP:3389</td>
<td>Usada para permitir login remoto no Windows.</td>
</tr>
<tr>
<td>TCP:443</td>
<td>Usada para fornecer serviço HTTPS de sites.</td>
</tr>
<tr>
<td>TCP:80</td>
<td>Usada para fornecer serviço HTTP de sites.</td>
</tr>
<tr>
<td>Regras de saída</td>
<td>TODAS</td>
<td>Usada para permitir todo o tráfego de saída para acesso a redes externas.</td>
</tr>
</tbody></table>

## Guia de operação
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Diagnostic Tools (Ferramentas de diagnóstico)** > **Port Verification (Verificação de portas)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Selecione uma região na parte superior da página, localize a instância que deseja verificar na lista e clique em **Quick Check (Verificação rápida)**.
4. Você pode visualizar os detalhes de detecção da porta na janela pop-up. Execute as seguintes operações conforme necessário.
   + Desmarque a porta que você não deseja detectar.
   + Insira portas personalizadas para detectar e clique em **Save (Salvar)**.
      + Protocol (Protocolo): selecione TCP ou UDP.
      + Port (Porta): insira um número de porta a ser detectado, que não pode ser igual a uma porta comum. Caso contrário, você precisa primeiro desmarcar a porta comum antes de continuar.
      + Direction (Direção): selecione **Inbound (Entrada)** ou **Outbound (Saída)**.
      + IP: insira o IP de origem para a direção de entrada e o IP de destino para a direção de saída. Insira **ALL (TODOS)** para todos os endereços IP de origem e destino.
      + É possível detectar até 15 portas personalizadas.
   
 Se você precisar detectar o tráfego de saída para o IP 10.0.1.12 usando o protocolo TCP por meio da porta 30, insira as seguintes informações na área **Custom port detection (Detecção de porta personalizada)**.

5. Quando concluir a configuração, clique em **Detect (Excluir)**. O resultado será exibido na coluna **Policy (Política)**.
<p>Suponha que você precisa abrir uma porta <b>Not opened (Não aberta)</b>, por exemplo `TCP:22`, </p>
<p>Depois, você pode adicionar uma regra de entrada para o grupo de segurança associado à instância no <a href="https://console.cloud.tencent.com/vpc/securitygroup">console do grupo de segurança</a> para abrir a porta TCP:22. Você pode selecionar <b>all (todos)</b> para <b>Source (Origem)</b>, a fim de permitir todos os IPs, ou inserir um IP (intervalo de IP) específico.</p>

## Informações relevantes
- Para obter informações sobre grupos de segurança, consulte [Visão geral de grupos de segurança](https://intl.cloud.tencent.com/document/product/215/38750) e [Adição de uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35513).
- Para obter mais informações sobre portas comuns, consulte [Portas de servidor comuns](https://intl.cloud.tencent.com/document/product/215/35520).
