## Descrição do erro

<span id="FaultPhenomenon1"> </span>
**Caso 1**: ao tentar se conectar a uma instância do Windows por meio da Área de Trabalho Remota do Windows, o usuário recebe o seguinte erro **The connection was denied because the user account is not authorized for remote login. (A conexão foi negada porque a conta do usuário não é autorizada para logon remoto.)**

<span id="FaultPhenomenon2"> </span>
**Caso 2**: ao tentar se conectar a uma instância do Windows por meio da Área de Trabalho Remota do Windows, o usuário recebe o seguinte erro **To sign in remotely, you need the right to sign in through Remote Desktop Services. By default, members of the Remote Desktop Users group have this right. If the group you’re in doesn’t have the right, or if the right has been removed from the Remote Desktop Users group, you need to be granted the right manually. (Para entrar remotamente, você deve ter permissão para se conectar nos Serviços de Área de Trabalho Remota. Por padrão, os membros do grupo Usuários da Área de Trabalho Remota têm esse direito. Se o grupo do qual você faz parte não tiver esse direito ou se a permissão tiver sido removida do grupo Área de Trabalho Remota, você precisará recebê-lo manualmente.)**

## Possíveis causas

O usuário não tem permissão para fazer login na instância do Windows por meio de conexões de Área de Trabalho Remota.

## Solução
- Para o [Caso 1](#FaultPhenomenon1), adicione a conta de usuário à lista de contas que são permitidas pela instância do Windows para fazer login por meio dos Serviços de Área de Trabalho Remota. Para instruções detalhadas, consulte [Permitir login remoto](#ConfigurationToAllowAccess).
- Para o [Caso 2](#FaultPhenomenon2), remova a conta de usuário da lista de contas que são negadas pela instância do Windows para fazer login por meio dos Serviços de Área de Trabalho Remota. Para instruções detalhadas, consulte [Negar login remoto](#ModifyLoginAuthority).

## Instruções

### Login no CVM usando o VNC
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, localize a instância do CVM em questão e clique em **Log In (Fazer login)**, conforme a figura a seguir:
![CVM list page](https://main.qcloudimg.com/raw/bd24015a7332c824e649c034417f708d.png)
3. Na janela **Log in to Windows Instance (Fazer login na instância do Windows)** exibida, selecione “Alternative login method (VNC) (Método alternativo de login (VNC))”, clique em **Log In Now (Fazer login agora)** para fazer login no CVM.
4. Na janela de login exibida, selecione **Send CtrlAltDel (Enviar CtrlAltDel)** no canto superior esquerdo e pressione **Ctrl-Alt-Delete** para abrir a janela de login do sistema, de acordo com a figura a seguir:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)


<span id="ConfigurationToAllowAccess"> </span>
### Permitir login remoto

>? As operações a seguir usam um Windows Server 2016 como exemplo.
>
1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, insira **gpedit.msc**, e pressione **Enter** para abrir o “Local Group Policy Editor (Editor de Política de Grupo Local)”.
2. Na árvore de navegação à esquerda, escolha **Computer Configuration (Configuração do Computador)** > **Windows Settings (Configurações do Windows)** > **Security Settings (Configurações de segurança)** > **Local Policies (Políticas locais)** > **User Rights Assignment (Atribuição de direitos de usuário)**, e clique com o botão direito em **Allow log on through Remote Desktop Services (Permitir logon pelos Serviços de Área de Trabalho Remota)**.
![](https://main.qcloudimg.com/raw/69a452fc83bb2d9013c1830ae67996ac.png)
3. Na janela de propriedades exibida, verifique se a conta de usuário que você deseja usar para fazer login remoto está na lista de usuários “Allow log on through Remote Desktop Services (Permitir logon pelos Serviços de Área de Trabalho Remota)”.
![Allow log on through Remote Desktop Services](https://main.qcloudimg.com/raw/a3d28bd18e13fe2c0ce1fceb850a3284.png)
 - Se o usuário não estiver na lista, vá para a [etapa 4](#step04).
 - Se o usuário estiver na lista, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
4. <span id="step04">Clique em **Add User or Group (Adicionar usuário ou grupo)** para abrir a janela **Select User or Group (Selecionar Usuário ou Grupo)**.</span>
5. Insira a conta que deseja usar para fazer login remoto e clique em **OK**.
6. Clique em **OK** e feche o “Local Group Policy Editor (Editor de Política de Grupo Local)”.
7. Reinicie a instância e tente se conectar à instância do Windows com a conta por meio da Área de Trabalho Remota novamente.


<span id="ModifyLoginAuthority"> </span>
### Negar login remoto

>? As operações a seguir usam um Windows Server 2016 como exemplo.
>
1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, insira **gpedit.msc**, e pressione **Enter** para abrir o “Local Group Policy Editor (Editor de Política de Grupo Local)”.
2. Na árvore de navegação à esquerda, escolha **Computer Configuration (Configuração do Computador)** > **Windows Settings (Configurações do Windows)** > **Security Settings (Configurações de segurança)** > **Local Policies (Políticas locais)** > **User Rights Assignment (Atribuição de direitos de usuário)**, e clique duas vezes em **Deny log on through Remote Desktop Services (Negar logon pelos Serviços de Área de Trabalho Remota)**, conforme mostrado abaixo:
![Deny log on through Remote Desktop Services](https://main.qcloudimg.com/raw/4c4d47a70c0d55e9c7de1f9351f4b0ab.png)
3. Na janela pop-up, verifique se a conta que você deseja usar para fazer login remoto está na lista de usuários “Deny log in through Remote Desktop Services (Negar logon pelos Serviços de Área de Trabalho Remota)”.
 - Se o usuário estiver na lista, remova a conta de usuário da lista e reinicie a instância.
 - Se o usuário não estiver na lista, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

 

