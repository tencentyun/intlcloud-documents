Este documento descreve problemas comuns que você pode encontrar ao fazer login no CVM do Windows no Mac por meio da Área de Trabalho Remota da Microsoft, e como resolvê-los.
## Problemas

- Ao fazer login no CVM do Windows por meio da Área de Trabalho Remota da Microsoft, você recebe um prompt “The certificate couldn't be verified back to a root certificate (O certificado não pôde ser validado com o certificado raiz)”.

<img src="https://main.qcloudimg.com/raw/070b9c862d6928988768b266461bc816.png" data-nonescope="true" />

- Ao usar a Conexão de Área de Trabalho Remota no Mac, você recebe um prompt “Remote Desktop Connection cannot verify the identity of the computer that you want to connect to (A Conexão de Área de Trabalho Remota não pode verificar a identidade do computador ao qual você deseja se conectar)”.


## Solução de problemas
> As operações a seguir usam um Windows Server 2016 como exemplo.
>

### Login no CVM usando o VNC

1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, localize o CVM que você precisa e clique em **Log In (Fazer login)**. Verifique a figura abaixo para mais detalhes.
![Login](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Na janela **Log into Windows instance (Fazer login na instância do Windows)** exibida, selecione **Alternative login methods (VNC) (Métodos de login alternativos (VNC))** e clique em **Log In Now (Fazer login agora)** para fazer login no CVM.
4. Na janela de login exibida, selecione **Send CtrlAltDel (Enviar CtrlAltDel)** no canto superior esquerdo, e clique em **Ctrl-Alt-Delete** para acessar a interface de login do sistema conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Modificação da política de grupo local da instância

1. Na interface do sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, insira **gpedit.msc**, e pressione **Enter** para abrir o Local Group Policy Editor (Editor de Política de Grupo Local).
> Você também pode usar o atalho “Win+R” para abrir a interface Run (Executar).
>
2. Na árvore de navegação à esquerda, selecione **Computer Configuration (Configuração do Computador)** > **Administrative Templates (Modelos Administrativos)** > **Windows Components (Componentes do Windows)** > **Remote Desktop Services (Serviços de Área de Trabalho Remota)** > **Remote Desktop Session Host (Host de Sessão da Área de Trabalho Remota)** > **Security (Segurança)**, clique duas vezes em **Require use of specific security layer for remote (RDP) connections (Solicitar o uso de camada de segurança específica para conexões remotas (RDP))**
3. Nessa janela, selecione **Enabled (Ativado)** e defina **Security Layer (Camada de Segurança)** como **RDP** 
4. Clique em **OK** para concluir a configuração.
5. Reinicie a instância e tente se conectar novamente.
Se a conexão falhar novamente, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
