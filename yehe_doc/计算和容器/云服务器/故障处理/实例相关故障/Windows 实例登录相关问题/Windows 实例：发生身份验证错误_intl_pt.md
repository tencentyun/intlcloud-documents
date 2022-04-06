## Descrição do problema

Quando os usuários tentam fazer login em uma instância do Windows por meio de uma Conexão de Desktop Remota e acontece um erro.
- A mensagem de erro indica “Authentication error. The token supplied to the function is invalid.” (Erro de autenticação. O token fornecido para a função é inválido.).
- “Authentication error. The requested function is not supported.”. (Erro de autenticação. A função solicitada não é compatível.).

## Análise do problema

A Microsoft lançou uma atualização de segurança em março de 2018. Ao corrigir como o protocolo Credential Security Support Provider (CredSSP) valida solicitações durante a autenticação, essa atualização corrige a vulnerabilidade de execução remota de código no CredSSP. Tanto o cliente quanto o servidor precisam instalar a atualização de segurança ou o erro anterior pode ocorrer.
A conexão remota falha nas seguintes condições:

- Condição 1: a atualização de segurança foi instalada no servidor, mas não no cliente, e a política “force updated clients (forçar clientes atualizados)” está configurada.
- Condição 2: a atualização de segurança foi instalada no cliente, mas não no servidor, e a política “force updated clients (forçar clientes atualizados)” está configurada.
- Condição 3: a atualização de segurança foi instalada no cliente, mas não no servidor, e a política “mitigated (mitigada)” está configurada.

## Solução

> Caso precise executar apenas uma atualização local do cliente, use a [Solução 1: instalar a atualização de segurança (recomendado)](#step4).
>
### Login no CVM usando VNC

1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, localize a instância do CVM em questão e clique em **Log In (Fazer login)**.
3. Na janela **Log in to Windows instance (Fazer login na instância do Windows)** exibida, selecione **Alternative login methods (VNC) (Métodos alternativos de login (VNC))** e clique em **Log In Now (Fazer login agora)**.
4. Na janela de login exibida, selecione **Send CtrlAltDel (Enviar CtrlAltDel)** no canto superior esquerdo e clique em **Ctrl-Alt-Delete** para acessar a página de login do sistema.

<span id="step4"></span>
### Solução 1: instalar a atualização de segurança (recomendado)

Instale a atualização de segurança no cliente ou servidor sem patch. Para obter atualizações para diferentes sistemas operacionais, consulte [CVE-2018-0886 | Vulnerabilidade de execução remota de código do CredSSP](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886). Essa solução usa o Windows Server 2016 como exemplo.
Em outros sistemas operacionais, você pode usar os métodos a seguir para acessar o **Windows Update**.
- Windows Server 2012: <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"></img> > **Control Panel (Painel de Controle)** > **System and Security (Sistema e Segurança)** > **Windows Update**
- Windows Server 2008: **Start (Iniciar)** > **Control Panel (Painel de Controle)** > **System and Security (Sistema e Segurança)** > **Windows Update**
- Windows 10: <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> > **Settings (Configurações)** > **Update and Security (Atualização e segurança)**
- Windows 7: <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 28px;"></img> > **Control Panel (Painel de Controle)** > **System and Security (Sistema e Segurança)** > **Windows Update**


1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> e selecione **Settings (Configurações)**.
2. Nessa janela, selecione **Update and Security (Atualização e Segurança)**.
3. Nessa página, selecione **Windows Update** e clique em **Check for updates (Procurar atualizações)**.
4. Clique em **Install updates (Instalar Atualizações)**.
5. Após a conclusão da instalação, reinicie a instância para finalizar a atualização.

### Solução 2: modificar a política

Com a atualização de segurança instalada no CVM, defina a política **Encryption Oracle Remediation (Remediação de criptografia da Oracle)** como **vulnerable (vulnerável)**. Essa solução usa o Windows Server 2016 como exemplo. Conclua as seguintes etapas:
> Se nenhum editor de política de grupo estiver disponível no sistema operacional Windows 10 Home, você poderá modificar a política no registro. Para mais detalhes, consulte a [Solução 3: modificar o registro](#Plan3).
>
1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, insira **gpedit.msc**, e pressione **Enter** para abrir o “Local Group Policy Editor (Editor de Política de Grupo Local)”.
> Você também pode pressionar **Win+R** para abrir a caixa de diálogo **Run (Executar)**.
>
3. Na árvore de navegação esquerda, selecione **Computer Configuration (Configuração do Computador)** > **Administrative Templates (Modelos Administrativos)** > **System (Sistema)** > **Credentials Delegation (Delegação de Credenciais)** e clique duas vezes em **Encryption Oracle Remediation (Remediação de criptografia da Oracle)**.
4. Nessa janela, selecione **Enabled (Ativada)** e defina **Protection Level (Nível de proteção)** como **Vulnerable (Vulnerável)**.
5. Clique em **OK** para concluir a configuração.

<span id="Plan3"></span>
### Solução 3: modificar o registro

1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, insira **regedit**, e pressione **Enter** para abrir o “Registry Editor (Editor do Registro)”.
> Você também pode pressionar **Win+R** para abrir a caixa de diálogo **Run (Executar)**.
> 
2. Na árvore de navegação esquerda, selecione **Computer (Computador)** > **HKEY_LOCAL_MACHINE** > **Software** > **Microsoft** > **Windows** > **CurrentVersion (Versão atual)** > **Policies (Políticas)** > **System (Sistema)** > **CredSSP** > **Parameters (Parâmetros)**.
> Se esse caminho não existir, crie um manualmente.
>
4. Clique com o botão direito em **Parameters (Parâmetros)**, selecione **New (Novo)** > **DWORD (32-bit) value (Valor DWORD (32 bits))** e nomeie o arquivo como “AllowEncryptionOracle”.
5. Clique duas vezes no novo arquivo, defina o “Value data (Dados de valor)” como “2” e clique em **OK**.
6. Reinicie a instância.

## Documentos relacionados

- [CVE-2018-0886 | Vulnerabilidade de execução remota de código do CredSSP](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [Atualizações do CredSSP para CVE-2018-0886](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)
