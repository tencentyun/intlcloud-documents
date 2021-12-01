## Cenário de operação
Um grupo de segurança é um firewall virtual para instâncias do CVM. Cada instância do CVM deve pertencer a pelo menos um grupo de segurança. O Tencent Cloud oferece dois modelos: **Open all ports to the Internet (Abrir todas as portas para a internet)** e **Open ports 22, 80, 443, and 3389 and ICMP protocol to the Internet (Abrir as portas 22, 80, 443 e 3389 e o protocolo ICMP para a internet)**. Com esses modelos, é possível criar um grupo de segurança padrão durante a criação de uma instância do CVM, caso ainda não o tenha criado. 

Se você não deseja que sua instância do CVM se junte ao grupo de segurança padrão, é possível criar outro no console do CVM da seguinte maneira:


## Etapas
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, clique em **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)** para ter acesso à pagina de gerenciamento de grupos de segurança.
3. Na página de gerenciamento de grupos de segurança, selecione **Region (Região)** e clique em **+Create (+Criar)**.
4. Na janela **Create a security group (Criar um grupo de segurança)** exibida, conclua a configuração, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/dc265c99d23e7a05bb9cc8b72f2cebee.png)
 - Modelo: com base nos serviços a serem implantados para as instâncias do CVM no grupo de segurança, selecione um modelo apropriado para simplificar a configuração das regras do grupo, conforme descrito na tabela a seguir:
<table>
	<tr><th>Modelo</th><th>Descrição</th><th>Cenário</th></tr>
	<tr><td>Open all ports to the Internet (Abrir todas as portas para a internet)</td><td>Por padrão, todas as portas serão abertas para a internet e rede privada; o que, no entanto, pode incorrer em riscos de segurança.</td><td>-</td></tr>
	<tr><td>Open ports 22, 80, 443, and 3389 and the ICMP protocol to the Internet (Abrir as portas 22, 80, 443 e 3389 e o protocolo ICMP para a internet)</td><td>Por padrão, as portas 22, 80, 443 e 3389 e o protocolo ICMP serão abertos para a internet. Além disso, todas as portas serão abertas para a rede privada.</td><td>O serviço Web precisa ser implantado para as instâncias no grupo de segurança.</td></tr>
	<tr><td>Custom (Personalizado)</td><td>Depois de criar um grupo de segurança, você pode adicionar regras a ele conforme necessário. Para obter informações detalhadas sobre a operação, consulte <a href="https://intl.cloud.tencent.com/document/product/215/35513">Adição de regras de grupo de segurança</a>.</td><td>-</rd></tr>
</table>
 - Name (Nome): personalize o nome de um grupo de segurança.
 - Project (Projeto): **Default project (Projeto padrão)** fica selecionado por padrão. Você também pode especificar outro projeto para facilitar o gerenciamento futuro.
 - Remarks (Observações): descreve resumidamente o grupo de segurança para facilitar o gerenciamento futuro.
5. Clique em **OK** para finalizar a criação do grupo de segurança.
Se você selecionar o modelo **Custom (Personalizado)** ao criar um grupo de segurança, clique em **Set rules now (Definir as regras agora)** após a criação para [adicionar regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35513).
