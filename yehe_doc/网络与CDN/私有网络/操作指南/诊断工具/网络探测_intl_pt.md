O serviço de sondagem de rede da Tencent Cloud é usado para monitorar a qualidade das conexões de rede da VPC, incluindo a latência, a taxa de perda de pacotes e outras métricas importantes.

Na arquitetura de rede de nuvem híbrida, você cria uma sonda de rede na sub-rede que precisa se comunicar com o IDC para monitorar a taxa de perda de pacotes e a latência da ligação sondada. A configuração permite: 
- Monitorar a qualidade da conexão
- Receber alertas em caso de falhas de conexão

## Instruções
- O serviço de sondagem de rede adota o método ping com uma frequência de 20 pings por minuto.
- São permitidas até 50 sondas para cada VPC.
- É possível ter sondas de rede em no máximo 20 sub-redes na mesma VPC.

## Criação de uma sonda de rede
1. Faça login no [console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Clique em **+New (+Novo)** na parte superior da página **Network Probe (Sonda de rede)**.
4. Na janela pop-up **Create Network Probe (Criar sonda de rede)**, preencha os campos relevantes.
>?
>- A rota da sonda de rede é atribuída pelo sistema e não pode ser modificada.
>- Quando você muda a rota da sub-rede, esta rota padrão será removida da tabela de rotas original associada à sub-rede e adicionada à nova tabela de rotas associada.
>
![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
**Descrição dos campos**
<table>
<thead>
<tr>
<th>Campo</th>
<th>Configuração</th>
</tr>
</thead>
<tbody><tr>
<td>Name (Nome)</td>
<td>Nome da sonda de rede.</td>
</tr>
<tr>
<td>VPC</td>
<td>A VPC ao qual pertence o IP de origem da sonda.</td>
</tr>
<tr>
<td>Subnet (Sub-rede)</td>
<td>A sub-rede à qual pertence o IP de origem da sonda.</td>
</tr>
<tr>
<td>Probe Destination IP (IP de destino da sonda)</td>
<td>São aceitos no máximo dois IPs de destino para a sonda de rede. Não se esqueça de ativar a política de firewall ICMP para o servidor de destino da sonda de rede.</td>
</tr>
<tr>
<td>Source Next Hop (Próximo salto de origem)</td>
<td>Você pode escolher <b>Specify (Especificar)</b> ou <b>Do Not Specify (Não especificar)</b> o próximo salto. <ul><li>Se <b>Do Not Specify (Não especificar)</b> for marcado, nenhum próximo salto será selecionado.<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Observação:
</div>
<p>Atualmente, a opção **Do Not Specify (Não especificar)** só está disponível para usuários beta. Para ativá-la, <a href="https://console.cloud.tencent.com/workorder/category">envie um tíquete</a>.</p></li><li>Se você especificar o próximo salto, selecione o tipo do próximo salto e as instâncias. Depois, o sistema adiciona automaticamente a rota de 32 bits correspondente à tabela de rotas associada à sub-rede. Atualmente, o tipo do próximo salto aceito inclui NAT Gateway, Peering Connections, gateway do VPN, gateway do Direct Connect, CVM e CCN.<p>
<dx-alert infotype="explain" title="">
Se você especificar o CCN como o próximo salto e os IPs de destino da sonda pertencerem a dois VPCs no CCN, o intervalo de IP com a máscara mais longa será correspondido e entrará em vigor.
</dx-alert>
</li></ul></td>
</tr>
</tbody></table>
5. (Opcional) **Verifique** o **IP de destino da sonda**.
>?Ignore essa etapa se você não especificar o próximo salto.
 - Se a conexão obtiver êxito, clique em **OK**.
 - Se a conexão falhar, verifique se a rota da sub-rede está configurada corretamente e se o dispositivo de sonda habilita a ACL de rede, o grupo de segurança ou outros firewalls, que podem bloquear a conexão. Para mais informações, consulte [Gerenciamento de ACLs de rede](https://intl.cloud.tencent.com/document/product/215/31852) e [Modificação de uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35515).

## Verificação da latência e perda de pacotes de uma sonda de rede

1. Faça login no [console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Clique no ícone de monitoramento da instância de sonda de rede em questão para exibir sua latência e taxa de perda de pacotes.
	![](https://main.qcloudimg.com/raw/b1a8a96df051a50cf58fd6f34b09a228.png)

## Modificação de uma sonda de rede
1. Faça login no [console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Na lista, localize a sonda de rede a ser modificada e clique em **Edit (Editar)** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. Na janela pop-up **Edit Network Probe (Editar sonda de rede)**, faça as alterações necessárias e clique em **Submit (Enviar)** para salvar as alterações.
>?
>- Esse exemplo não tem o próximo salto especificado.
>- Se nenhum próximo salto for especificado, o nome, o IP de destino da sonda e as observações da sonda de rede podem ser modificados.
>- Se algum próximo salto for especificado, o nome, o IP de destino da sonda, o próximo salto da origem e as observações da sonda de rede podem ser modificados.
> 
 ![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## Exclusão de uma sonda de rede
1. Faça login no [console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Na lista, localize a sonda de rede a ser excluída e clique em **Delete (Excluir)** na coluna **Operation (Operação)**.
4. Clique em **Delete (Excluir)** na janela pop-up para confirmar a exclusão.
>!A exclusão de uma sonda de rede também exclui todas as políticas de alarme associadas e as rotas configuradas. Verifique se os seus negócios serão afetados antes de continuar.
>
  ![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)

## Configuração de uma política de alarme
Você pode configurar uma política de alarme para o serviço de sondagem de rede, para que possa detectar prontamente qualquer exceção de rota, a fim de ajudar a alternar as rotas rapidamente e a garantir a disponibilidade dos negócios.
1. Faça login no console do CM e acesse a página [**Alarm Policy (Política de alarme)**](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Clique em **Create (Criar)**.
3. Na janela pop-up **Create Alarm Policy (Criar política de alarme)**, insira o nome da política, selecione **Network Probe (Sonda de rede)** para o tipo de política, configure o objeto de alarme, a condição de disparo do alarme e a política de alarme e clique em **Complete (Concluir)**.
