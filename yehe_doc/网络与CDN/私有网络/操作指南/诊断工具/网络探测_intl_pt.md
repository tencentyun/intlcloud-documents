O serviço de sondagem de rede do Tencent Cloud é usado para monitorar a qualidade das conexões de rede do VPC, incluindo latência, taxa de perda de pacotes e outras métricas importantes.

Na arquitetura de rede de nuvem híbrida, é possível usar o VPN ou o Direct Connect para conectar o VPC no Tencent Cloud ao seu próprio IDC. Para monitorar a qualidade das conexões da rede em tempo real, você pode criar uma sonda de rede na sub-rede que precisa se comunicar com o IDC. Depois, você obterá a taxa de perda de pacotes e a latência do link testado e atenderá às seguintes finalidades:

- Monitoramento em tempo real da qualidade da conexão
- Alarme de falha de conexão em tempo real

## Instruções

- O serviço de sondagem de rede adota o método ping com uma frequência de 20 detecções por minuto.
- São permitidas até 50 sondas para cada VPC.
- No máximo 20 sub-redes no mesmo VPC podem ter sondas de rede.

## Criação de uma sonda de rede

1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Clique em **+New (+Novo)** na parte superior da página **Network Probe (Sonda de rede)**.
4. Na janela pop-up **Create Network Probe (Criar sonda de rede)**, preencha os campos relevantes.
>?
>- A rota da sonda de rede é atribuída pelo sistema e não pode ser modificada.
>- Quando você muda a rota da sub-rede, esta rota padrão será removida da tabela de rotas original associada à sub-rede e adicionada à nova tabela de rotas associada.

![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
**Descrição dos campos**

<table>
<thead>
<tr>
<th>Campo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody><tr>
<td>Name (Nome)</td>
<td>Nome da sonda de rede.</td>
</tr>
<tr>
<td>VPC</td>
<td>O VPC ao qual pertence o IP de origem da sonda.</td>
</tr>
<tr>
<td>Subnet (Sub-rede)</td>
<td>A sub-rede à qual pertence o IP de origem da sonda.</td>
</tr>
<tr>
<td>Probe Destination IP (IP de destino da sonda)</td>
<td>No máximo dois IPs de destino são aceitos para a sonda de rede. Certifique-se de ter habilitado a política de firewall ICMP para o servidor de destino da sonda de rede.</td>
</tr>
<tr>
<td>Next hop (Próximo salto)</td>
<td>Você pode escolher "Specify (Especificar)" ou "Do Not Specify (Não especificar)" o próximo salto. <ul><li>Se "Do Not Specify (Não especificar)" for selecionado, nenhum próximo salto será selecionado.<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Observação:
</div>
<p>Se você não quiser especificar o próximo salto,<a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC&level3_id=185&radio_title=%E5%85%B6%E4%BB%96%E9%97%AE%E9%A2%98&queue=96&scene_code=16314&step=2">envie um tíquete</a> para habilitar esta funcionalidade de lista de permissões.</p></li><li>Se você especificar o próximo salto, selecione o tipo e as instâncias dele. Depois, o sistema adiciona automaticamente a rota de 32 bits correspondente à tabela de rotas associada à sub-rede.</li></ul></td>
</tr>
</tbody></table>

5. **Verifique** o **IP de destino da sonda**
	- Se a conexão obtiver êxito, clique em **OK**.
	- Se a conexão falhar, verifique se a rota de sub-rede está configurada corretamente e se o dispositivo de sonda habilita ACL de rede, grupo de segurança ou outros firewalls, que podem bloquear a conexão. Para obter mais informações, consulte [Gerenciamento de ACLs de rede](https://intl.cloud.tencent.com/document/product/215/31852) e [Modificação de uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35515).

## Verificação da latência e perda de pacotes de uma sonda de rede

1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Clique no ícone de monitoramento da instância de sonda de rede de destino para exibir sua latência e taxa de perda de pacotes.
   ![](https://main.qcloudimg.com/raw/b1a8a96df051a50cf58fd6f34b09a228.png)

## Modificação de uma sonda de rede

1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Na lista, localize a sonda de rede a ser modificada e clique em **Edit (Editar)** na coluna de operação.
![](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. Na janela pop-up **Edit Network Probe (Editar sonda de rede)** (este exemplo não tem o próximo salto especificado), faça as alterações necessárias e clique em **Submit (Enviar)** para salvar as alterações.
![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## Exclusão de uma sonda de rede
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Diagnostic Tools (Ferramentas de diagnóstico)** -> **Network Probe (Sonda de rede)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Na lista, localize a sonda de rede a ser excluída e clique em **Delete (Excluir)** na coluna de operação.
4. Clique em **Delete (Excluir)** na janela pop-up para confirmar a exclusão.
 >!A exclusão de uma sonda de rede também exclui todas as rotas relacionadas.

 ![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)
