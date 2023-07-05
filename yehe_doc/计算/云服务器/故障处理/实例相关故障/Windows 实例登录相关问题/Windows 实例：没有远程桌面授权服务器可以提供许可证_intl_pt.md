Este documento descreve como gerenciar prompts de alarme, como “Remote session has been disconnected as no remote desktop authorization server is available for licensing” (A sessão remota foi desconectada porque nenhum servidor de autorização de área de trabalho remota está disponível para licenciamento), quando você tenta se conectar remotamente a uma instância do Windows.

## Problema

Quando você tenta se conectar a uma instância do Windows usando a Área de Trabalho Remota do Windows, um prompt informando “Remote session has been disconnected as no remote desktop authorization server is available for licensing. For assistance, please contact your system administrator” (A sessão remota foi desconectada porque nenhum servidor de autorização de área de trabalho remota está disponível para licenciamento. Para obter ajuda, entre em contato com o administrador do sistema) é exibido, conforme a figura abaixo:
![](https://main.qcloudimg.com/raw/0034f9d4e822ca556bd54dafb9b13c17.png)

## Análise do problema

As possíveis causas desse problema incluem, entre outras, as apresentadas abaixo. Portanto, sempre analise o problema com base na situação em si.
- Por padrão, o limite do RDP-TCP é definido pelo sistema e permite apenas uma sessão para cada usuário. Se a conta estiver logada, nenhuma sessão adicional poderá ser estabelecida.
- O recurso de função “Remote Desktop Session Host (Host da Sessão da Área de Trabalho Remota)” foi adicionado pelo sistema, mas o período de validade do recurso expirou.
Esse recurso pode ser usado gratuitamente por 120 dias. Após esse período, você deve pagar pelo recurso para continuar a usá-lo.

## Solução
### Login no CVM usando o VNC

1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, localize a instância do CVM em questão e clique em **Log In (Fazer login)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Na janela **Log in to Windows Instance (Fazer login na instância do Windows)** exibida, selecione **Alternative login methods (VNC) (Métodos alternativos de login (VNC))**, e clique em **Log In Now (Fazer login agora)** para fazer login no CVM.
4. Na janela de login exibida, selecione **Send Remote Command (Enviar comando remoto)** no canto superior esquerdo e pressione **Ctrl-Alt-Delete** para acessar a interface de login do sistema, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Solução 1: modificar a configuração da política
1. Na interface do sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> para abrir uma janela do Windows PowerShell.
2. Nessa janela, digite **gpedit.msc**, e pressione **Enter** para abrir o **Local Group Policy Editor (Editor de Política de Grupo Local)**.
3. Na árvore de navegação à esquerda, selecione **Computer Configuration (Configuração do Computador)** > **Administrative Templates (Modelos Administrativos)** > **Windows Components (Componentes do Windows)** > **Remote Desktop Services (Serviços de Área de Trabalho Remota)** > **Remote Desktop Session Host (Host da Sessão da Área de Trabalho Remota)** > **Connections (Conexões)**, e clique duas vezes em **Limit number of connections (Número limite de conexões)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/e0420d2bb8ddd3e1524ee688173cb9d1.png)
4. Na janela “Limit number of connections (Número limite de conexões)” exibida, modifique o **Maximum RD connections supported (Máximo de conexões RD aceitas)** e clique em **OK**, conforme a figura abaixo:
![](https://main.qcloudimg.com/raw/066c9dfb06dc4c092424c4e1142f7471.png)
5. Alterne para a janela do Windows PowerShell.
6. Nessa janela, digite **gpupdate**, e pressione **Enter** para atualizar a política.


### Solução 2: excluir a função “Remote Desk Session Host (Host da Sessão da Área de Trabalho Remota)”
> Caso queira manter a função “Remote Desk Session Host (Host da Sessão da Área de Trabalho Remota)”, pule esta etapa e acesse o [site oficial da Microsoft](https://www.microsoft.com/) para comprar e configurar o certificado apropriado.
>
1. Na interface do sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"> para abrir o **Server Manager (Gerenciador de Servidor)**.
2. Clique em **Manage (Gerenciar)** no canto superior direito da janela “Server Manager (Gerenciador de Servidor)” e selecione **Delete roles and features (Excluir funções e recursos)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/373ef0a31c2b8e8fd1539e29852c4fab.png)
3. No assistente “Delete roles and features (Excluir funções e recursos)”, clique em **Next (Avançar)**.
4. Na página “Delete server roles (Excluir funções do servidor)”, desmarque **Remote Desktop Services (Serviços de Área de Trabalho Remota)**. Na caixa de prompt exibida, selecione **Remove Feature (Remover o recurso)**.
6. Clique em **Next (Avançar)** duas vezes.
6. Marque **Restart the destination server automatically if required (Reiniciar cada servidor de destino automaticamente, se necessário)** e clique em **Sim** na caixa de prompt exibida.
8. Clique em **Delete (Excluir)**.
Aguarde a reinicialização do CVM.






