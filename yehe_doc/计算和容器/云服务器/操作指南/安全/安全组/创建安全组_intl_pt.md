## Cenário
Os grupos de segurança agem como firewalls virtuais para os CVMs. Cada instância do CVM deve estar associada a pelo menos um grupo de segurança. Por padrão, cada instância do CVM tem dois modelos (**Open all ports (Abrir todas as portas)** e **Open port 22, 80, 443, 3389 and ICMP protocol (Abrir as portas 22, 80, 443, 3389 e o protocolo ICMP)**) para criar um grupo de segurança padrão. Para obter detalhes, consulte [Visão geral de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452).

Se o grupo de segurança padrão não atender às suas necessidades, é possível criar seu próprio grupo de segurança conforme as instruções abaixo.


## Instruções

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, selecione **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)**. A página Security Group (Grupo de segurança) é exibida.
3. Selecione uma região para o grupo de segurança. Clique em **+New (+Novo)**. 
4. Na página **Create a security group (Criar um grupo de segurança)**, conclua as seguintes configurações:
![](https://main.qcloudimg.com/raw/575b2a589a58aef436bc5208facf4614.png)
 - **Template (Modelo)**: selecione um modelo que atenda às suas necessidades, conforme mostrado abaixo:
<table>
	<tr><th>Modelo</th><th>Descrição</th><th>Observações</th></tr>
	<tr><td>Abrir todas as portas</td><td>Todas as portas são abertas. Pode apresentar problemas de segurança.</td><td>-</td></tr>
	<tr><td>Abrir as portas TCP 22, 80, 443, 3389 e o ICMP</td><td>As portas TCP 22, 80, 443 e 3389 e o ICMP são abertos. Todas as portas são abertas internamente.</td><td>Adequado para instâncias com serviços web.</td></tr>
	<tr><td>Personalizado</td><td>Cria um grupo de segurança em branco no qual as regras são adicionadas posteriormente. Para obter detalhes sobre como adicionar regras, consulte <a href="https://intl.cloud.tencent.com/document/product/213/34272">este artigo</a>.</td><td>-</rd></tr>
</table>
 - **Name (Nome)**: nome do grupo de segurança.
 - **Project (Projeto)**: **Default project (Projeto padrão)** fica selecionado por padrão. Selecione um projeto para melhor gerenciamento.
 - **Notes (Observações)**: uma breve descrição do grupo de segurança.
5. Clique em **OK** para criar o grupo de segurança.
Se você selecionar **Custom (Personalizado)** como o modelo para o seu grupo de segurança, clique em **Add rules now (Adicionar regras agora)** para [adicionar regras de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
