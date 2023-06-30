## Problema

A seguinte mensagem de erro é exibida ao tentar fazer login em um CVM do Windows remotamente por meio do protocolo RDP, como usar o MSTSC.
As credenciais usadas para se conectar a `XXX.XXX.XXX.XXX` não funcionaram. Insira novas credenciais.
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## Soluções
>? Este documento usa um CVM da Tencent Cloud com o sistema operacional Windows Server 2012 como exemplo. O procedimento pode variar um pouco de acordo com a versão do sistema operacional.
> Siga as instruções abaixo e tente se conectar ao CVM do Windows após cada etapa. Se o problema persistir, vá para a próxima etapa.

### Etapa 1: modificar a política de acesso à rede
1. [Faça login em uma instância do Windows usando VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Quando fizer login, clique em <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> para abrir a janela do **Windows PowerShell**.
3. Nessa janela, digite **gpedit.msc** e pressione **Enter**. A janela **Local Group Policy Editor (Editor de Política de Grupo Local)** será exibida.
4. Na barra lateral esquerda, expanda os seguintes diretórios em ordem: **Computer Configuration (Configuração do Computador)** > **Windows Settings (Configurações do Windows)** > **Security Settings (Configurações de segurança)** > **Local Policies (Políticas locais)** > **Security Options (Opções de segurança)**.
5. Localize e abra **Network access: Sharing and security model for local accounts (Acesso à rede: modelo de compartilhamento e segurança para contas locais)** em **Security Options (Opções de segurança)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6. Selecione **Classic - local users authenticate as themselves (Clássico - os usuários locais são autenticados como eles próprios)** e clique em **OK**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. Verifique se você consegue se conectar ao CVM do Windows agora.
 - Se conseguir, o problema foi resolvido.
 - Se não conseguir, vá para a “Etapa 2: modificar a delegação de credenciais”.

### Etapa 2: modificar a delegação de credenciais
1. Na barra lateral esquerda do **Local Group Policy Editor (Editor de Política de Grupo Local)**, expanda os seguintes diretórios em ordem: **Computer Configuration (Configuração do Computador)** > **Administrative Templates (Modelos Administrativos)** > **System (Sistema)** > **Credentials Delegation (Delegação de Credenciais)**.
2. Localize e abra o **Allow delegating saved credentials with NTLM-only server authentication (Permitir delegação de credenciais salvas com autenticação de servidor somente NTML)** em **Credentials Delegation (Delegação de Credenciais)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3. Na janela pop-up, selecione **Enabled (Ativado)**. Clique em **Show… (Mostrar…)** em **Options (Opções)**, digite `TERMSRV/*` para **Show Contents (Mostrar conteúdo)** e clique em **OK**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4. Clique em **OK**.
5. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> para abrir a janela do **Windows PowerShell**.
6. Nessa janela, digite **gpupdate /force** e pressione **Enter** para atualizar a política de grupo, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. Verifique se você consegue se conectar ao CVM do Windows agora.
 - Se conseguir, o problema foi resolvido.
 - Se não conseguir, vá para a “Etapa 3: configurar credenciais locais”.

### Etapa 3: configurar credenciais locais
1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> e navegue para **Control Panel (Painel de Controle)** > **Users Accounts (Contas de usuários)** > **Credential Manager (Gerenciador de Credenciais)**. Clique em **Windows Credentials (Credenciais do Windows)** para exibir as credenciais do Windows, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. Verifique se a credencial que você usou para fazer login no CVM do Windows existe.
 - Se não existir, vá para a próxima etapa para adicionar credenciais do Windows.
 - Se existir, vá para a “Etapa 4: desativar o compartilhamento protegido por senha”.
3. Clique em **Add a Windows credential (Adicionar uma credencial do Windows)** e a janela abrirá, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. Insira o endereço IP, o nome de usuário e a senha da instância do CVM e clique em **OK**.
>?
> - O endereço IP refere-se ao endereço IP público da instância do CVM. Para mais informações, consulte [Obtenção de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/17940).
> - O nome de usuário padrão para uma instância do Windows é `Administrator` e a senha é definida quando você cria a instância. Se você esqueceu sua senha, você pode [redefinir a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
>
5. Verifique se você consegue se conectar ao CVM do Windows agora.
 - Se conseguir, o problema foi resolvido.
 - Se não conseguir, vá para a “Etapa 4: desativar o compartilhamento protegido por senha”.

### Etapa 4: desativar o compartilhamento protegido por senha
1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> e navegue para **Control Panel (Painel de Controle)** > **Network and Sharing Center (Central de Rede e Compartilhamento)** > **Advanced sharing settings (Configurações de compartilhamento avançadas)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2. Expanda a guia **All Networks (Todas as redes)**, selecione **Turn off password protected sharing (Desativar compartilhamento protegido por senha)** em **Password protected sharing (Compartilhamento protegido por senha)** e clique em **Save changes (Salvar alterações)**.
3. Verifique se você consegue se conectar ao CVM do Windows agora.
 - Se conseguir, o problema foi resolvido.
 - Se não conseguir, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) para obter ajuda.


